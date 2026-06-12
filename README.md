# 🔐 A Importância da Segurança AWS — Postura de Segurança para Farmácia Vida+

**Implementação de Controles de Identidade, Proteção de Dados e Detecção de Ameaças em Ambiente AWS, com foco em conformidade LGPD**

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![Security](https://img.shields.io/badge/Security-Best_Practices-green)
![Cloud Practitioner](https://img.shields.io/badge/AWS-Cloud_Practitioner-blue)
![Compliance](https://img.shields.io/badge/LGPD-Compliance-purple)
![Status](https://img.shields.io/badge/Status-Concluído-success)

---

## 1. Problema de Negócio

A **Farmácia Vida+** (rede varejista farmacêutica com operação híbrida — e-commerce e lojas físicas) migrou seu sistema de vendas e prontuários eletrônicos para a AWS. Por armazenar dados sensíveis de saúde (receitas médicas, CPFs vinculados a medicamentos controlados e histórico clínico), a empresa se tornou um alvo crítico para vazamento de dados e ataques de ransomware.

O risco real não é apenas técnico: é regulatório e financeiro. A LGPD prevê sanções de até **2% do faturamento por infração**, e qualquer indisponibilidade do sistema de vendas paralisa simultaneamente o e-commerce e os caixas das lojas físicas.

Este projeto responde à pergunta central: **como reduzir, com três controles AWS priorizados, a exposição a vazamento de dados, sequestro de credenciais e indisponibilidade operacional — sem adicionar complexidade desproporcional ao porte da empresa?**

---

## 2. Contexto e Baseline (Cenário Atual)

Antes da implementação, o ambiente da Vida+ apresentava três fragilidades estruturais:

| Dimensão | Situação Atual (Baseline) |
|---|---|
| **Identidade** | Contas IAM compartilhadas entre funcionários, sem MFA ativo. Desenvolvedores com `AdministratorAccess` permanente. |
| **Dados** | Receitas médicas armazenadas em buckets S3 sem criptografia forçada no servidor e com políticas de acesso excessivamente abertas. |
| **Visibilidade** | Nenhum monitoramento centralizado. Detecção de incidentes é puramente reativa — depende de relato manual. |

Esse baseline é o ponto de comparação para medir o impacto de cada medida implementada nas seções seguintes.

---

## 3. Premissas

- O escopo considera **1 conta AWS de produção**, região `us-east-1`.
- O Modelo de Responsabilidade Compartilhada da AWS é o ponto de partida: a AWS cobre a infraestrutura física; a Vida+ é responsável pela configuração de identidade, dados e monitoramento.
- As três medidas foram selecionadas por critério de **maior redução de risco por menor esforço de implementação**, adequado a uma farmácia de médio porte (não uma operação enterprise multi-conta).
- Dados de receitas médicas e fiscais possuem exigência de retenção mínima de 5 anos para fins de auditoria.

---

## 4. Estratégia da Solução — Arquitetura

```
Usuários
   │
   ▼
AWS IAM + MFA (Identidade)
   │
   ▼
Recursos AWS
┌─────────┬─────────┬─────────┐
│   EC2   │   S3     │   RDS   │
└─────────┴─────────┴─────────┘
   │
   ▼
AWS CloudTrail (Auditoria imutável)
   │
   ▼
AWS GuardDuty + Prowler (Detecção e Compliance)
   │
   ▼
EventBridge + SNS → Alertas para a equipe de TI
```

A arquitetura segue o princípio de **defesa em profundidade**: cada camada (identidade, dados, observabilidade) é independente, de forma que a falha de um controle não compromete os demais.

---

## 5. Decisões Técnicas e Trade-offs

Esta seção documenta não apenas *o que* foi implementado, mas *por que* — incluindo as alternativas descartadas e os trade-offs conscientemente aceitos.

### Medida 1 — AWS IAM com Privilégio Mínimo e MFA Obrigatório

**O que resolve:** elimina o risco de acesso não autorizado por credenciais compartilhadas ou roubadas, e impede escalada de privilégios por funcionários de balcão ou administradores.

**Implementação:**
- Fim das contas compartilhadas; cada colaborador possui identidade individual.
- Políticas RBAC: farmacêuticos têm acesso de leitura às receitas; operadores de caixa apenas gravam vendas; exclusão de logs é bloqueada via Service Control Policies (SCPs) no AWS Organizations.
- MFA obrigatório para todas as contas, com prioridade absoluta para perfis administrativos e acesso root.

**Alternativa considerada:** AWS IAM Identity Center (federação corporativa completa, multi-conta).
**Racional da escolha:** para uma conta única, grupos IAM + SCPs entregam o mesmo princípio de menor privilégio com configuração mais simples e auditável, sem a sobrecarga operacional de um Identity Provider externo.
**Trade-off aceito:** menor preparo para expansão multi-conta no curto prazo, em troca de implementação mais rápida e curva de manutenção compatível com uma equipe de TI pequena.

---

### Medida 2 — Amazon S3: Criptografia com AWS KMS + Object Lock

**O que resolve:** garante **confidencialidade** (dados ilegíveis sem a chave correta) e **integridade** (impossibilidade de alteração ou exclusão de registros, mesmo por um atacante com credenciais root comprometidas).

**Implementação:**
- Criptografia SSE-KMS forçada via política de bucket, com Customer Managed Keys (CMKs).
- AWS S3 Object Lock em modo **Compliance**, com retenção de 5 anos para receitas e relatórios fiscais — bloqueio de exclusão/alteração mesmo pela conta root.
- Bloqueio total de acesso público ao S3 em nível de conta.

**Alternativa considerada:** criptografia client-side antes do upload.
**Racional da escolha:** SSE-KMS com CMK gera trilha de auditoria nativa de uso de chaves via CloudTrail, sem exigir que a aplicação gerencie chaves criptográficas — reduzindo superfície de erro humano.
**Trade-off aceito:** pequeno overhead de custo e latência por chamada ao KMS, em troca de auditabilidade total e proteção definitiva contra ransomware via Object Lock.

---

### Medida 3 — Auditoria Contínua com Prowler + AWS Systems Manager Session Manager

**O que resolve:** transforma a postura de segurança de **reativa para proativa**, identificando desvios de conformidade (CIS Benchmark, ISO 27001) antes que se tornem incidentes.

**Implementação:**
- Instância EC2 em sub-rede privada, com acesso administrativo via **AWS Systems Manager Session Manager** — elimina a necessidade de expor a porta SSH (22) à internet.
- **Prowler 4.0+** integrado via script automatizado (`prowler_scan.sh`), executando varreduras semanais de conformidade.
- AWS CloudTrail registrando todas as chamadas de API (quem, de onde, o quê, com qual resultado), com integridade validada por **S3 Log File Integrity Validation**.
- EventBridge + SNS disparando alertas por e-mail à equipe de TI quando a pontuação de conformidade cai ou vulnerabilidades críticas são detectadas.

**Alternativa considerada:** depender exclusivamente do AWS GuardDuty (detecção comportamental baseada em ML).
**Racional da escolha:** GuardDuty é excelente para detectar comportamento anômalo em tempo real, mas não avalia configurações estáticas contra frameworks regulatórios. O Prowler complementa essa lacuna com relatórios de compliance estruturados, prontos para auditoria.
**Trade-off aceito:** varreduras do Prowler são periódicas (não em tempo real), em troca de cobertura ampla de configurações e relatórios diretamente utilizáveis em processos de auditoria externa.

---

## 6. Mapeamento da Tríade de Segurança (CIA + Não Repúdio)

| Pilar | Risco de Negócio Associado | Serviço AWS | Mecanismo de Proteção |
|---|---|---|---|
| **Confidencialidade** | Vazamento de receitas médicas e dados de clientes | IAM + KMS | Acesso restrito por função + criptografia de chaves |
| **Integridade** | Alteração fraudulenta de logs ou dados fiscais | CloudTrail (File Validation) + S3 Object Lock | Assinaturas criptográficas e imutabilidade de registros |
| **Disponibilidade** | Paralisação do sistema de vendas por ataque direcionado | GuardDuty + Prowler | Detecção precoce de varreduras e configurações vulneráveis |
| **Não Repúdio** | Negação de autoria de ação crítica no sistema | CloudTrail | Trilha histórica imutável vinculando identidade à ação |

---

## 7. Resultados e Impacto de Negócio (Business Performance)

| Indicador | Antes (Baseline) | Depois (Com a Solução) |
|---|---|---|
| MFA habilitado | 0% | 100% |
| Usuários com privilégios excessivos | Múltiplos (incluindo devs com AdministratorAccess) | 0 |
| Cobertura de auditoria (CloudTrail) | Inexistente | 100% das chamadas de API |
| Tempo de detecção de incidente | Reativo (dias) | Minutos (GuardDuty + alertas automatizados) |
| Tempo de preparação de relatório de auditoria | Semanas | Minutos (Prowler automatizado) |

**Tradução financeira do risco mitigado:**
- **Risco regulatório:** exposição a multas de até 2% do faturamento por vazamento de dados de saúde é mitigada na camada de infraestrutura antes que o dado saia do ambiente controlado.
- **Continuidade operacional:** com S3 Object Lock ativo, o cenário de paralisação total das lojas por ransomware — que interromperia 100% do faturamento diário das operações físicas e online — passa de risco ativo para risco residual próximo de zero.
- **Custo de auditoria:** consolidação automatizada via Prowler reduz o esforço de preparação de evidências de conformidade de semanas-pessoa para minutos.

---

## 8. Modelo de Responsabilidade Compartilhada na Prática

| Camada | Responsável | Aplicação no Projeto |
|---|---|---|
| Data centers, hardware, rede física, virtualização | **AWS** | Infraestrutura subjacente ao IAM, S3, EC2, CloudTrail e GuardDuty |
| Configuração de IAM, criptografia (KMS), Object Lock, monitoramento e resposta a alertas | **Farmácia Vida+** | Toda a Seção 5 deste projeto |

O projeto concentra-se inteiramente na camada de responsabilidade do cliente — onde, na prática, a maioria dos incidentes de segurança em nuvem se origina.

---

## 9. Como Executar (Templates de Infraestrutura)

Os templates CloudFormation de referência estão em `/templates`:

```bash
# Habilita o CloudTrail
aws cloudformation deploy \
  --template-file templates/cloudtrail-template.yaml \
  --stack-name vidaplus-cloudtrail

# Habilita o GuardDuty
aws cloudformation deploy \
  --template-file templates/guardduty-template.yaml \
  --stack-name vidaplus-guardduty

# Habilita o Security Hub
aws cloudformation deploy \
  --template-file templates/securityhub-template.yaml \
  --stack-name vidaplus-securityhub
```

**Pré-requisitos:** AWS CLI configurado com credenciais que possuam permissão para criar os recursos acima.

---

## 10. Estrutura do Repositório

```
a-Importancia-da-seguranca-AWS/
│
├── README.md
│
├── docs/
│   ├── RELATORIO_EXECUTIVO.md
│   ├── arquitetura-seguranca.md
│   ├── aws-security-best-practices.md
│   ├── business-value.md
│   ├── incident-response-plan.md
│   ├── lgpd-compliance.md
│   ├── modelo-responsabilidade-compartilhada.md
│   └── plano-remediacao.md
│
├── diagrams/
│   └── arquitetura.drawio
│
├── templates/
│   ├── cloudtrail-template.yaml
│   ├── guardduty-template.yaml
│   └── securityhub-template.yaml
│
├── .github/workflows/
│   └── security-scan.yml
│
└── LICENSE
```

---

## 11. Próximos Passos

- **AWS Security Hub:** consolidar os achados do Prowler e GuardDuty em um painel único com score de segurança da organização.
- **Amazon Macie:** automatizar a descoberta e classificação de dados PII (CPFs, dados de pagamento) em buckets S3, garantindo que nenhum dado sensível esteja fora do escopo protegido.
- **AWS Config:** monitorar continuamente configurações de recursos para impedir que um bucket S3 seja alterado acidentalmente para acesso público.
- **Expansão multi-conta:** avaliar migração para AWS IAM Identity Center caso a Vida+ passe a operar múltiplas contas AWS (ambientes de dev/staging/produção separados).

---

## Competências Demonstradas

`AWS IAM` · `AWS KMS` · `Amazon S3 (Object Lock)` · `AWS CloudTrail` · `AWS GuardDuty` · `Prowler` · `AWS Systems Manager` · `Governança Cloud` · `LGPD` · `Modelo de Responsabilidade Compartilhada` · `Resposta a Incidentes` · `Arquitetura de Segurança em Camadas`

---

**Autor:** Sérgio Luiz dos Santos — Senior Data Engineer & Cloud Architect | Sistemas Críticos e Governança de Dados

[![Portfólio](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)
