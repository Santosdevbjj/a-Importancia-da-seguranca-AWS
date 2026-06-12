## Formação AWS Cloud Practitioner Certification.

<img width="122" height="120" alt="1000127470" src="https://github.com/user-attachments/assets/30bc674a-68d1-4fcb-ae8d-bed9baca297e" />


---

## 🔐 A Importância da Segurança AWS

Implementação de Controles de Segurança para uma Farmácia em Ambiente Cloud


"AWS" (https://img.shields.io/badge/AWS-Cloud-orange)
"Security" (https://img.shields.io/badge/Security-Best_Practices-green)
"Cloud Practitioner" (https://img.shields.io/badge/AWS-Cloud_Practitioner-blue)
"Status" (https://img.shields.io/badge/Status-Concluído-success)

---

📖 Sobre o Projeto

A segurança da informação é um dos pilares fundamentais da computação em nuvem.

Este projeto foi desenvolvido como parte da formação AWS Cloud Practitioner Certification, com o objetivo de demonstrar a aplicação prática de serviços AWS voltados para proteção de ambientes corporativos.

O cenário proposto considera uma farmácia fictícia chamada Farmácia VidaPlus, que armazena informações sensíveis de clientes, receitas médicas, dados financeiros e registros operacionais.

A missão deste projeto é identificar riscos de segurança e implementar controles capazes de aumentar a proteção dos ativos digitais da organização utilizando serviços nativos da AWS.

---

🎯 Objetivo

Projetar uma estratégia de segurança baseada em três serviços essenciais da AWS:

- AWS IAM
- AWS Security Hub
- AWS CloudTrail

A solução busca garantir:

- Controle de acesso seguro
- Monitoramento contínuo
- Auditoria completa
- Conformidade regulatória
- Proteção de dados sensíveis

---

🏥 Cenário de Negócio

Empresa

Farmácia VidaPlus

Segmento

Varejo Farmacêutico

Desafio

A organização enfrenta desafios relacionados à:

- Controle inadequado de acessos
- Falta de rastreabilidade
- Ausência de monitoramento centralizado
- Necessidade de adequação à LGPD
- Crescimento acelerado do ambiente digital

---

🚨 Problemas Identificados

1. Permissões Excessivas

Usuários possuíam acesso além do necessário para execução de suas atividades.

Impacto

- Acesso indevido
- Alterações não autorizadas
- Exclusão acidental de recursos

---

2. Falta de Visibilidade

Eventos de segurança estavam distribuídos em múltiplos serviços.

Impacto

- Detecção tardia de incidentes
- Dificuldade de investigação

---

3. Ausência de Auditoria Completa

Não existia trilha confiável de auditoria.

Impacto

- Não conformidade
- Dificuldade em identificar responsáveis por alterações

---

🛠️ Serviços AWS Utilizados

AWS IAM

Responsável pelo gerenciamento de identidades e permissões.

Implementações

- Grupos de usuários
- Políticas baseadas em função
- MFA obrigatório
- Princípio do menor privilégio

Benefícios

✅ Redução de riscos internos

✅ Controle granular de acesso

✅ Maior governança

---

AWS Security Hub

Centralização de descobertas de segurança.

Implementações

- Consolidação de alertas
- Monitoramento contínuo
- Avaliação de conformidade

Benefícios

✅ Visão única do ambiente

✅ Resposta rápida a incidentes

✅ Melhoria da postura de segurança

---

AWS CloudTrail

Auditoria e rastreabilidade.

Implementações

- Registro de eventos
- Armazenamento seguro de logs
- Integração com monitoramento

Benefícios

✅ Investigação facilitada

✅ Evidências para auditoria

✅ Conformidade regulatória

---

🏗️ Arquitetura da Solução

                   +--------------------+
                   |     Usuários       |
                   +---------+----------+
                             |
                             v
                   +--------------------+
                   |      AWS IAM       |
                   +---------+----------+
                             |
                             v
                   +--------------------+
                   | Aplicações AWS     |
                   +---------+----------+
                             |
          +------------------+------------------+
          |                                     |
          v                                     v
+--------------------+              +--------------------+
| AWS Security Hub   |              | AWS CloudTrail     |
+--------------------+              +--------------------+
          |                                     |
          +------------------+------------------+
                             |
                             v
                   +--------------------+
                   | Monitoramento      |
                   | Auditoria          |
                   +--------------------+

---

📂 Estrutura do Repositório

a-Importancia-da-seguranca-AWS/
│
├── README.md
│
├── docs/
│   ├── business-value.md
│   ├── architecture.md
│   ├── implementation-report.md
│   ├── security-analysis.md
│   └── shared-responsibility-model.md
│
├── diagrams/
│   ├── architecture.png
│   └── security-workflow.png
│
├── assets/
│   ├── capa-projeto.png
│   ├── aws-security-banner.png
│   └── screenshots/
│
└── LICENSE

---

🔒 Princípios de Segurança Aplicados

O projeto foi desenvolvido considerando os pilares fundamentais da Segurança da Informação.

Confidencialidade

Garantir acesso apenas a usuários autorizados.

Integridade

Proteger dados contra alterações indevidas.

Disponibilidade

Garantir acesso contínuo aos sistemas.

Não Repúdio

Registrar e rastrear todas as ações realizadas.

---

☁️ Modelo de Responsabilidade Compartilhada

Uma das competências fundamentais para profissionais AWS é compreender o modelo de responsabilidade compartilhada.

AWS é responsável por

- Data Centers
- Hardware
- Rede Física
- Virtualização
- Infraestrutura Global

Cliente é responsável por

- Usuários
- Permissões
- Dados
- Configuração dos serviços
- Criptografia
- Governança

Este projeto concentra-se exatamente na camada de responsabilidade do cliente.

---

📊 Benefícios Esperados

Operacionais

- Redução de erros humanos
- Monitoramento contínuo
- Melhor governança

Financeiros

- Redução de custos com incidentes
- Menor risco de multas
- Melhor utilização da equipe de TI

Estratégicos

- Proteção da reputação
- Aumento da confiança dos clientes
- Escalabilidade segura

---

📈 Indicadores de Sucesso

Indicador| Meta
MFA habilitado| 100%
Usuários com privilégios excessivos| 0
Eventos auditados| 100%
Cobertura de monitoramento| 100%
Tempo de resposta a incidentes| < 30 min

---

🎓 Competências Demonstradas

Este projeto evidencia conhecimentos em:

- Cloud Computing
- AWS Security
- AWS IAM
- AWS CloudTrail
- AWS Security Hub
- Governança Cloud
- Compliance
- LGPD
- Gestão de Riscos
- Arquitetura de Segurança

---

🚀 Possíveis Evoluções

Em ambientes corporativos reais a solução poderia ser expandida utilizando:

- AWS GuardDuty
- AWS Inspector
- AWS Config
- AWS WAF
- AWS Shield
- AWS Control Tower
- AWS Organizations
- Amazon Macie



---


# Case Corporativo: Arquitetura de Segurança AWS — Farmácia Vida+

**Foco em Governança, Compliance (LGPD) e Mitigação de Riscos de Negócio**


## 1. Introdução & Escopo
Este documento estabelece o plano estratégico de Segurança da Informação e Arquitetura em Nuvem para a **Farmácia Vida+**, uma rede varejista com operações híbridas (e-commerce e lojas físicas). O escopo deste projeto compreende a proteção do pipeline de dados que trafega receitas médicas, dados cadastrais de clientes (PII) e transações financeiras na AWS, em total conformidade com a LGPD (Lei Geral de Proteção de Dados) e os pilares do *AWS Well-Architected Framework*.
## 2. O Problema de Negócio (Análise de Risco)
A falta de controles centralizados e a ausência de trilhas de auditoria expõem a Farmácia Vida+ a três grandes ameaças comerciais:
 * **Vazamento de Dados de Saúde (Dados Sensíveis):** O vazamento de receitas e históricos médicos pode resultar em sanções administrativas e multas da ANPD (Autoridade Nacional de Proteção de Dados) de até 2% do faturamento por infração.
 * **Ataques de Engenharia Social e Sequestro de Credenciais:** Sem uma política estrita de identidades, credenciais administrativas compartilhadas comprometem a integridade operacional da infraestrutura.
 * **Indisponibilidade do Sistema de Vendas:** A falta de detecção proativa de anomalias na nuvem pode paralisar a integração com os caixas das lojas físicas, gerando prejuízos financeiros por minuto de inoperabilidade.
## 3. O Baseline (O Cenário Atual)
 * **Identidade:** Uso de usuários IAM sem MFA ativado e políticas com permissões excessivas (AdministratorAccess em contas de desenvolvedores).
 * **Visibilidade:** Inexistência de logs centralizados. A equipe de TI não consegue rastrear quem modificou um recurso ou quando houve um acesso anômalo.
 * **Postura:** Segurança baseada em perímetros estáticos (apenas Security Groups), sem análise de comportamento de rede ou detecção de ameaças baseada em Inteligência Artificial.
## 4. Estratégia da Solução: Implementação e Justificativa Técnica
Abaixo estão detalhadas as três medidas de engenharia de segurança implementadas para mitigar os riscos de negócio listados.
### Medida 1: Controle de Acesso Centrado em Identidade (AWS IAM)
 * **Abordagem Técnica:** Implementação do **Princípio do Menor Privilégio** e separação de funções (*Segregation of Duties*).
 * **Mecanismo:**
   * Fim das contas compartilhadas. Cada funcionário técnico possui uma identidade única federada.
   * Configuração obrigatória de **MFA (Multi-Factor Authentication)** para todos os usuários através de políticas de controle de serviço (SCPs) no AWS Organizations.
   * Criação de *IAM Roles* específicas: Atendentes de loja têm acesso restrito de escrita ao banco de dados via API; analistas de BI possuem acesso exclusivo de leitura de dados anonimizados; a exclusão de arquivos de auditoria é explicitamente negada a todos os usuários.
### Medida 2: Detecção Inteligente de Ameaças (AWS GuardDuty)
 * **Abordagem Técnica:** Monitoramento contínuo da postura de segurança e comportamento do ambiente em tempo real utilizando Machine Learning nativo da nuvem.
 * **Mecanismo:**
   * Ativação do **AWS GuardDuty** em nível organizacional para analisar logs do AWS CloudTrail, VPC Flow Logs e DNS Logs.
   * Detecção automatizada de comportamentos anômalos, como tentativas de força bruta em instâncias, acessos à API da AWS vindos de IPs maliciosos conhecidos (redes TOR/Botnets) ou exfiltração de dados incomum no Amazon S3.
   * Integração com alertas críticos para resposta imediata a incidentes.
### Medida 3: Auditoria Imutável e Rastreabilidade (AWS CloudTrail)
 * **Abordagem Técnica:** Garantia do princípio do **Não Repúdio** e conformidade com auditorias de segurança (ISO 27001 / LGPD).
 * **Mecanismo:**
   * Criação de um *Trail* organizacional que registra todas as chamadas de API feitas na conta (quem solicitou, de qual IP, qual recurso foi afetado e qual foi a resposta).
   * Armazenamento dos logs em um Bucket Amazon S3 isolado na conta de segurança, com criptografia de ponta a ponta via AWS KMS (Key Management Service).
   * Ativação do **S3 Log File Integrity Validation** e **S3 Object Lock** em modo *Compliance*, impedindo que invasores ou administradores mal-intencionados apaguem ou alterem os registros de log para esconder suas ações.
## 5. Mapeamento da Tríade de Segurança da Informação (CIA + N)
Para provar o valor estratégico do projeto, a infraestrutura foi mapeada diretamente com os pilares fundamentais de segurança:
| Pilar de Segurança | Risco de Negócio Associado | Serviço AWS Adotado | Mecanismo de Proteção |
|---|---|---|---|
| **Confidencialidade** | Vazamento de receitas médicas e dados de clientes. | **AWS IAM & AWS KMS** | Controle restrito de acessos e criptografia de chaves para que apenas usuários autorizados decifrem os dados. |
| **Integridade** | Alteração fraudulenta de logs operacionais ou dados fiscais. | **AWS CloudTrail (File Validation)** | Assinaturas criptográficas garantem que os arquivos de log não sofreram adulteração desde sua gravação. |
| **Disponibilidade** | Queda do sistema de vendas por ataques direcionados. | **AWS GuardDuty** | Identificação prévia de varreduras de portas ou instâncias comprometidas, permitindo isolamento rápido antes do downtime. |
| **Não Repúdio** | Um usuário negar ter realizado uma ação crítica no sistema. | **AWS CloudTrail** | Trilha histórica imutável que vincula de forma inequívoca a identidade digital à ação executada na nuvem. |
## 6. Modelo de Responsabilidade Compartilhada na Prática
O sucesso deste projeto FAANG baseia-se no entendimento claro das fronteiras de segurança:
 * **Segurança DA Nuvem (Responsabilidade da AWS):** A AWS assegura a proteção física dos data centers, do hardware e do software de virtualização que rodam o IAM, o CloudTrail e o GuardDuty.
 * **Segurança NA Nuvem (Responsabilidade da Farmácia Vida+):** Cabe a nós configurar adequadamente as políticas do IAM, ativar o MFA, definir as chaves de criptografia do KMS, habilitar o Object Lock no S3 e agir prontamente sobre os alertas gerados pelo GuardDuty.
## 7. Resultados Esperados & Retorno sobre o Investimento (ROI)
 1. **Risco de Multas Zerado no Escopo:** Mitigação proativa de vazamentos na camada de infraestrutura, blindando a marca contra sanções econômicas da LGPD.
 2. **Tempo de Resposta a Incidentes (MTTR):** Redução do tempo de identificação de uma invasão de horas para minutos através dos alertas automatizados do GuardDuty.
 3. **Auditoria Automatizada:** Redução de custos operacionais com equipes de auditoria, uma vez que toda a infraestrutura gera evidências automatizadas e imutáveis em conformidade com as regulamentações vigentes.
## 8. Próximos Passos (Evolução da Postura)
 * **AWS Security Hub:** Consolidar os achados do GuardDuty em um painel unificado com o Score de segurança da organização.
 * **Amazon Macie:** Automatizar a descoberta e classificação de dados PII (CPFs, Nomes, Cartões) dentro dos Buckets S3 para garantir que nenhum dado sensível foi armazenado fora do local correto.
 * **AWS Config:** Monitorar continuamente as configurações dos recursos para garantir que nenhum desenvolvedor altere acidentalmente um Bucket S3 para o modo "público".

---
**Autor:** Sérgio Santos — Cientista de Dados | Ambientes Críticos e Governança de Dados

[![Portfólio Sérgio Santos](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn Sérgio Santos](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)


---




