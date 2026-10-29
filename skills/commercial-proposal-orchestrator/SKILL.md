---
name: commercial-proposal-orchestrator
description: >-
  Orquestra o pipeline agêntico em loop Generator-Critic (Reflexion) para transformar o dossiê técnico de pré-venda
  (DOSSIE_TECNICO_PRE_PROPOSTA.md) em uma Proposta Comercial e Técnica Executiva de alto impacto (PROPOSTA_COMERCIAL_EXECUTIVA.md),
  estruturada nos 6 Pilares Executivos e pré-alinhada com os 5 Anexos Técnicos Contratuais.
---

# Commercial Proposal Orchestrator Skill (Generator-Critic Reflexion)

Esta skill expõe o comando `/commercial-proposal-orchestrator` e coordena a geração e auditoria crítica de propostas comerciais executivas de engenharia de software a partir de dossiês técnicos de pré-venda.

Diferente de esteiras fragmentadas que dividem a escrita entre múltiplos redatores e geram colagens desconexas ("efeito Frankenstein"), esta skill opera sob arquitetura **Generator-Critic (Reflexion)**: um único redator executivo compõe a narrativa completa de ponta a ponta com unidade estilística, enquanto um auditor implacável (*Red Team*) inspeciona o texto sob 4 lentes antes da consolidação definitiva.

---

## Gatilhos e Invocação
- **Comando direto via Slash Command:**
  ```text
  /commercial-proposal-orchestrator [dossier_path] [output_dir]
  ```
  *Exemplo:* `/commercial-proposal-orchestrator DOSSIE_TECNICO_PRE_PROPOSTA.md ./propostas_comerciais`
- **Invocação contextual por linguagem natural:** Sempre que o usuário solicitar criar, redigir ou estruturar uma proposta comercial, orçamento executivo ou apresentação de proposta técnica/comercial a partir de um dossiê de pré-proposta ou discovery.

---

## Diretórios, Templates e Isolamento de Artefatos Transitórios (`.scratch/`)
- **Localização do Template:** Reside encapsulado dentro da pasta desta skill:
  `skills/commercial-proposal-orchestrator/templates/PROPOSTA_COMERCIAL_EXECUTIVA.template.md`
- **Injeção de Template no Contexto:** O Orquestrador lê o conteúdo integral do template e fornece a string diretamente no contexto do subagente `executive-proposal-generator`, garantindo execução global segura sem dependência de paths relativos locais.
- **Isolamento em `.scratch/`:** Todos os artefatos intermediários do ciclo Reflexion residem exclusivamente em `{{output_dir}}/.scratch/`:
  - `{{output_dir}}/.scratch/proposal_narrative_plan.json` (Plano narrativo canônico e fallbacks aplicados)
  - `{{output_dir}}/.scratch/PROPOSTA_DRAFT_V1.md` (Minuta inicial gerada na voz única)
  - `{{output_dir}}/.scratch/redteam_critique.json` (Parecer estruturado das 4 lentes do Crítico)
- **Diretório Final Limpo:** Na raiz de `{{output_dir}}/` deve residir apenas o documento final aprovado e higienizado: `{{output_dir}}/PROPOSTA_COMERCIAL_EXECUTIVA.md`.

---

## Fluxo Obrigatório de Execução (Loop Generator-Critic / Reflexion)

```text
[DOSSIE_TECNICO_PRE_PROPOSTA.md + Parâmetros Comerciais]
│
▼ (Pre-Flight Check de Arquivo)
[Validação de Existência do Dossiê]
│
▼ (Passo 1: Ingestão, Sizing & Smart Fallbacks)
[proposal-ingestion-planner]
│
▼
[{{output_dir}}/.scratch/proposal_narrative_plan.json]
│
▼ (Passo 2: Geração em Voz Executiva Única + Context Injection)
[executive-proposal-generator]
│
▼
[{{output_dir}}/.scratch/PROPOSTA_DRAFT_V1.md]
│
▼ (Passo 3: Auditoria Red Team nas 4 Lentes)
[deal-redteam-critic]
│
▼
[{{output_dir}}/.scratch/redteam_critique.json]
│
┌──────────────┴──────────────┐
▼ (REVISION_REQUIRED)         ▼ (APPROVED)
[Passo 4: Refinamento Reflexion]  [Sanity Check Determinístico]
[executive-proposal-generator]            │
│                                         │
└──────────────┬──────────────────────────┘
▼
[{{output_dir}}/PROPOSTA_COMERCIAL_EXECUTIVA.md]
```

