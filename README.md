# 📘 Caderno Temático NotebookLM: Fundamentos do WDOFUT & Análise Quantitativa

## 🎯 Contexto & Objetivos de Estudo
Este repositório documenta a criação de um Caderno Temático no NotebookLM focado nos fundamentos do **Dólar Futuro (WDOFUT)**, integrando análise macroeconômica, leitura de fluxo e ferramentas quantitativas. O projeto alinha teoria financeira prática com o uso estratégico de IA generativa como ferramenta de **aprendizagem ativa**, curadoria crítica e organização do conhecimento.

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
- **Resumo da IA:** Curva ascendente (`slope > 0`) indica pressão de alta nos juros, atraindo capital e pressionando o dólar. Curva descendente sugere alívio fiscal/corte de juros, enfraquecendo o Real e elevando o WDO. Relação mediada por carry trade e expectativas monetárias.
- **Fontes Citadas:** `Fonte 1 (CVM), Fonte 2 (BCB), Indicadores-Quantitativos.pdf`
- **🩹 Cicatriz/Troubleshooting:** A IA inicialmente deu respostas genéricas. Ao adicionar `"Cite slope da curva e mecanismo de carry trade"`, a resposta ganhou precisão técnica e alinhamento com a lógica implementada no `ai_engine.py` (`analyze_di_curve()`).

### 🔹 Prompt 2: VWAP vs PTAX vs Ajuste
- **Pergunta Base:** `Qual a diferença prática entre VWAP, PTAX e Preço de Ajuste?`
- **Variação Testada:** `Crie uma tabela comparando VWAP, PTAX e Preço de Ajuste: cálculo, horário de referência e uso operacional. Inclua referência.`
- **Resumo da IA:** 
  - `VWAP`: Média ponderada por volume intraday. Suporte/resistência dinâmico.
  - `PTAX`: Média de 4 cotações do BCB (10h-13h). Referência para câmbio e derivativos.
  - `Ajuste`: Preço de liquidação financeira calculado pela B3 no fechamento. Define margens e marcação a mercado.
- **Fontes Citadas:** `Fonte 2 (BCB), Fonte 3 (B3), ai_engine.txt`
- **🩹 Cicatriz:** Confusão inicial entre PTAX Futuro e Spot. Ajustei o prompt especificando `"Diferencie PTAX cálculo FRP0 vs VWAP intraday"`.

### 🔹 Prompt 3: Gestão de Risco & Sizing
- **Pergunta Base:** `Como calcular posição e stop com base em volatilidade?`
- **Variação Testada:** `Monte um checklist de 5 passos para sizing e stop técnico em WDOFUT, considerando afastamento de médias e Deltas. Cite fontes.`
- **Resumo da IA:** Checklist focou em: 1) Definir risco máximo por operação (% do capital), 2) Medir volatilidade (afastamento MM57-MM114), 3) Posicionar stop além de D1/DN1 ou VWAP, 4) Calcular lotes via `(Risco $ / Distância Stop)`, 5) Validar confluência de fluxo antes da entrada.
- **Fontes Citadas:** `Fonte 1, Fonte 5, ai_engine.txt`
- **🩹 Cicatriz:** IA sugeriu stops fixos. Forcei `"baseie em afastamento de EMAs e zonas de Deltas"` para alinhar com minha lógica de `calculate_deltas()` e `calcular_medias_wdo()`.

---

## 📘 Miniguia de Estudo (Entrega Final)

### 🔹 Resumo Estruturado
- **Macro:** PTAX (referência BCB), DI1F (slope como filtro de viés), DXY (dólar global), risco fiscal e commodities. A estrutura de juros domésticos e fluxo cross-asset direcionam a tendência primária do WDOFUT.
- **Técnico/Fluxo:** EMAs (23/57/114) definem tendência e afastamento. VWAP e PTAX funcionam como pivôs institucionais. Deltas (calculados da abertura/volatilidade) e Fibonacci dinâmico mapeiam zonas de reação. `Quant Pressure` e Order Blocks (SMC) identificam agressão e exaustão.
- **Gestão:** Sizing por volatilidade, stops técnicos posicionados além de Deltas/EMAs, viés probabilístico (altista/baixista/lateral) e checklist de confluência de pelo menos 3 fatores. Preservação de capital > retorno agressivo.

