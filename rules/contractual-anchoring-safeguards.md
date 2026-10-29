---
description: Aplicar exclusivamente durante o planejamento, redação ou revisão crítica (Red Team) de propostas comerciais executivas de engenharia de software para ancorar salvaguardas contratuais.
trigger: model_decision
---

# SALVAGUARDAS DE ANCORAGEM PRÉ-CONTRATUAL (PONTE PROPOSTA -> ANEXOS TÉCNICOS)

Toda proposta comercial deve introduzir, sob tom consultivo, elegante e de parceria mútua, os 5 pilares de governança que serão formalizados nos Anexos Técnicos do Contrato (consolidados no Quadro de Espelhamento de 13 linhas):

1. **Recorte Estratégico e Não-Escopo Consultivo (Ancoragem do Anexo 1 - SOW):**
   - As exclusões técnicas obrigatórias não devem soar como recusa defensiva, mas como "Recorte Estratégico de Proteção de Prazo e Orçamento".
   - Deve constar explicitamente que não integram o orçamento inicial: (a) migração, higienização ou saneamento de bancos de dados legados; (b) suporte a navegadores obsoletos fora das 3 últimas versões de Chrome, Safari e Edge; (c) pagamento de faturas de nuvem, licenças SaaS ou taxas de APIs terceiras; e (d) treinamento presencial ou suporte nível 1 a usuários finais.

2. **Enquadramento do Modelo Comercial e Propriedade Intelectual (Ancoragem do Anexo 1 - SOW):**
   - A proposta deve estruturar o investimento de acordo com o modelo recomendado no dossiê: Modo A (Escopo Fechado por Marcos M0..Mn), Modo B (Squad Dedicada / Time & Materials por Sprint), Modo C (Fase 0 / Inception Técnica Paga) ou Modo Híbrido (Fase 0 Inception Fechada + Estimativa Balizada de Construção).
   - **Foreground IP vs. Background IP:** Posicionar a cessão definitiva de 100% do código-fonte desenvolvido sob encomenda (*Foreground IP*, efetivada após a quitação integral do projeto) como vantagem patrimonial do Cliente, e a injeção de bibliotecas internas, módulos de IaC e boilerplates pré-existentes da Contratada (*Background IP*, cedidos sob licença de uso perpétua, não-exclusiva e irrevogável embutida na solução) como acelerador gratuito que reduz o prazo e o custo do orçamento.

3. **Pacto de Agilidade, Interlocutor Único, Standby e LGPD (Ancoragem do Anexo 2 - RACI):**
   - Posicionar a designação de um Product Owner (PO) único do Cliente com SLA de resposta de até 48 horas úteis como fator crítico para cumprir a data de Go-Live.
   - Explicar de forma transparente que bloqueios de insumos/acessos superiores a 48h úteis deslocam o cronograma proporcionalmente (1:1) sem ônus (*Schedule Freeze*), e que paralisações superiores a 10 dias úteis permitem a realocação da squad (com janela de 5 dias úteis para remobilização prioritária) ou a manutenção da equipe mediante Taxa de Standby proporcional (custo dos profissionais retidos).
   - Sob a ótica de *Privacy by Design* (LGPD), estabelecer o Cliente como Controlador e a Contratada como Operadora técnica, vedando o envio de dumps de produção com dados pessoais reais (PII) não anonimizados para ambientes de Desenvolvimento, QA e Staging.

4. **Rito de Homologação em Staging, Aceite Tácito e Resiliência a Legados (Ancoragem do Anexo 3):**
   - Apresentar a janela de 5 dias úteis de homologação em ambiente de Staging como rito de velocidade contínua: na ausência de apontamento de falhas impeditivas (P1/P2) instruídas com evidências técnicas (URL, payload, passos de reprodução e logs) dentro dos 5 dias úteis, a entrega é considerada aprovada automaticamente (*Aceite Tácito*), liberando o faturamento e a fase seguinte (ajustes cosméticos P3/P4 entram no ciclo subsequente sem reter a etapa).
   - Destacar o uso de testes automatizados com simuladores (*mocks/stubs*) em CI/CD como garantia de que eventuais quedas ou instabilidades em APIs/sandboxes legados do Cliente não travam a validação nem o cronograma da entrega.

5. **Proteção Orçamentária de Mudanças, Garantia vs. AMS e Quadro de Espelhamento (Ancoragem dos Anexos 4 e 5):**
   - Posicionar a proibição de alterações de escopo via canais informais (WhatsApp, Slack, conversas verbais) como mecanismo de **proteção do orçamento do Cliente contra cobranças surpresa**, exigindo que toda mudança (Change Request) seja previamente avaliada em horas, impacto no caminho crítico e custo (com taxa horária técnica já fixada na proposta) antes de qualquer codificação.
   - Apresentar a garantia técnica de 60 dias corridos pós-Go-Live (Modos A, B e Híbrido) para vícios ocultos do código autoral com SLA de pronto atendimento (P1: resposta em 2h/contorno em 8h; P2: 4h/16h; P3: 8h) — ou 15 dias de revisão documental e de artefatos no Modo C (Fase 0) —, diferenciando-a claramente de falhas em APIs terceiras e apresentando a opção de plano de Sustentação Contínua (AMS/Retainer) para evolução após a garantia.
   - Consolidar todos os 13 parâmetros no **Quadro de Espelhamento Pré-Contratual**, assegurando previsibilidade jurídica total sem atrito negocial.
