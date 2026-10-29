---
description: Aplicar exclusivamente durante o planejamento, redação ou revisão crítica (Red Team) de propostas comerciais executivas de engenharia de software.
trigger: model_decision
---

# PADRÕES DE PERSUASÃO EXECUTIVA E RIGOR TÉCNICO EM PROPOSTAS COMERCIAIS

1. **Inversão de Foco, Empatia e Matriz de Retorno (Pilar 1):**
   - É terminantemente proibido abrir a proposta comercial falando sobre a história da software house ou apresentando autoelogios institucionais.
   - O documento deve iniciar obrigatoriamente pelo diagnóstico executivo do cliente: **1.1 Contexto e Dores (As-Is)** quantificando gargalos operacionais, retrabalho e riscos; **1.2 Visão de Transformação (To-Be)** demonstrando automação e ganhos de escala; e **1.3 Matriz de Retorno** com tabela comparativa de KPIs/OKRs mensuráveis (Linha de Base Atual vs. Meta Almejada com o projeto).

2. **Substantivação Executiva de Entregáveis (Zero Ambiguidade):**
   - O escopo jamais deve ser descrito com verbos vagos ("desenvolver telas", "otimizar processos", "criar integrações").
   - Todo módulo proposto deve ser apresentado como um ativo tangível e auditável (substantivo), acompanhado do seu impacto operacional e critérios objetivos de entrega.

3. **Justificativa Arquitetural, Diagramas Protegidos, Resiliência e TCO (Pilar 3):**
   - Decisões tecnológicas (linguagens, bancos de dados, mensageria, nuvem) devem ser justificadas por atributos concretos de negócio (redução de custo operacional, resiliência, segurança ou velocidade de entrega).
   - O Pilar 3.1 deve conter obrigatoriamente a topologia de contêineres renderizada em bloco Mermaid `flowchart TD` com todos os nós protegidos entre aspas duplas (`["..."]`).
   - A subseção 3.2 deve formalizar a mitigação de riscos de integração (Red Flags) via Staging dedicado e mocks/simuladores na esteira de CI/CD para que instabilidades de sistemas legados do cliente não paralisem os testes nem congelem a homologação.
   - O Custo Total de Propriedade (TCO) mensal estimado de infraestrutura em nuvem (AWS/GCP/Azure) e licenças SaaS deve ser exposto com transparência, deixando claro que tais faturas são contratadas e pagas diretamente pelo Cliente junto aos provedores para assegurar soberania patrimonial sobre os ambientes.

4. **Unidade Estilística, Tom Consultivo e Tolerância Zero a Slides:**
   - É estritamente proibido gerar apresentações em tópicos superficiais de slides ou textos fragmentados ("efeito Frankenstein").
   - A proposta deve ter narrativa executiva fluida, coesa e consultiva em Markdown (.md), equilibrando persuasão C-Level (CEO/CFO), autoridade de engenharia (CTO) e previsibilidade de contratação (Quadro de Espelhamento de 13 linhas).

5. **Higienização Estrita de Output (.md) e Whitelist de Placeholders:**
   - Nenhum comentário HTML (`<!-- ... -->`) oriundo de templates ou tag bruta (`{{...}}`) pode permanecer exposto na versão final da proposta comercial.
   - São tolerados unicamente os placeholders executivos padronizados registrados no array `applied_defaults` do plano (ex.: `[R$ VALOR_TOTAL_A_PREENCHER]`, `[R$ VALOR_HORA_TECNICA_A_DEFINIR]`, `[US$ ESTIMATIVA_CLOUD_MENSAL_A_DEFINIR]`), utilizados como fallbacks intencionais para definição de pricing pela diretoria comercial.