---

### Passo 0: Pre-Flight Check de Arquivo
1. Verifique a existência física do arquivo indicado em `dossier_path` (padrão: `./DOSSIE_TECNICO_PRE_PROPOSTA.md`) e resolva `output_dir` (padrão: `./propostas_comerciais`).
2. Se o arquivo de dossiê não existir ou estiver vazio:
   - **NÃO force a execução** de ferramentas com arquivos inexistentes.
   - Avise amigavelmente o usuário no chat:
     > *"O arquivo de dossiê técnico `{dossier_path}` não foi localizado. Para gerar a proposta comercial, você pode fornecer o caminho correto ou executar previamente o pipeline de discovery (`/discovery-to-proposal-engine`)."*
   - Conclua a interação sem quebrar a esteira.

---

### Passo 1: Ingestão, Verificação Estrutural e Plano Narrativo
1. Garanta a criação do diretório `{{output_dir}}/.scratch/`.
2. Acione o subagente `proposal-ingestion-planner` fornecendo o dossiê e eventuais parâmetros comerciais do usuário.
3. **Barreira de Qualidade Estrutural:**
   - Se o planejador retornar `STATUS: BLOCKED_MISSING_PRECONDITIONS` (ausência total de problema de negócio ou ausência de definição arquitetural básica), interrompa a esteira e aponte no chat os dados estruturais faltantes no dossiê.
   - Se faltarem apenas variáveis comerciais/financeiras, o planejador aplica os **Smart Fallbacks** da software house (registrando-os em `applied_defaults`), incluindo a heurística de TCO Cloud (ex.: US$ 250 a US$ 500/mês para stack padrão) e placeholders como `[R$ VALOR_TOTAL_A_PREENCHER]`, gravando `{{output_dir}}/.scratch/proposal_narrative_plan.json`.

---

### Passo 2: Redação da Minuta Inicial em Voz Única (`Draft V1`)
1. Leia o template `skills/commercial-proposal-orchestrator/templates/PROPOSTA_COMERCIAL_EXECUTIVA.template.md` (localizado dentro do diretório desta skill no plugin).
2. Acione o subagente `executive-proposal-generator`, injetando diretamente no seu contexto o plano JSON e o conteúdo integral do template Markdown.
3. O gerador redige a minuta completa cobrindo os **6 Pilares Executivos** e o **Quadro de Espelhamento (13 Linhas)**:
   - **Pilar 1 estruturado:** 1.1 As-Is, 1.2 To-Be e 1.3 Matriz de Retorno (tabela comparativa Linha de Base vs. Meta).
   - **Pilar 2:** Módulos substantivos tangíveis e Recorte Estratégico de Não-Escopo consultivo.
   - **Pilar 3:** Diagrama de contêineres Mermaid com textos entre aspas duplas (`["..."]`), subseção 3.2 de mitigação de riscos/mocks em CI/CD, 3.3 Segurança/LGPD e 3.4 TCO transparente.
   - **Pilar 4:** Topologia de squad, cronograma e Pacto de Agilidade (PO SLA 48h, homologação em Staging com Aceite Tácito).
   - **Pilar 5:** Modelo comercial correspondente (`Modo A: Marcos`, `Modo B: Squad Dedicada`, `Modo C: Fase 0` ou `Modo Híbrido: Fase 0 + Construção`), taxa horária técnica e divisão de Foreground/Background IP.
   - **Pilar 6:** Gestão formal de CR (vedação de WhatsApp), garantia de 60 dias (ou 15 dias na Fase 0) e 3 passos de kick-off.
   - **Quadro de Espelhamento de 13 Linhas:** Tom consultivo, executivo e de parceria bilateral.