### 🔹 Glossário de Conceitos
| Termo | Definição (com fonte) |
|-------|----------------------|
| **PTAX** | Taxa de câmbio de referência do BCB, calculada a partir de 4 janelas de cotação (10h-13h). Base para FRP0 e ajuste de derivativos. *(Fonte: Estudo Especial BCB nº 42/2019)* |
| **DI1F** | Futuro de Depósito Interbancário. A inclinação da curva (`slope`) reflete expectativas de juros: `> +0,05` = pressão altista; `< -0,05` = viés baixista. *(Fonte: ai_engine.py + Livro Top Derivativos CVM/B3)* |
| **VWAP** | Volume Weighted Average Price. Preço médio ponderado por volume, usado como suporte/resistência intraday e filtro de tendência. *(Fonte: B3 Educação + servervoz.py)* |
| **Delta** | Nível institucional calculado a partir da abertura e volatilidade (`abertura * 0,002`). Marcadores de expansão e zonas de reação. *(Fonte: ai_engine.py (calculate_deltas) + Indicadores-Quantitativos.pdf)* |
| **Sizing** | Dimensionamento de posição baseado em risco por operação e volatilidade do ativo. Fórmula: `lotes = risco_max / (distancia_stop * R$10)`. *(Fonte: ai_engine.py + Objetivos de Estudo)* |
| **Order Block (SMC)** | Região onde grandes players acumularam posições, gerando suporte/resistência significativo. *(Fonte: Indicadores-Quantitativos.pdf (Quant SMC OB))* |

### 🛠️ Banco de Prompts Reutilizáveis
```text
1. [Resumo Macro] "Sintetize em 3 tópicos o impacto de [EVENTO/ATIVO] no WDOFUT. Cite PTAX, DI1F e DXY. Referencie as fontes."
2. [Checklist Técnico] "Gere um checklist de 5 itens para validar entrada LONG/SHORT em dólar, incluindo confluência de EMAs, VWAP e pressão de fluxo."
3. [Gestão de Risco] "Explique como calcular stop técnico e tamanho de posição com base em afastamento de médias (57/114) e Deltas. Inclua fórmula de sizing."
4. [Simulação de Cenário] "Se DI slope > 0.10, DXY caindo e VWAP como resistência, qual viés probabilístico e alvos dinâmicos? Fundamente com as fontes."

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 🛠️ **Notas Extras**
💡 Integração com Projeto Pessoal: CandleZita IA
Este caderno não é apenas teórico. Os conceitos validados foram implementados em um engine quantitativo real (ai_engine.py + servervoz.py), que transforma a literatura financeira em regras executáveis. O ai_engine.py operacionaliza a teoria ao calcular EMAs em tempo real, quantificar a inclinação da curva DI (analyze_di_curve), projetar níveis de Delta baseados na volatilidade da abertura (calculate_deltas) e gerar um scoring probabilístico que pondera macro, fluxo e estrutura técnica. O servervoz.py valida a aplicação prática ao monitorar continuamente a distância entre preço e níveis críticos (PTAX, VWAP), emitindo alertas automáticos e narrando relatórios operacionais que eliminam viés emocional e reforçam a disciplina de checklist. Assim, o código atua como laboratório vivo: a teoria é estudada no NotebookLM, validada estatisticamente no engine e executada com precisão nos indicadores NTSL do Profit Pro.
📌 Necessidade da plataforma PROFIT PRO da Nelogica para funcionamento completo dos indicadores proprietários e Projeto Pessoal: CandleZita IA.
📝 Material educacional. Não constitui recomendação de investimento. Trading de derivativos envolve risco de perda superior ao capital inicial.
🚀 Projeto desenvolvido como parte do Desafio de Projeto DIO | NotebookLM + AI Learning
📝 Parte prática de estudos realizados para área de TI & Trading Quantitativo.
