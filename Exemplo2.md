# Traçando o Brasil
## Mapas temáticos com GeoPandas — IDH e Cobertura Vegetal por Estado
**Atividade didática — Ensino de Geografia com Python**

> Dados: PNUD Brasil (2021) · MapBiomas Coleção 8 (2022) · Malha: IBGE (2022)  
> Bibliotecas: geopandas, pandas, matplotlib

---

## Como rodar no Google Colab

1. Acesse [colab.research.google.com](https://colab.research.google.com) com sua conta Google
2. Clique em **Arquivo → Novo notebook**
3. Cole o código célula por célula (cada bloco `# ── CÉLULA` é uma célula separada)
4. Execute com **Shift+Enter** em cada célula, ou vá em **Ambiente de execução → Executar tudo**

> **Nenhuma instalação é necessária.** O Google Colab já vem com geopandas, pandas e matplotlib pré-instalados. Caso apareça erro de importação, rode `!pip install geopandas --quiet` na primeira célula.

> ⚠️ **Atenção:** a Célula 2 faz o download do shapefile diretamente do servidor do IBGE (~30 MB). Aguarde a conclusão antes de executar as células seguintes — o progresso aparece na barra de execução.

---

## Estrutura do código — 7 células

### Célula 1 · Importação das bibliotecas

Carrega o **geopandas** (leitura e manipulação de dados geoespaciais), o **pandas** (tabelas), o **matplotlib** (gráficos) e utilitários de escala de cores.

**Saída esperada:**
```
✅ Bibliotecas carregadas com sucesso!
   GeoPandas versão: 1.x.x
```

---

### Célula 2 · Download do shapefile dos estados brasileiros (IBGE)

Baixa e carrega diretamente o shapefile oficial dos estados brasileiros do repositório **IBGE Malhas Territoriais 2022**, sem necessidade de download manual ou descompactação — o geopandas faz tudo a partir da URL.

**URL utilizada:**
```
https://geoftp.ibge.gov.br/organizacao_do_territorio/
malhas_territoriais/malhas_municipais/municipio_2022/
Brasil/BR/BR_UF_2022.zip
```

**Saída esperada:**
```
⏳ Baixando shapefile dos estados brasileiros do IBGE...
✅ Shapefile carregado! Total de unidades: 27
   Colunas disponíveis: ['SIGLA_UF', 'NM_UF', 'NM_REGIAO', 'geometry', ...]
```

---

### Célula 3 · Dados temáticos: IDH e Cobertura Vegetal por estado

Cria um DataFrame com dois indicadores para todos os 27 estados, integrado ao shapefile via `merge()` — equivalente a um PROCV do Excel, unindo as tabelas pela sigla da UF.

| Indicador | Fonte | Ano |
|-----------|-------|-----|
| IDH estadual | PNUD Brasil — Atlas do Desenvolvimento Humano | 2021 |
| Cobertura vegetal nativa (%) | MapBiomas — Coleção 8 | 2022 |

**Saída esperada:**
```
✅ Dados temáticos integrados ao shapefile!
  SIGLA_UF    IDH  Cobertura_Vegetal_pct       Regiao
       DF  0.824                    2.1  Centro-Oeste
       SP  0.826                   13.2      Sudeste
       SC  0.792                   28.1          Sul
       ...
```

---

### Célula 4 · Mapa 1 — IDH por estado (paleta sequencial RdYlGn)

Gera um **mapa coroplético** onde cada estado é colorido pelo seu valor de IDH. A paleta vai do vermelho (IDH mais baixo) ao verde (IDH mais alto), passando pelo amarelo.

Cada estado recebe a sigla como rótulo, posicionada automaticamente no centroide do polígono.

| Cor | Significado |
|-----|-------------|
| 🔴 Vermelho | IDH mais baixo |
| 🟡 Amarelo | IDH intermediário |
| 🟢 Verde | IDH mais alto |

Arquivo salvo: `mapa1_idh_estados.png`

---

### Célula 5 · Mapa 2 — Cobertura vegetal nativa (paleta Greens)

Mapa coroplético representando o percentual de vegetação nativa remanescente em cada estado. Verde mais intenso indica maior preservação; tons claros indicam menor cobertura.

Os rótulos mostram a sigla do estado e o percentual de cobertura.

| Cor | Significado |
|-----|-------------|
| 🟩 Verde escuro | Alta cobertura vegetal |
| 🟨 Verde claro | Cobertura intermediária |
| ⬜ Branco/bege | Baixa cobertura vegetal |

Arquivo salvo: `mapa2_cobertura_vegetal.png`

---

### Célula 6 · Mapa 3 — Comparação lado a lado: IDH × Cobertura Vegetal

Apresenta os dois mapas lado a lado em uma única figura, facilitando a comparação visual e a identificação de padrões e contradições entre os dois indicadores.

Arquivo salvo: `mapa3_comparacao_idh_vegetal.png`

---

### Célula 7 · Análise estatística + perguntas para debate

Agrupa os dados por região geográfica com `groupby()`, calcula médias e identifica destaques nacionais. Calcula também a **correlação** entre IDH e cobertura vegetal, gerando uma interpretação automática do resultado.

**Saída esperada:**
```
══════════════════════════════════════════════════════════════════
  ANÁLISE POR REGIÃO GEOGRÁFICA
══════════════════════════════════════════════════════════════════
              IDH Médio  Cobertura Vegetal Média (%)
Regiao
Sul               0.792                        25.4
Sudeste           0.783                        25.7
Centro-Oeste      0.777                        35.5
Norte             0.726                        83.8
Nordeste          0.710                        38.3

══════════════════════════════════════════════════════════════════
  DESTAQUES NACIONAIS
══════════════════════════════════════════════════════════════════
🏆 Maior IDH:            São Paulo (SP) — 0.826
📉 Menor IDH:            Maranhão (MA) — 0.676
🌿 Maior cobertura veg.: Amazonas (AM) — 97.6%
🏭 Menor cobertura veg.: Distrito Federal (DF) — 2.1%

📐 Correlação IDH × Cobertura Vegetal: -0.xxx
   → Correlação negativa: estados com maior IDH tendem a ter
     menos vegetação nativa, refletindo maior urbanização e
     desmatamento histórico nas regiões mais desenvolvidas.
```

**Perguntas para debate em sala:**

1. O mapa do IDH confirma a ideia de que o Brasil tem grandes desigualdades regionais? Que fatores históricos explicam isso?
2. Os estados com maior cobertura vegetal são os mais ou menos desenvolvidos economicamente? O que isso revela sobre o modelo de desenvolvimento adotado no Brasil?
3. O Distrito Federal tem o maior IDH do país. Que particularidades desse território explicam esse dado?
4. A Amazônia concentra alta cobertura vegetal e baixo IDH. Como conciliar preservação ambiental e desenvolvimento humano?
5. Um mapa temático é sempre neutro? Quem escolhe os dados e as paletas de cores influencia a leitura do mapa?

---

## Conceitos geográficos trabalhados na atividade

**Mapa coroplético** — tipo de mapa temático que usa variações de cor para representar valores numéricos em áreas geográficas. A escolha da paleta e dos intervalos de classe afeta diretamente a leitura do mapa — o que torna essa discussão parte essencial da atividade.

**Shapefile** — formato padrão para armazenamento de dados geoespaciais vetoriais (pontos, linhas e polígonos). Cada estado brasileiro é representado como um polígono com atributos associados (nome, sigla, área etc.).

**Centroide** — ponto geométrico central de um polígono, usado aqui para posicionar os rótulos de cada estado sobre o mapa.

**Correlação** — medida estatística que indica se duas variáveis tendem a variar juntas. Uma correlação negativa entre IDH e cobertura vegetal significa que estados mais desenvolvidos tendem a ter menos vegetação — padrão que merece interpretação crítica em sala.

---

## Atalhos úteis no Colab

| Atalho | Ação |
|--------|------|
| `Shift + Enter` | Executa a célula atual e avança para a próxima |
| `Ctrl + Enter` | Executa a célula atual sem avançar |
| `Ctrl + F9` | Executa todas as células do notebook |
| `Ctrl + M + B` | Insere nova célula abaixo da atual |

---

## Dicas pedagógicas

**Ciclo de investigação geográfica:** estruture a aula em quatro momentos — (1) observe os mapas antes de ler os valores; (2) formule perguntas sobre os padrões percebidos; (3) processe os dados e leia os resultados; (4) interprete e debata os resultados em grupo.

**Antes de rodar o código:** mostre o mapa do Brasil em branco (sem dados) e peça aos alunos que escrevam em quais estados imaginam encontrar maior IDH e maior cobertura vegetal. Compare com os resultados reais após a execução.

**Para personalizar:** os alunos podem substituir o indicador `IDH` por qualquer outra variável quantitativa estadual disponível no IBGE, PNUD ou MapBiomas — por exemplo, mortalidade infantil, PIB per capita, área desmatada ou acesso à internet.

**Para discutir representação cartográfica:** experimente trocar a paleta de cores (`cmap`) no código e observe como a mesma informação parece diferente. Paletas como `'Blues'`, `'plasma'` ou `'coolwarm'` produzem mapas com leituras distintas — excelente exercício para discutir a não-neutralidade dos mapas.

**Para baixar os mapas:** no painel esquerdo do Colab, clique no ícone de pasta 📁, localize os arquivos `.png` gerados e clique com o botão direito → *Fazer download*.

> ⚠️ **Atenção:** o Google Colab apaga os arquivos gerados quando a sessão é encerrada. Baixe os mapas antes de fechar o navegador, ou monte seu Google Drive com o comando abaixo para salvar automaticamente:
> ```python
> from google.colab import drive
> drive.mount('/content/drive')
> ```

---

## Fontes dos dados

IBGE. *Malhas territoriais — BR_UF_2022*. Rio de Janeiro: IBGE, 2022. Disponível em: <https://geoftp.ibge.gov.br/organizacao_do_territorio/malhas_territoriais>. Acesso em: mar. 2026.

MAPBIOMAS. *Coleção 8 — Estatísticas de uso e cobertura da terra*. São Paulo: MapBiomas, 2022. Disponível em: <https://mapbiomas.org/estatisticas>. Acesso em: mar. 2026.

PNUD BRASIL. *Atlas do Desenvolvimento Humano no Brasil*. Brasília: PNUD, 2021. Disponível em: <https://atlasbrasil.org.br>. Acesso em: mar. 2026.
