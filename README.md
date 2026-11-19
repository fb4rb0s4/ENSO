# 🌊 Raio-X dos eventos ENSO — El Niño e La Niña

Painel interativo em **Power BI**, aplicativo web **[Pulso do Pacífico](https://alertaenso.netlify.app)** e análise de séries temporais em **Python** sobre o **El Niño–Oscilação Sul (ENSO)**, com 73 anos de dados mensais (jan/1950 a jun/2023) e foco nos impactos no Brasil.

> Projeto acadêmico da disciplina **Análise de Dados e Big Data · UC HUB**.

---

## 📌 Sobre o projeto

O ENSO é um dos principais modos de variação do clima do planeta. Ele alterna entre três fases, definidas pela temperatura das águas do Pacífico Equatorial (índice **ONI**):

| Fase | Critério (ONI) | O que significa |
|---|---|---|
| 🔴 **El Niño** | acima de **+0,5 °C** | Aquecimento anormal das águas do Pacífico central e leste |
| ⚪ **Neutro** | entre **−0,5** e **+0,5 °C** | Temperatura dentro do esperado para a época |
| 🔵 **La Niña** | abaixo de **−0,5 °C** | Resfriamento anormal dessas mesmas águas |

**Por que importa no Brasil?**

- **El Niño:** seca no Norte e Nordeste (Amazônia e Semiárido, com mais risco de queimadas) e chuvas acima da média no Sul, com risco de enchentes.
- **La Niña:** padrão inverso, com mais chuva no Norte e Nordeste e menos chuva no Sul.
- **Setores afetados:** agricultura, energia hidrelétrica, abastecimento de água e defesa civil.

O objetivo é tornar o tema **fácil de entender para qualquer pessoa**, mesmo sem conhecimento técnico em climatologia, servindo a estudantes e professores, analistas e pesquisadores e órgãos públicos.

---

## 📂 Estrutura do repositório

| Arquivo | Descrição |
|---|---|
| `ENSO_Dashboard.pbix` | Dashboard do Power BI (3 páginas) |
| `ENSO_PowerBI.xlsx` | Base modelada para o Power BI: cada aba é uma tabela do modelo, com abas de **LEIA-ME** e **sugestões de gráficos** |
| `ENSO_PowerBI_mensal.csv` | Tabela fato mensal (882 meses, 43 colunas) em CSV, separador `;` e decimal `,` |
| `el-ni-o-la-ni-a-brazil-sarima-arima.ipynb` | Notebook Python com análise exploratória e previsão com ARIMA/SARIMA |
| `Raio-X dos eventos ENSO.pptx` / `.pdf` | Apresentação final do projeto |
| `https://www.youtube.com/watch?v=OdFvkMeM1no` | Pitch |

---

## 📊 Base de dados

- **882 registros mensais**, de janeiro de 1950 a junho de 2023
- **43 episódios** identificados: **23 El Niños** e **20 La Niñas**
- **Fonte:** `ENSO.csv` (Kaggle), com índices publicados principalmente pela **NOAA**, e validação com **SOI** e **MEI.v2**
- **Variáveis:** ONI, SOI, MEI.v2, OLR, TNI, PNA, TSM e anomalias das regiões Niño 1+2, 3, 3.4 e 4, e anomalia de temperatura global

**Regra da NOAA para episódios:** o ONI precisa ficar acima de +0,5 ou abaixo de −0,5 por **pelo menos 5 meses seguidos**. Para cada episódio foram calculados início, fim, duração, pico e intensidade.

---

## 🧩 Modelagem dos dados

Fluxo: **CSV → classificação mensal → tabelas agregadas → medidas DAX**.

Modelo em **estrela**, com uma tabela fato ligada a dimensões e a tabelas de eventos e impactos:

| Grupo | Tabelas | Conteúdo |
|---|---|---|
| **Fato** | `fato_enso_mensal` | 1 linha por mês, com ONI, fase, intensidade e demais índices |
| **Dimensões** | `dim_ano_enso`, `dim_fase`, `dim_regioes`, `dim_estados_br` | Ano (fase, ONI médio/mín./máx., meses por fase), fases e cores, regiões e estados |
| **Eventos** | `eventos_enso`, `eventos_por_decada`, `resumo_frequencia` | 1 linha por episódio (duração, pico, mês do pico, estação de início, intervalo desde o anterior) |
| **Impactos** | `impactos_regionais`, `exposicao_historica`, `mapa_global` | Região × fase: nível de impacto, efeito típico, riscos e índice de exposição |

---

## 📈 Dashboard (Power BI)

**Página 1 — Visão geral:** cartões de indicadores, ONI mês a mês com os limites de ±0,5 °C, fases e intensidades por ano, ENSO × temperatura global, e filtros de ano, fase e intensidade.

**Página 2 — Eventos e frequência:** eventos por década, duração × pico do ONI, intervalo entre eventos, eventos fortes e multianuais, mês do pico, estação de início e linha do tempo anual.

**Página 3 — Impactos e regiões:** mapa de impacto (Brasil e mundo), ranking de regiões por índice de exposição (1950–2023), impacto por região e fase, e filtros de fase e escopo.

---

## 📱 Aplicativo — Pulso do Pacífico

🔗 **Acesse:** [alertaenso.netlify.app](https://alertaenso.netlify.app)

O **Pulso do Pacífico** é o protótipo de aplicativo do projeto. Ele leva os dados e análises do dashboard para uma interface web simples, voltada a qualquer pessoa, e soma funções de **alerta**, **colaboração** e **apoio às comunidades afetadas**.

**Fluxo de uso:** `1 Acessar` → `2 Menu` → `3 Funcionalidade` → `4 Informações`

| Funcionalidade | O que faz |
|---|---|
| 🔎 **Pesquisar um evento** | Busca qualquer El Niño ou La Niña desde 1950 |
| 📈 **Consultar histórico** | Índice ONI mês a mês, anos por fase e intensidade, ENSO × temperatura global, eventos por década, duração × pico, intervalo entre eventos, mês do pico e estação de início, com filtros de período, fase e intensidade |
| 🗺️ **Regiões afetadas** | Mapa do Brasil e do mundo por nível de impacto (baixo, médio e alto), ranking por índice de exposição (1950–2023) e impacto típico por região e fase |
| ⚠️ **Alertas e previsões** | Situação atual do Pacífico (El Niño 2026–2027), chance de o evento ser histórico, regiões em alerta e cadastro para receber alertas por e-mail ou no app |
| 🤝 **Colaborar** | Envio de pesquisa acadêmica, relato de desastre, proposta de solução ou projeto de ONG, com região e fase relacionadas |
| 🌐 **Comunidade** | Iniciativas em andamento de governos, ONGs, centros de pesquisa e agências internacionais, além das contribuições publicadas pelos participantes |
| 📰 **Notícias** | O que o El Niño 2026–2027 já está causando pelo mundo, filtrado por região |
| 💙 **Doar** | Campanha de apoio a comunidades atingidas por secas e enchentes, com escolha de destino e valor |

**Fontes dos alertas:** NOAA/CPC, Painel El Niño 2026–2027 (Inmet, Inpe, ANA, Cemaden, SGB, Sedec e Censipam), OMM e Bureau of Meteorology da Austrália.

**Tecnologia:** aplicação web hospedada no **Netlify** e conectada a um banco de dados. Contas, contribuições e doações são compartilhadas entre todos os usuários.

> ℹ️ **Protótipo:** a tela de doação é apenas demonstrativa. Nenhum pagamento é processado e nenhum dado bancário é pedido. Na versão real, o pagamento seria feito pela plataforma de uma ONG parceira.

---

## 🔍 Principais resultados

- 🗓️ **10 de 23** El Niños atingem o pico em **novembro**
- 🔥 **Maior evento:** El Niño **2014–16** (ONI de **+2,6 °C**), seguido por 1997–98 e 1982–83
- ⏳ **Duração média:** La Niña com **12,6 meses** contra **10,2** do El Niño; a La Niña mais longa (1998–2001) durou **32 meses**
- 🌱 **31 de 43** eventos começam no **inverno ou na primavera**, o que ajuda a antecipar cada fase

**Antes e depois de 1990:**

| Indicador | 1950–1989 | 1990–2023 |
|---|:---:|:---:|
| Episódios de El Niño | 14 | 9 |
| Episódios de La Niña | 9 | 11 |
| **Total** | **23** | **20** |

Nas últimas décadas houve menos El Niños e mais La Niñas. No mesmo período, a anomalia de temperatura global sobe de perto de 0 °C para cerca de 1 °C, enquanto o ONI segue oscilando em torno de zero.

---

## 🤖 Previsão com séries temporais (notebook)

O notebook analisa a série de **anomalias de TSM na região Niño 3.4** e compara modelos ARIMA e SARIMA ajustados com `auto_arima`:

1. Análise exploratória (médias móveis de 12 meses, sazonalidade, desvio padrão mensal, correlação entre índices)
2. Teste de estacionariedade **ADF**: p-valor ≈ 1,2e-6, ou seja, a série é estacionária
3. Ajuste dos modelos: **ARIMA(2,0,1)** e **SARIMA(2,0,1)(0,0,2)[12]**
4. Avaliação nos últimos 24 meses do conjunto de teste:

| Modelo | MSE | RMSE | MAE |
|---|:---:|:---:|:---:|
| **ARIMA** | **1,104** | **1,051** | **0,954** |
| SARIMA | 1,326 | 1,152 | 1,058 |

Neste teste, o ARIMA teve desempenho um pouco melhor que o SARIMA.

**Bibliotecas:** pandas, numpy, matplotlib, seaborn, plotly, scikit-learn, statsmodels e pmdarima.

---

## ▶️ Como usar

**Aplicativo**
- Acesse [alertaenso.netlify.app](https://alertaenso.netlify.app) no navegador do computador ou do celular.

**Dashboard**
1. Instale o [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (gratuito, Windows).
2. Abra o arquivo `ENSO_Dashboard.pbix`.
3. Use os filtros de ano, fase, intensidade e região para explorar os dados.

**Notebook**
```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn statsmodels pmdarima watermark
jupyter notebook el-ni-o-la-ni-a-brazil-sarima-arima.ipynb
```
> O notebook foi criado no Kaggle e lê o arquivo em `/kaggle/input/enso-data/ENSO.csv`. Para rodar localmente, baixe o dataset ENSO do Kaggle e ajuste o caminho no `pd.read_csv`.

---

## ⚠️ Aviso

Este projeto tem **finalidade acadêmica e analítica**. Ele complementa soluções oficiais como o NOAA PSL, o NOAA CPC e o IRI/Columbia, mas **não substitui previsões ou alertas oficiais**.

---

## 👥 Integrantes

- Eduardo Garcia
- Felipe Barbosa
- Fernanda do Nascimento Bastos
- João Lucas Menezes Lima
- Samuel Gomes

**Orientadores:** Prof. Henrique Ruiz Poyatos Neto · Profa. Iara Maria Gonçalves Salvador Novaes