4. O resultado é gravado em `{{output_dir}}/.scratch/PROPOSTA_DRAFT_V1.md`.

---

### Passo 3: Auditoria Red Team nas 4 Lentes (`Critic`)
1. Acione o subagente `deal-redteam-critic` fornecendo a minuta `Draft V1` e o plano narrativo JSON.
2. O crítico inspeciona rigorosamente:
   - **Lente 1 (Persuasão C-Level):** Foco empático nas dores do cliente, Matriz de Retorno quantificada (1.3) e adequação ao modelo financeiro (Modo A, B, C ou Híbrido).
   - **Lente 2 (Rigor CTO & TCO):** Diagrama Mermaid válido com nós entre aspas duplas (`["..."]`), mitigação de riscos em CI/CD com mocks/stubs na subseção 3.2, papéis LGPD e TCO de nuvem.
   - **Lente 3 (Ancoragem dos 5 Anexos Contratuais):** Presença consultiva do Não-Escopo, Foreground IP 100% pós-quitação vs. licença de Background IP, PO único SLA 48h (*Schedule Freeze* 1:1 e remobilização/Taxa de Standby após 10 dias úteis), Staging 5 dias com Aceite Tácito e Quadro de Espelhamento de 13 linhas completo.
   - **Lente 4 (Higienização e Substantivação):** Ausência de verbos vagos, eliminação de 100% de comentários HTML (`<!-- ... -->`), ausência de tags brutas (`{{...}}`) e validação de whitelist de placeholders permitidos (`applied_defaults`).
3. O crítico grava `{{output_dir}}/.scratch/redteam_critique.json`, pontuando `scores` (0 a 10) e exigindo média geral >= 8.5 e nenhuma nota < 8.0 para status `"APPROVED"`.

---

### Passo 4: Refinamento Reflexion e Sanity Check Determinístico
1. Avalie o parecer do Crítico:
   - Se `status == "REVISION_REQUIRED"` (ou se `mandatory_fixes` não for vazio):
     * Revoque o `executive-proposal-generator`, instruindo a aplicação cirúrgica de cada correção solicitada.
     * Emita a minuta atualizada.
   - Se `status == "APPROVED"` com zero apontamentos:
     * Promova diretamente a minuta auditada.
2. **Sanity Check Determinístico de Higienização:**
   - Execute varredura no texto final:
     * Se houver algum comentário HTML residual (`<!-- ... -->`), remova-o programaticamente.
     * Se houver alguma tag de template não-resolvida (`{{...}}`), alerte o erro.
     * Assegure que os únicos placeholders em colchetes pertencem à whitelist documentada em `applied_defaults`.
3. Grave o arquivo definitivo higienizado em **`{{output_dir}}/PROPOSTA_COMERCIAL_EXECUTIVA.md`**.

---

## Entrega Final ao Usuário no Chat
Ao finalizar com sucesso, apresente:
1. **Resumo Executivo da Proposta Gerada:** Projeto, cliente, modelo comercial adotado (Modo A, B, C ou Híbrido) e placar de notas das 4 lentes do Red Team Critic (`scores` e média geral).
2. **Lapidação no Loop Reflexion:** Principais apontamentos resolvidos entre a `Draft V1` e a versão definitiva.
3. **Quadro de Espelhamento e Ações Comerciais Pendentes:** Destaque a ancoragem dos 13 parâmetros e informe explicitamente os campos de `applied_defaults` (ex.: valor total da proposta, taxa horária técnica, estimativa de nuvem) que requerem preenchimento de preços pela equipe comercial antes da emissão formal ao cliente.
4. **Caminho do Arquivo Gerado:** Link ou caminho absoluto para `{{output_dir}}/PROPOSTA_COMERCIAL_EXECUTIVA.md`.
