# 💼 Business Value Report
## Projeto: A Importância da Segurança AWS para o Setor Farmacêutico

---

# Sumário

- Visão Executiva
- Contexto do Negócio
- Problemas Identificados
- Solução Proposta
- Benefícios Estratégicos
- Benefícios Operacionais
- Benefícios Financeiros
- Benefícios Regulatórios
- Indicadores de Sucesso (KPIs)
- ROI Qualitativo
- Conclusão

---

# Visão Executiva

A transformação digital no setor farmacêutico trouxe inúmeras oportunidades para melhorar a experiência dos clientes, otimizar processos internos e aumentar a competitividade.

Por outro lado, também aumentou significativamente a superfície de ataque cibernético das organizações.

Farmácias modernas armazenam e processam diariamente informações altamente sensíveis, incluindo:

- Dados pessoais de clientes
- Informações de receitas médicas
- Histórico de compras
- Dados financeiros
- Informações de convênios
- Dados de colaboradores

A exposição dessas informações pode resultar em:

- Vazamento de dados
- Multas regulatórias
- Danos reputacionais
- Interrupção dos serviços
- Perda de clientes

Para mitigar esses riscos, foi proposta a implementação de três serviços estratégicos da AWS:

1. AWS Identity and Access Management (IAM)
2. AWS Security Hub
3. AWS CloudTrail

Essas soluções fortalecem a postura de segurança da organização e estabelecem uma base sólida para crescimento sustentável e conformidade regulatória.

---

# Contexto do Negócio

## Empresa

Farmácia VidaPlus (empresa fictícia)

## Segmento

Varejo Farmacêutico

## Porte

Médio Porte

## Modelo Operacional

- Loja física
- E-commerce
- Aplicativo Mobile
- Atendimento Omnichannel

## Ambiente Tecnológico

- Aplicações Web
- Banco de Dados na Nuvem
- Serviços AWS
- Integrações com Operadoras de Saúde
- Sistemas ERP

---

# Problemas Identificados

Durante a avaliação inicial foram identificados riscos relevantes relacionados à segurança da informação.

## Problema 1 — Controle de Acesso Insuficiente

Usuários possuíam permissões excessivas.

Riscos:

- Exclusão acidental de recursos
- Alterações indevidas
- Escalada de privilégios
- Acesso não autorizado

---

## Problema 2 — Falta de Visibilidade Centralizada

Eventos de segurança estavam dispersos entre múltiplos serviços.

Riscos:

- Detecção tardia de incidentes
- Dificuldade de auditoria
- Falhas de conformidade

---

## Problema 3 — Ausência de Rastreabilidade Completa

Não existia mecanismo centralizado para registrar todas as ações realizadas na conta AWS.

Riscos:

- Dificuldade de investigação
- Falta de evidências
- Não conformidade regulatória

---

# Solução Proposta

A solução foi estruturada utilizando três serviços nativos da AWS.

---

# 1. AWS IAM

## Objetivo

Controlar identidades e permissões.

## Implementação

### Criação de Grupos

- Administradores
- Desenvolvedores
- Operações
- Auditoria

### Aplicação do Princípio do Menor Privilégio

Cada usuário recebe apenas as permissões necessárias para executar suas atividades.

### MFA Obrigatório

Ativação de autenticação multifator para:

- Administradores
- Usuários privilegiados

### Rotação de Credenciais

Políticas para:

- Senhas fortes
- Expiração periódica
- Revogação automática

---

## Benefícios

- Redução de acessos indevidos
- Maior controle operacional
- Proteção contra comprometimento de contas

---

# 2. AWS Security Hub

## Objetivo

Centralizar monitoramento e conformidade.

## Implementação

### Consolidação de Alertas

Integração com:

- AWS Config
- GuardDuty
- Inspector
- IAM Access Analyzer

### Avaliação de Compliance

Frameworks monitorados:

- CIS AWS Foundations
- AWS Foundational Security Best Practices

### Painel Centralizado

Visualização única para:

- Vulnerabilidades
- Não conformidades
- Riscos críticos

---

## Benefícios

- Visibilidade completa do ambiente
- Resposta rápida a incidentes
- Melhor governança

