# RELATÓRIO EXECUTIVO DE SEGURANÇA E CONFORMIDADE AWS
**Postura de Segurança para Operações Farmacêuticas Híbridas**

**Data:** 11 de Junho de 2026  
**Empresa Fictícia:** Drogaria Alfa (Grupo Abstergo Industries)  
**Responsável Técnico:** Sergio Luiz dos Santos (Senior Systems Analyst / Cloud Security Practitioner)  
**Escopo do Ambiente:** 1 Conta AWS (Workload de Produção), Região us-east-1 (N. Virginia)  

---

## 1. Problema de Negócio e Contexto
A Drogaria Alfa migrou recentemente seu sistema de gerenciamento de vendas e prontuários eletrônicos para a AWS. Por lidar diretamente com dados sensíveis de clientes (fórmulas médicas, CPFs associados a medicamentos de controle especial e histórico de saúde), a empresa tornou-se alvo crítico para ataques de vazamento de dados. 

**O Desafio:** A operação atual corre o risco de sofrer sanções pesadas da LGPD por falta de criptografia e controle de acessos inadequado, além de potenciais prejuízos por indisponibilidade do sistema de vendas nas lojas físicas em caso de um ataque de Ransomware.

---

## 2. O Baseline (O Cenário Atual)
Atualmente, a farmácia opera sob um modelo de segurança frágil:
* **Identidade:** Funcionários utilizam credenciais compartilhadas do IAM sem MFA (Multi-Factor Authentication) ativo.
* **Armazenamento:** Os dados de receitas médicas são gravados em Buckets Amazon S3 sem criptografia forçada na camada do servidor e com políticas excessivamente abertas.
* **Auditoria:** Não há monitoramento contínuo ou centralizado de falhas na infraestrutura. A detecção de problemas é puramente reativa.

---

## 3. Estratégia da Solução: As 3 Medidas de Segurança Fundamentais

Seguindo o Modelo de Responsabilidade Compartilhada da AWS (onde a infraestrutura física é dever da AWS e a proteção dos dados internos é dever do cliente), foram selecionadas três ferramentas estratégicas:

### Medida 1: AWS Identity and Access Management (IAM) com Privilégio Mínimo e MFA
* **O que resolve:** Elimina o risco de acessos não autorizados por roubo de senhas ou engenharia social de funcionários de balcão e administradores.
* **Implementação Técnica:** * Substituição das contas compartilhadas por identidades federadas individuais.
    * Aplicação do princípio do privilégio mínimo através de políticas baseadas em funções (RBAC). Farmacêuticos possuem acesso de leitura às receitas; operadores de caixa apenas gravam vendas; privilégios de exclusão de logs são restritos e bloqueados por SCPs (Service Control Policies).
    * Imposição obrigatória de MFA (Multi-Factor Authentication) para todas as contas, principalmente para perfis administrativos e acesso root.

### Medida 2: Amazon S3 Security (Criptografia com AWS KMS + Object Lock)
* **O que resolve:** Garante a **Confidencialidade** e **Integridade** dos dados médicos armazenados, blindando a empresa contra vazamentos e alterações criminosas.
* **Implementação Técnica:**
    * Habilitação de Criptografia Baseada no Servidor forçada por políticas de bucket (SSE-KMS) utilizando chaves gerenciadas pelo cliente (CMKs). Mesmo que um arquivo seja interceptado, ele será ilegível sem a chave criptográfica correta.
    * Ativação do **AWS S3 Object Lock** configurado no modo *Compliance* com retenção de 5 anos para os relatórios fiscais e receitas. Isso impede que os dados sejam excluídos ou modificados por qualquer usuário (incluindo a conta root), servindo como proteção definitiva contra ataques de criptografia por Ransomware.
    * Bloqueio total de acesso público ao S3 em nível de conta.

### Medida 3: Auditoria Automatizada Contínua com Prowler + AWS Systems Manager (Session Manager)
* **O que resolve:** Transforma a segurança da farmácia de reativa para proativa, monitorando vulnerabilidades em tempo real de acordo com frameworks como CIS Benchmark e ISO 27001.
* **Implementação Técnica:**
    * Implementação de uma instância Amazon EC2 em uma sub-rede privada controlada. O acesso administrativo a essa instância é feito de forma segura e auditada via **AWS Systems Manager Session Manager**, eliminando a necessidade de expor portas SSH (22) para a internet.
    * Instalação da ferramenta de código aberto **Prowler** (versão 4.0+) integrada via script automatizado (`prowler_scan.sh`) para realizar varreduras paralelas semanais de conformidade no ambiente.
    * Configuração do Amazon EventBridge e Amazon SNS para enviar alertas imediatos por e-mail à equipe de TI caso a pontuação de conformidade caia ou vulnerabilidades críticas sejam detectadas.

---

## 4. Resultados de Negócio (Business Performance)
O impacto financeiro e operacional direto dessas medidas na Drogaria Alfa inclui:
1.  **Redução do Risco Regulatório:** Mitigação de multas da LGPD que poderiam alcançar até 2% do faturamento por infração devido ao vazamento de dados de saúde.
2.  **Continuidade dos Negócios:** Com o S3 Object Lock ativo, o risco de paralisação total das lojas físicas devido a ataques de Ransomware cai para próximo de zero, protegendo o faturamento diário contra indisponibilidades operacionais.
3.  **Auditoria Ágil:** O tempo necessário para preparar relatórios de conformidade para auditorias de segurança foi reduzido de semanas para minutos com a consolidação automatizada de dados gerada pelo Prowler em planilhas Excel estruturadas.

---

## 5. Próximos Passos
* Integrar os relatórios do Prowler ao **AWS Security Hub** para obter um painel visual consolidado e unificado das descobertas.
* Implementar o **Amazon Macie** para escanear de forma inteligente os arquivos legados no S3 e identificar se dados sensíveis ocultos (como números de cartões ou documentos não catalogados) estão desprotegidos.
