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