---

# 3. AWS CloudTrail

## Objetivo

Garantir auditoria e rastreabilidade.

## Implementação

### Registro de Eventos

Monitoramento de:

- Logins
- Alterações de configuração
- Criação de recursos
- Exclusão de recursos

### Armazenamento Seguro

Logs armazenados em:

- Amazon S3
- Retenção de longo prazo

### Integração com CloudWatch

Geração de alertas automáticos para atividades suspeitas.

---

## Benefícios

- Investigação eficiente
- Evidências para auditoria
- Atendimento a requisitos regulatórios

---

# Benefícios Estratégicos

## Proteção da Marca

Incidentes de segurança podem comprometer a confiança dos clientes.

A implementação reduz significativamente a probabilidade de vazamentos e acessos indevidos.

---

## Vantagem Competitiva

Empresas com melhores práticas de segurança possuem maior credibilidade perante:

- Clientes
- Parceiros
- Órgãos reguladores

---

## Escalabilidade Segura

A arquitetura permite crescimento sem perda de governança.

---

# Benefícios Operacionais

## Redução de Erros Humanos

Controles automatizados reduzem falhas operacionais.

---

## Monitoramento Contínuo

A equipe de TI passa a atuar de forma proativa.

---

## Resposta Mais Rápida

Incidentes podem ser identificados em minutos ao invés de dias.

---

# Benefícios Financeiros

## Redução de Custos com Incidentes

Segundo estudos internacionais, vazamentos de dados podem gerar prejuízos milionários.

A prevenção reduz significativamente:

- Custos jurídicos
- Custos operacionais
- Custos de recuperação

---

## Melhor Uso dos Recursos de TI

Automação reduz esforço manual.

A equipe passa a focar em atividades estratégicas.

---

## Redução de Multas

A conformidade reduz riscos regulatórios.

---

# Benefícios Regulatórios

## LGPD

A solução contribui para:

- Confidencialidade
- Integridade
- Disponibilidade

dos dados pessoais tratados pela farmácia.

---

## Auditorias

Facilidade para demonstrar:

- Controles implementados
- Trilhas de auditoria
- Histórico de eventos

---

## Boas Práticas AWS

Aderência às recomendações oficiais da AWS.

---

# Indicadores de Sucesso (KPIs)

| Indicador | Meta |
|------------|--------|
| MFA habilitado | 100% |
| Usuários com privilégios excessivos | 0 |
| Cobertura de auditoria | 100% |
| Eventos registrados | 100% |
| Descobertas críticas abertas | < 5 |
| Tempo médio de resposta | < 30 min |

---

# ROI Qualitativo

Embora seja difícil mensurar financeiramente todos os benefícios da segurança da informação, os ganhos são evidentes:

✅ Redução de riscos operacionais

✅ Maior confiabilidade dos sistemas

✅ Melhoria da reputação institucional

✅ Maior confiança dos clientes

✅ Atendimento às exigências regulatórias

✅ Ambiente preparado para crescimento

---

# Alinhamento com o Modelo de Responsabilidade Compartilhada AWS

A AWS é responsável pela:

- Segurança da infraestrutura global
- Data centers
- Hardware
- Rede física
- Camada de virtualização

A Farmácia VidaPlus é responsável por:

- Gestão de usuários
- Controle de acesso
- Configuração dos serviços
- Proteção dos dados
- Monitoramento de eventos

A implementação proposta fortalece exatamente a camada de responsabilidade do cliente.

---

# Conclusão

A adoção dos serviços AWS IAM, AWS Security Hub e AWS CloudTrail representa um avanço significativo na maturidade de segurança da Farmácia VidaPlus.

A solução proposta reduz riscos operacionais, melhora a governança dos dados, fortalece a conformidade regulatória e aumenta a confiança dos clientes.

Além dos benefícios técnicos, a iniciativa cria valor estratégico para o negócio ao proteger ativos críticos, preservar a reputação da marca e preparar a organização para um crescimento seguro e sustentável na nuvem.

---

## Autor

Sérgio Santos

Formação AWS Cloud Practitioner Certification

Projeto Acadêmico – AWS Cloud Security

2026
