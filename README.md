# Propostas de Atividades Didáticas em Geografia Utilizando Python
### Tecnologia, Programação e Interdisciplinaridade na Educação Básica

---

## Tecnologias utilizadas

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org)
[![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)

[![Pandas](https://img.shields.io/badge/Pandas-2.2-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-3.10-11557C?style=for-the-badge&logo=matplotlib&logoColor=white)](https://matplotlib.org)
[![GeoPandas](https://img.shields.io/badge/GeoPandas-1.1-139C5A?style=for-the-badge&logo=geopandas&logoColor=white)](https://geopandas.org)
[![Folium](https://img.shields.io/badge/Folium-0.19-77B829?style=for-the-badge&logo=leaflet&logoColor=white)](https://python-visualization.github.io/folium)

[![IBGE](https://img.shields.io/badge/Dados-IBGE_Censo_2022-003087?style=for-the-badge&logo=databricks&logoColor=white)](https://sidra.ibge.gov.br)
[![PNUD](https://img.shields.io/badge/Dados-PNUD_Brasil_2021-009EDB?style=for-the-badge&logo=unitednations&logoColor=white)](https://atlasbrasil.org.br)
[![MapBiomas](https://img.shields.io/badge/Dados-MapBiomas_2022-4CAF50?style=for-the-badge&logo=openstreetmap&logoColor=white)](https://mapbiomas.org)

---

## Sobre este projeto

Este repositório reúne três atividades didáticas desenvolvidas para o ensino de **Geografia na Educação Básica**, integrando o uso da linguagem de programação **Python** como ferramenta de análise, visualização e representação espacial de dados geográficos reais.

As atividades foram concebidas no contexto da **Licenciatura em Geografia** e articulam três eixos pedagógicos centrais:

- **Aprendizagem ativa** — os estudantes formulam hipóteses, processam dados e confrontam resultados
- **Interdisciplinaridade** — Geografia, Matemática, Estatística e Cartografia trabalham em conjunto
- **Partir do lugar** — conforme Callai (2005), o cotidiano e o espaço vivido dos alunos são o ponto de entrada para compreender o espaço geográfico mais amplo

Todo o código é executado gratuitamente no **Google Colab**, sem necessidade de instalação de softwares, e utiliza exclusivamente **dados públicos e de acesso livre**.

---


## [ Atividade 1 — Quem Somos Nós?](Exemplo1.md)

**Leitura do território a partir de dados do IBGE**

[![Pandas](https://img.shields.io/badge/Pandas-2.2-150458?style=flat-square&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-3.10-11557C?style=flat-square&logo=matplotlib&logoColor=white)](https://matplotlib.org)
[![IBGE](https://img.shields.io/badge/Fonte-IBGE_Censo_2022-003087?style=flat-square)](https://sidra.ibge.gov.br)
[![Colab](https://img.shields.io/badge/Rodar_no-Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com)

### O que é

Os estudantes utilizam o **Pandas** para importar e analisar dados do Censo Demográfico 2022, construindo gráficos com o **Matplotlib** que representam a distribuição populacional por faixa etária, renda e grau de instrução em cinco municípios brasileiros de diferentes regiões.

### Metodologia

A atividade segue o princípio da **aprendizagem ativa**: antes de executar qualquer código, os alunos anotam suas hipóteses sobre as características de cada território. Após o processamento dos dados, comparam os resultados com as percepções iniciais — momento central de reflexão geográfica.

### O que o código produz

| Saída | Tipo | Conteúdo |
|-------|------|----------|
| `grafico1_distribuicao_etaria.png` | Imagem | Barras empilhadas — composição etária por município |
| `grafico2_renda_media.png` | Imagem | Barras horizontais — renda per capita com faixas de cor |
| `grafico3_instrucao.png` | Imagem | Barras agrupadas — 5 níveis de escolaridade |
| Relatório no terminal | Texto | Destaques automáticos + 5 perguntas para debate |

### Conceitos geográficos

`Transição demográfica` · `Desigualdade regional` · `Indicadores socioeconômicos` · `Leitura de gráficos` · `Geografia Humana`

### Por que essa atividade importa

A articulação entre dados reais do IBGE e ferramentas de visualização transforma o aluno de receptor passivo em **analista do território**. A comparação entre municípios de regiões distintas revela padrões de desigualdade que seriam invisíveis em uma aula expositiva tradicional.

---

## [Atividade 2 — Traçando o Brasil](Exemplo2.md)

**Mapas temáticos com GeoPandas — IDH e Cobertura Vegetal por Estado**

[![GeoPandas](https://img.shields.io/badge/GeoPandas-1.1-139C5A?style=flat-square&logo=geopandas&logoColor=white)](https://geopandas.org)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-3.10-11557C?style=flat-square&logo=matplotlib&logoColor=white)](https://matplotlib.org)
[![PNUD](https://img.shields.io/badge/Fonte-PNUD_Brasil_2021-009EDB?style=flat-square)](https://atlasbrasil.org.br)
[![MapBiomas](https://img.shields.io/badge/Fonte-MapBiomas_2022-4CAF50?style=flat-square)](https://mapbiomas.org)
[![IBGE Malhas](https://img.shields.io/badge/Malha-IBGE_BR_UF_2022-003087?style=flat-square)](https://geoftp.ibge.gov.br)
[![Colab](https://img.shields.io/badge/Rodar_no-Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com)

### O que é

Os estudantes utilizam o **GeoPandas** para carregar o shapefile oficial dos estados brasileiros diretamente do repositório do IBGE e integrar indicadores reais — IDH (PNUD 2021) e cobertura vegetal nativa (MapBiomas 2022) — produzindo **mapas coropléticos** temáticos.

### Metodologia

A atividade segue o **ciclo de investigação geográfica** em quatro etapas:

1. **Observação** — o aluno examina o mapa do Brasil sem dados, apenas com as formas dos estados
2. **Formulação de perguntas** — onde imagina encontrar maior IDH? Maior cobertura vegetal?
3. **Coleta e processamento** — execução do código e geração dos mapas
4. **Interpretação** — debate sobre padrões, contradições e o que os mapas revelam (e ocultam)

### O que o código produz

| Saída | Tipo | Conteúdo |
|-------|------|----------|
| `mapa1_idh_estados.png` | Imagem | Coroplético IDH — paleta vermelho→amarelo→verde |
| `mapa2_cobertura_vegetal.png` | Imagem | Coroplético vegetação — paleta Greens com % em cada estado |
| `mapa3_comparacao_idh_vegetal.png` | Imagem | Dois mapas lado a lado para comparação direta |
| Relatório no terminal | Texto | Médias por região, correlação IDH × vegetação, destaques |

### Conceitos geográficos

`Mapa coroplético` · `Shapefile` · `Cartografia temática` · `IDH` · `Cobertura vegetal` · `Desigualdade regional` · `Correlação espacial`

### Por que essa atividade importa

A produção de mapas pelos próprios estudantes — e não apenas a leitura de mapas prontos — desenvolve a **literacia cartográfica** de forma ativa. Discutir a escolha da paleta de cores, dos intervalos de classe e do indicador representado revela que todo mapa é uma construção, nunca uma representação neutra da realidade.

> ⚠️ **Atenção:** a Célula 2 faz o download do shapefile (~30 MB) diretamente do servidor do IBGE. Aguarde a conclusão antes de executar as células seguintes.

---

## [Atividade 3 — Conectando Lugares](Exemplo3.md)

**Rotas, distâncias e desigualdades territoriais com Folium**

[![Folium](https://img.shields.io/badge/Folium-0.19-77B829?style=flat-square&logo=leaflet&logoColor=white)](https://python-visualization.github.io/folium)
[![Pandas](https://img.shields.io/badge/Pandas-2.2-150458?style=flat-square&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![OpenStreetMap](https://img.shields.io/badge/Mapa_Base-OpenStreetMap-7EBC6F?style=flat-square&logo=openstreetmap&logoColor=white)](https://www.openstreetmap.org)
[![CNES](https://img.shields.io/badge/Fonte-DataSUS_CNES-005C99?style=flat-square)](https://cnes.datasus.gov.br)
[![Inep](https://img.shields.io/badge/Fonte-Inep_Censo_Escolar-003087?style=flat-square)](https://inep.gov.br/censo-escolar)
[![Colab](https://img.shields.io/badge/Rodar_no-Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com)

### O que é

Os estudantes utilizam o **Folium** para criar três mapas interativos em HTML representando a distribuição de equipamentos públicos (escolas, unidades de saúde, parques) em uma cidade, as rotas entre as residências dos alunos e suas escolas, e um mapa de calor revelando desigualdades na cobertura territorial de serviços públicos.

### Metodologia

A atividade apoia-se na perspectiva do **lugar como ponto de partida** para a compreensão do espaço geográfico, conforme Callai (2005). Os alunos partem de uma questão concreta e pessoal — *"Quanto tempo levo de casa até a escola?"* — e utilizam a fórmula de **Haversine** para calcular distâncias geográficas reais, confrontando percepção subjetiva com dado objetivo.

### O que o código produz

| Saída | Tipo | Conteúdo |
|-------|------|----------|
| `mapa1_equipamentos_publicos.html` | Mapa interativo | Três camadas (escolas, saúde, parques) com popups e ferramenta de medição |
| `mapa2_rotas_alunos_escolas.html` | Mapa interativo | Rotas tracejadas coloridas de cada aluno até a escola mais próxima |
| `mapa3_heatmap_equipamentos.html` | Mapa interativo | Mapa de calor sobre fundo escuro revelando vazios de cobertura |
| Relatório no terminal | Texto | Distâncias por aluno, equipamentos por bairro, perguntas para debate |

### Conceitos geográficos

`Lugar` · `Direito à cidade` · `Equipamentos públicos` · `Desigualdade territorial` · `Heatmap` · `Cartografia digital` · `Fórmula de Haversine`

### Por que essa atividade importa

Ao trabalhar com a **própria realidade espacial**, os alunos deixam de ser observadores externos do território para se tornarem sujeitos que o investigam. O mapa de calor torna visível algo que muitas vezes é invisível no cotidiano: a desigualdade no acesso a serviços públicos entre bairros de uma mesma cidade.

> 🔒 **Privacidade:** os alunos informam apenas o nome do bairro de residência — nunca o endereço completo. O código usa o centroide do bairro, preservando a privacidade dos estudantes.

> ⚠️ **Atenção:** o Folium não vem pré-instalado no Colab. A Célula 1 faz a instalação automaticamente — execute-a primeiro e aguarde antes de prosseguir.


