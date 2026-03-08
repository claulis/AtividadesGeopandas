
# Conectando Lugares
## Rotas, distâncias e desigualdades territoriais com Folium
**Atividade didática — Ensino de Geografia com Python**

> Referência pedagógica: Callai (2005) — o lugar como ponto de partida para a compreensão do espaço geográfico  
> Bibliotecas: folium, pandas, math

---

## Como rodar no Google Colab

1. Acesse [colab.research.google.com](https://colab.research.google.com) com sua conta Google
2. Clique em **Arquivo → Novo notebook**
3. Cole o código célula por célula (cada bloco `# ── CÉLULA` é uma célula separada)
4. Execute a **Célula 1 primeiro** e aguarde a instalação do Folium antes de prosseguir
5. Execute as demais com **Shift+Enter**, ou use **Ambiente de execução → Executar tudo**

> ⚠️ **Atenção:** diferente das atividades anteriores, o Folium **não vem pré-instalado** no Colab. A Célula 1 faz a instalação automaticamente — aguarde a conclusão antes de executar as demais.

> 💡 **Para visualizar os mapas no Colab** (sem precisar baixar o arquivo), cole o código abaixo em uma nova célula após cada `mapa.save(...)`:
> ```python
> from IPython.display import IFrame
> IFrame('mapa1_equipamentos_publicos.html', width=800, height=500)
> ```

---

## Estrutura do código — 7 células

### Célula 1 · Instalação e importação das bibliotecas

Instala o **folium** via pip e importa todas as bibliotecas necessárias: folium (mapas interativos), pandas (tabelas) e math (cálculo de distâncias).

**Saída esperada:**
```
✅ Bibliotecas carregadas com sucesso!
   Folium versão: 0.x.x
```

---

### Célula 2 · Dados: equipamentos públicos de uma cidade fictícia

Define as coordenadas e atributos de 5 categorias de dados para a cidade fictícia **Vila Esperança**, inspirada em municípios brasileiros de médio porte:

| Categoria | Quantidade | Atributos |
|-----------|-----------|-----------|
| 🏫 Escolas municipais | 5 | nome, bairro, vagas, Índice de Estrutura |
| 🏥 Unidades de saúde | 5 | nome, tipo (UBS/Hospital/UPA), atendimentos/dia |
| 🌳 Parques e áreas verdes | 4 | nome, área em m² |
| 🏠 Residências dos alunos | 5 | bairro (centroide, sem endereço exato) |

> **Privacidade:** os alunos informam apenas o bairro de residência — nunca o endereço completo. O código usa o centroide do bairro para preservar a privacidade dos estudantes.

**Saída esperada:**
```
✅ Dados carregados!
   5 escolas | 5 unidades de saúde | 4 parques | 5 alunos
```

**Para usar dados reais da sua cidade:** substitua as coordenadas (`lat`, `lon`) pelos valores da sua cidade. Coordenadas gratuitas em:
- [Google Maps](https://maps.google.com) → clique com botão direito → *"O que há aqui?"*
- [OpenStreetMap](https://www.openstreetmap.org) → clique com botão direito → *"Mostrar endereço"*

---

### Célula 3 · Função de distância geográfica (fórmula de Haversine)

Define e aplica a **fórmula de Haversine**, que calcula a distância real entre dois pontos na superfície da Terra a partir de suas coordenadas. É mais precisa que o cálculo euclidiano simples porque considera a curvatura terrestre.

```
distância ≈ 2R · arcsin(√(sin²(Δlat/2) + cos(lat1)·cos(lat2)·sin²(Δlon/2)))
onde R = 6.371 km (raio médio da Terra)
```

Para cada aluno, o código identifica automaticamente a escola mais próxima e calcula o tempo estimado de caminhada (velocidade média de 5 km/h).

**Saída esperada:**
```
📏 Distância de cada aluno até a escola mais próxima:
───────────────────────────────────────────────────────
  Aluno A (Centro      ) → EMEF João Paulo II      | 0.87 km | ~10 min a pé
  Aluno B (Jardim Sul  ) → EMEF Monteiro Lobato    | 1.23 km | ~15 min a pé
  Aluno C (Bela Vista  ) → EMEF Zumbi dos Palmares | 1.56 km | ~19 min a pé
  Aluno D (Parque Norte) → EMEF Santos Dumont      | 0.94 km | ~11 min a pé
  Aluno E (Vila Nova   ) → EMEF Maria Quitéria     | 1.41 km | ~17 min a pé
```

---

### Célula 4 · Mapa 1 — Equipamentos públicos com camadas interativas

Gera um mapa interativo com **três camadas independentes**, que podem ser ligadas e desligadas pelo usuário:

| Camada | Ícone | Cor |
|--------|-------|-----|
| 🏫 Escolas municipais | Capelo 🎓 | Azul |
| 🏥 Unidades de saúde | Cruz ➕ / Ambulância | Verde · Vermelho · Laranja |
| 🌳 Parques e áreas verdes | Círculo proporcional à área | Verde |

**Recursos interativos do mapa:**
- **Popups** ao clicar em cada marcador, com nome, bairro e dados do equipamento
- **Tooltips** ao passar o mouse, exibindo o nome rapidamente
- **Mini-mapa** de contexto no canto inferior direito
- **Ferramenta de medição** (canto superior direito) — o aluno pode medir distâncias diretamente no mapa
- **Controle de camadas** (canto superior esquerdo) — liga/desliga cada categoria

Arquivo salvo: `mapa1_equipamentos_publicos.html`

---

### Célula 5 · Mapa 2 — Rotas dos alunos até as escolas

Desenha linhas tracejadas coloridas conectando a residência de cada aluno à sua escola mais próxima. Cada aluno tem uma cor distinta. No ponto médio de cada rota, aparece a distância em quilômetros.

**Elementos do mapa:**
- 🏠 Marcador cinza → residência do aluno
- 🏫 Marcador azul → escola de destino
- `- - -` Linha tracejada colorida → rota (em linha reta)
- Etiqueta no meio da rota com a distância em km

> **Para avançar:** na atividade com turmas mais avançadas, as linhas retas podem ser substituídas por rotas reais de rua usando a [API gratuita do OpenRouteService](https://openrouteservice.org), que retorna o traçado real pelo sistema viário.

Arquivo salvo: `mapa2_rotas_alunos_escolas.html`

---

### Célula 6 · Mapa 3 — Mapa de calor (heatmap) da cobertura territorial

Gera um **mapa de calor** sobre fundo escuro que revela visualmente onde os equipamentos públicos estão concentrados — e onde há "vazios de serviços públicos".

| Cor | Significado |
|-----|-------------|
| 🔴 Vermelho | Alta concentração de equipamentos |
| 🟠 Laranja | Concentração média |
| 🟡 Amarelo | Concentração baixa |
| 🔵 Azul | Ausência ou baixíssima cobertura |

Os hospitais e UPAs têm **peso maior** no heatmap (maior impacto territorial); os parques têm peso proporcional à sua área. As residências dos alunos são marcadas com círculos coloridos para contextualizar quem mora nas áreas de menor cobertura.

Arquivo salvo: `mapa3_heatmap_equipamentos.html`

---

### Célula 7 · Análise de desigualdades territoriais + debate

Gera um relatório textual comparando o acesso de cada aluno aos equipamentos públicos, incluindo barras de texto proporcional às distâncias e tabela de equipamentos por bairro.

**Saída esperada:**
```
📏 DISTÂNCIAS CASA → ESCOLA (km):
───────────────────────────────────────────────────────
  Aluno A (Centro      ): 0.87 km  ████████
  Aluno B (Jardim Sul  ): 1.23 km  ████████████
  Aluno C (Bela Vista  ): 1.56 km  ███████████████
  Aluno D (Parque Norte): 0.94 km  █████████
  Aluno E (Vila Nova   ): 1.41 km  ██████████████

  Distância média:  1.20 km
  Distância máxima: 1.56 km (Aluno C)
  Distância mínima: 0.87 km (Aluno A)
  Razão máx/mín:    1.8x

🏘️ EQUIPAMENTOS PÚBLICOS POR BAIRRO:
───────────────────────────────────────────────────────
  Centro         : ████░░ | 🏫 1 escola  🏥 2 saúde  🌳 2 parques
  Jardim Sul     : ███░░░ | 🏫 1 escola  🏥 1 saúde  🌳 1 parque
  Bela Vista     : ██░░░░ | 🏫 1 escola  🏥 0 saúde  🌳 1 parque
  Parque Norte   : ██░░░░ | 🏫 1 escola  🏥 1 saúde  🌳 0 parques
  Vila Nova      : ██░░░░ | 🏫 1 escola  🏥 1 saúde  🌳 0 parques
```

**Perguntas para debate em sala:**

1. Observe o mapa de calor: quais bairros têm mais equipamentos públicos? Isso coincide com as áreas de maior renda?
2. Compare as distâncias dos alunos até a escola. Essa diferença é justa? Quem é mais afetado?
3. Um aluno que mora a 2 km da escola leva quanto tempo a pé? E de ônibus? E se não houver transporte público no bairro?
4. O que significa "direito à cidade"? Os moradores de todos os bairros têm o mesmo acesso aos equipamentos públicos?
5. Se você fosse gestor municipal, onde construiria a próxima escola ou UBS? Justifique com base nos mapas produzidos.

---

## Conceitos geográficos trabalhados na atividade

**Lugar** — categoria central da Geografia Humanista, entendida como espaço vivido e carregado de significados. Callai (2005) defende que o lugar de vivência dos alunos é o ponto de partida mais potente para o ensino geográfico, pois conecta o conhecimento científico à experiência concreta.

**Equipamentos públicos** — infraestruturas e serviços disponibilizados pelo Estado à população: escolas, unidades de saúde, parques, praças, creches etc. Sua distribuição espacial é um indicador direto de desigualdade territorial.

**Direito à cidade** — conceito de Henri Lefebvre que designa o direito de todos os cidadãos ao acesso equitativo aos bens e serviços urbanos, independentemente do bairro em que residem.

**Heatmap (mapa de calor)** — técnica de visualização que representa a densidade espacial de um fenômeno por meio de gradientes de cor. Amplamente usado em análises de vulnerabilidade territorial, saúde pública e segurança.

**Fórmula de Haversine** — fórmula matemática que calcula a distância geodésica (em linha reta sobre a superfície esférica da Terra) entre dois pontos a partir de suas coordenadas geográficas. Mais precisa que o cálculo euclidiano plano para distâncias maiores que alguns quilômetros.

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

**Partir do lugar vivido:** antes de mostrar qualquer mapa, peça aos alunos que desenhem no papel o trajeto que fazem de casa até a escola. Depois, compare os desenhos com o mapa digital produzido — essa confrontação entre percepção e dado real é o coração da atividade.

**Privacidade dos alunos:** nunca peça o endereço completo. Use apenas o nome do bairro e trabalhe com o centroide (ponto central aproximado) do bairro. Explique aos alunos por que isso é importante — é também uma oportunidade para discutir privacidade de dados geográficos.

**Personalizar para a cidade real:** substitua as coordenadas da cidade fictícia pelos dados reais do município onde a escola está localizada. O IBGE, o DataSUS (CNES) e o Inep (Censo Escolar) disponibilizam gratuitamente as coordenadas de equipamentos públicos de todos os municípios brasileiros.

**Para avançar com a turma:** uma vez dominado o código básico, os alunos podem acrescentar novas camadas — pontos de ônibus, ciclovias, áreas de risco de enchente — usando dados do OpenStreetMap via biblioteca [OSMnx](https://osmnx.readthedocs.io), também gratuita.

**Para baixar os mapas:** no painel esquerdo do Colab, clique no ícone de pasta 📁, localize os arquivos `.html` e clique com o botão direito → *Fazer download*. Os mapas funcionam offline no navegador sem necessidade de internet.

> ⚠️ **Atenção:** o Google Colab apaga os arquivos gerados quando a sessão é encerrada. Baixe os mapas antes de fechar o navegador, ou salve no Google Drive com:
> ```python
> from google.colab import drive
> drive.mount('/content/drive')
> ```

---

## Fontes dos dados

CALLAI, Helena Copetti. Aprendendo a ler o mundo: a geografia nos anos iniciais do ensino fundamental. *Cadernos CEDES*, Campinas: UNICAMP, v. 25, n. 66, p. 227-247, maio-ago. 2005. Disponível em: <https://www.scielo.br/j/ccedes/a/3BJWQ6GqwGCfTbpDhyFmqpS>. Acesso em: mar. 2026.

DATASUS. *Cadastro Nacional de Estabelecimentos de Saúde (CNES)*. Brasília: Ministério da Saúde, 2023. Disponível em: <https://cnes.datasus.gov.br>. Acesso em: mar. 2026.

INEP. *Censo Escolar da Educação Básica 2023*. Brasília: INEP, 2023. Disponível em: <https://inep.gov.br/censo-escolar>. Acesso em: mar. 2026.

OPENSTREETMAP. *OpenStreetMap*. OpenStreetMap Foundation, 2024. Disponível em: <https://www.openstreetmap.org>. Acesso em: mar. 2026.
