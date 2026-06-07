# -miniguia-estudos-notebooklm
# 📘 Caderno Temático NotebookLM: Fundamentos do WDOFUT & Análise Quantitativa

## 🎯 Contexto & Objetivos de Estudo
Este repositório documenta a criação de um **Caderno Temático no NotebookLM** focado nos fundamentos do **Dólar Futuro (WDOFUT)**, integrando análise macroeconômica, leitura de fluxo e ferramentas quantitativas. O projeto alinha teoria financeira prática com o uso estratégico de IA generativa como ferramenta de **aprendizagem ativa**, curadoria crítica e organização do conhecimento.

**Objetivos:**
1. Compreender a estrutura do WDOFUT, formadores de preço (PTAX, VWAP, DXY) e a influência da curva de juros (DI1F).
2. Aplicar conceitos de análise técnica e fluxo (EMAs, Fibonacci, Deltas, Order Blocks) para identificação de confluência e zonas de liquidez.
3. Validar teorias através de um engine quantitativo real (`CandleZita IA`) e desenvolver prompts reutilizáveis para estudo contínuo.
4. Consolidar um miniguia com resumos, glossário e banco de prompts para revisões rápidas e tomada de decisão disciplinada.

---

## 📚 Curadoria de Fontes Abertas
Material selecionado, validado e carregado no NotebookLM:

| # | Fonte | Formato | Link | Aplicação no Estudo |
|---|-------|---------|------|---------------------|
| 1 | TOP Mercado de Derivativos (CVM/B3) | PDF | [🔗 Baixar](https://www.gov.br/investidor/pt-br/educacional/publicacoes-educacionais/livros-cvm/livro-topderivativos.pdf) | Estrutura de contratos, mecânica da B3 e fundamentos de câmbio/juros |
| 2 | A taxa de câmbio de referência Ptax (BCB) | PDF | [🔗 Baixar](https://www.bcb.gov.br/conteudo/relatorioinflacao/EstudosEspeciais/EE042_A_taxa_de_cambio_de_referencia_Ptax.pdf) | Metodologia da PTAX, cálculo FRP0 e correlação com WDOFUT |
| 3 | Curso B3: Futuro Mini de Dólar (WDO) | Web | [🔗 Acessar](https://edu.b3.com.br/w/mini-dolar) | Especificações contratuais, margens, horários e liquidação |
| 4 | Fibonacci Retracement (Investopedia) | Web | [🔗 Acessar](https://www.investopedia.com/terms/f/fibonacciretracement.asp) | Conceito técnico, níveis 23.6%/38.2%/61.8% e projeção de alvos |
| 5 | Indicadores Quantitativos "QUANT DÓLAR TRADER" | PDF | *([Arquivo próprio](https://github.com/brunofugideoliveiradev/-miniguia-estudos-notebooklm/blob/main/Indicadores-Quantitativos-QUANT-DOLAR-TRADER.pdf))* | Case prático: aplicação de pressão de fluxo, Deltas, SMC OB e VWAP dinâmica |

---

## 🔍 Engenharia de Prompts & "Cicatrizes"
Registro do processo iterativo de extração de conhecimento via NotebookLM. O mercado valoriza quem documenta o raciocínio por trás dos resultados.

### 🔹 Prompt 1: Relação Macro Juros ↔ Dólar
- **Pergunta Base:** `Como a curva de DI influencia o WDOFUT?`
- **Variação Testada:** `Explique em 3 tópicos a relação entre inclinação da curva DI1F e direção do dólar futuro. Cite as fontes usadas.`
- **Resumo da IA:** Curva ascendente (slope > 0) indica pressão de alta nos juros, atraindo capital estrangeiro e pressionando o dólar para baixo. Curva descendente sugere alívio fiscal/corte de juros, enfraquecendo o Real e elevando o WDO. A relação é mediada pelo carry trade e expectativas de política monetária.
- **Fontes Citadas:** `Fonte 1 (CVM), Fonte 2 (BCB)`
- **🩹 Cicatriz/Troubleshooting:** A IA inicialmente deu respostas genéricas. Ao adicionar `"Cite slope da curva e mecanismo de carry trade"`, a resposta ganhou precisão técnica e alinhamento com a lógica implementada no `ai_engine.py` (`analyze_di_curve()`).

### 🔹 Prompt 2: VWAP vs PTAX vs Ajuste
- **Pergunta Base:** `Qual a diferença prática entre VWAP, PTAX e Preço de Ajuste?`
- **Variação Testada:** `Crie uma tabela comparando VWAP, PTAX e Preço de Ajuste: cálculo, horário de referência e uso operacional. Inclua referência.`
- **Resumo da IA:** 
  - **VWAP:** Média ponderada por volume intraday. Suporte/resistência dinâmico.
  - **PTAX:** Média de 4 cotações do BCB (10h-13h). Referência para câmbio e derivativos.
  - **Ajuste:** Preço de liquidação financeira calculado pela B3 no fechamento. Define margens e marcação a mercado.
- **Fontes Citadas:** `Fonte 2 (BCB), Fonte 3 (B3)`
- **🩹 Cicatriz:** Confusão inicial entre PTAX Futuro e Spot. Ajustei o prompt especificando `"Diferencie PTAX cálculo FRP0 vs VWAP intraday"`.

### 🔹 Prompt 3: Gestão de Risco & Sizing
- **Pergunta Base:** `Como calcular posição e stop com base em volatilidade?`
- **Variação Testada:** `Monte um checklist de 5 passos para sizing e stop técnico em WDOFUT, considerando afastamento de médias e Deltas. Cite fontes.`
- **Resumo da IA:** Checklist focou em: 1) Definir risco máximo por operação (% do capital), 2) Medir volatilidade (afastamento MM57-MM114), 3) Posicionar stop além de D1/DN1 ou VWAP, 4) Calcular lotes via `(Risco $ / Distância Stop)`, 5) Validar confluência de fluxo antes da entrada.
- **Fontes Citadas:** `Fonte 1, Fonte 5`
- **🩹 Cicatriz:** IA sugeriu stops fixos. Forcei `"baseie em afastamento de EMAs e zonas de Deltas"` para alinhar com minha lógica de `calculate_deltas()` e `calcular_medias_wdo()`.

---

## 📘 Miniguia de Estudo (Entrega Final)

### 📌 Resumo Estruturado
- **Macro & Formadores de Preço:** O WDOFUT é lastreado no USD/BRL, com preço influenciado pela PTAX (BCB), DXY (dólar global), curva DI1F (juros domésticos) e fluxo estrangeiro. A inclinação da curva DI atua como filtro de viés macro.
- **Técnico & Fluxo:** EMAs (23, 57, 114) definem tendência e afastamento. VWAP e PTAX funcionam como pivôs institucionais. Fibonacci dinâmico e Deltas (calculados a partir da abertura/volatilidade) mapeiam zonas de reação. Order Blocks (SMC) e `Quant Pressure` identificam agressão e exaustão.
- **Gestão de Risco:** Edge sustentável vem de confluência + sizing proporcional à volatilidade + stops técnicos. Preservação de capital > retorno agressivo. Viés é probabilístico (altista/baixista/lateral), nunca certeiro.

### 📖 Glossário de Conceitos
| Termo | Definição |
|-------|-----------|
| **PTAX** | Taxa de câmbio de referência do BCB, calculada a partir de 4 médias diárias. Base para FRP0 e ajuste de derivativos. |
| **DI1F** | Futuro de Depósito Interbancário. A inclinação da curva (slope) reflete expectativas de juros e pressiona o câmbio. |
| **VWAP** | Volume Weighted Average Price. Preço médio ponderado por volume, usado como suporte/resistência intraday e filtro de tendência. |
| **Deltas** | Níveis calculados a partir da abertura e volatilidade do ativo. Marcadores de expansão de preço e zonas de reação institucional. |
| **Sizing** | Dimensionamento da posição baseado no risco financeiro máximo por operação e na distância do stop técnico. |
| **Order Block (SMC)** | Região onde grandes players acumularam posições, gerando suporte/resistência significativo para entradas futuras. |

### 🛠️ Banco de Prompts Reutilizáveis
```text
1. [Resumo Macro] "Sintetize em 3 tópicos o impacto de [EVENTO/ATIVO] no WDOFUT. Cite PTAX, DI1F e DXY. Referencie as fontes."
2. [Checklist Técnico] "Gere um checklist de 5 itens para validar entrada LONG/SHORT em dólar, incluindo confluência de EMAs, VWAP e pressão de fluxo."
3. [Gestão de Risco] "Explique como calcular stop técnico e tamanho de posição com base em afastamento de médias (57/114) e Deltas. Inclua fórmula de sizing."
4. [Simulação de Cenário] "Se DI slope > 0.10, DXY caindo e VWAP como resistência, qual viés probabilístico e alvos dinâmicos? Fundamente com as fontes."
