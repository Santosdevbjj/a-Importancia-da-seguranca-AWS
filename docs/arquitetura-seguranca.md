## Arquitetura de Segurança AWS para a Farmácia Vida+

## Objetivo

Implementar uma arquitetura de segurança em camadas utilizando serviços nativos da AWS para proteger dados sensíveis, monitorar atividades suspeitas e garantir auditoria completa do ambiente.


Arquitetura Proposta

Usuários
                    │
                    ▼
            AWS IAM + MFA
                    │
                    ▼
          Recursos da AWS
      ┌──────────┬──────────┐
      │          │          │
      ▼          ▼          ▼
    EC2         S3         RDS
      │          │          │
      └──────────┴──────────┘
                    │
                    ▼
             AWS CloudTrail
                    │
                    ▼
              Logs Seguros
                    │
                    ▼
             AWS GuardDuty
                    │
                    ▼
           Alertas de Segurança 


           ---


           

Camada 1 – Controle de Identidade
Serviço utilizado:
AWS IAM
Objetivos:
Controle de acesso
Princípio do menor privilégio
Gestão de permissões
MFA obrigatório




Camada 2 – Auditoria
Serviço utilizado:
AWS CloudTrail
Objetivos:
Registrar ações realizadas
Criar trilha de auditoria
Facilitar investigações 





Camada 3 – Detecção de Ameaças
Serviço utilizado:
AWS GuardDuty
Objetivos:
Detectar atividades suspeitas
Monitorar comportamento anômalo
Alertar equipes de segurança 







Benefícios da Arquitetura
Confidencialidade
Garantida pelo IAM.
Integridade
Garantida pelo CloudTrail.
Disponibilidade
Garantida pelo monitoramento contínuo.
Não Repúdio
Garantido pelos logs imutáveis. 






Conclusão
A combinação de IAM, CloudTrail e GuardDuty fornece uma estratégia robusta de defesa em profundidade para ambientes corporativos hospedados na AWS. :::





