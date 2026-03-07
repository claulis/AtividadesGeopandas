# Quem Somos Nós?
## Leitura do território a partir de dados do IBGE
**Atividade didática — Ensino de Geografia com Python**

> Dados: Censo Demográfico 2022 · IBGE/SIDRA · Bibliotecas: pandas, matplotlib

---

## Como rodar no Google Colab

1. Acesse [colab.research.google.com](https://colab.research.google.com) com sua conta Google
2. Clique em **Arquivo → Novo notebook**
3. Cole o código célula por célula (cada bloco `# ── CÉLULA` é uma célula separada)
4. Execute com **Shift+Enter** em cada célula, ou vá em **Ambiente de execução → Executar tudo**

> **Nenhuma instalação é necessária.** O Google Colab já vem com pandas e matplotlib pré-instalados.

---

## Estrutura do código — 7 células

### Célula 1 · Importação das bibliotecas

Carrega o **pandas** (manipulação de tabelas) e o **matplotlib** (gráficos), além de configurar o estilo visual padrão dos gráficos.

**Saída esperada:**
```
✅ Bibliotecas carregadas com sucesso!
```

---

### Célula 2 · Distribuição etária — Censo 2022

Define os dados de distribuição etária de 5 municípios (Manaus, Fortaleza, Belo Horizonte, Curitiba e Porto Alegre) e cria um **DataFrame** — a estrutura central do pandas, equivalente a uma planilha.

**Saída esperada:**
```
📊 Tabela: Distribuição etária por município (%)
                     0 a 14 anos  15 a 29 anos  30 a 59 anos  60 anos ou mais
Município
Manaus (AM)                 27.1          26.4          37.2              9.3
Fortaleza (CE)              24.8          25.9          37.5             11.8
Belo Horizonte (MG)         18.9          22.1          41.8             17.2
Curitiba (PR)               19.2          22.8          41.3             16.7
Porto Alegre (RS)           16.4          20.3          42.1             21.2
```

---

### Célula 3 · Renda e escolaridade

Cria dois DataFrames adicionais: renda média domiciliar per capita e grau de instrução da população de 25 anos ou mais. Todos os dados são do **Censo Demográfico 2022 (IBGE/SIDRA)**.

**Saída esperada:**
```
💰 Tabela: Renda média domiciliar per capita (R$)
🎓 Tabela: Grau de instrução por município (%)
```

---

### Célula 4 · Gráfico 1 — Distribuição etária (barras empilhadas)

Gera um gráfico de **barras empilhadas** comparando a composição etária dos 5 municípios. Cada cor representa uma faixa etária; os percentuais aparecem dentro de cada segmento.

Arquivo salvo: `grafico1_distribuicao_etaria.png`

| Cor | Faixa etária |
|-----|--------------|
| 🟦 Azul-água | 0 a 14 anos |
| 🔵 Azul | 15 a 29 anos |
| 🟢 Verde | 30 a 59 anos |
| 🟡 Amarelo | 60 anos ou mais |

---

### Célula 5 · Gráfico 2 — Renda média (barras horizontais)

Cria barras horizontais ordenadas do menor para o maior valor, com cores que indicam faixas de renda:

| Cor | Faixa de renda |
|-----|----------------|
| 🔴 Vermelho | Abaixo de R$ 1.200 |
| 🟠 Laranja | R$ 1.200 a R$ 1.600 |
| 🟢 Verde | Acima de R$ 1.600 |

Arquivo salvo: `grafico2_renda_media.png`

---

### Célula 6 · Gráfico 3 — Escolaridade (barras agrupadas)

Gera barras agrupadas com 5 cores para os 5 níveis de instrução, permitindo comparação direta entre municípios para cada nível educacional.

Arquivo salvo: `grafico3_instrucao.png`

---

### Célula 7 · Análise automática + perguntas para debate

Identifica automaticamente os municípios com maior/menor renda, mais jovem, mais envelhecido e maior escolaridade. Apresenta 5 perguntas estruturadas para discussão em sala.

**Saída esperada:**
```
👶 Município com maior % de crianças (0-14 anos): Manaus (AM) (27.1%)
👴 Município com maior % de idosos (60+):          Porto Alegre (RS) (21.2%)

💰 Maior renda média: Porto Alegre (RS) (R$ 2.031)
💸 Menor renda média: Fortaleza (CE)   (R$ 1.021)
📐 Razão entre maior e menor renda: 2.0x

🎓 Maior % com ensino superior: Porto Alegre (RS) (28.2%)
📉 Menor % com ensino superior: Fortaleza (CE)   (14.5%)
```

**Perguntas para debate em sala:**

1. Por que municípios do Norte/Nordeste tendem a ter populações mais jovens? Que fatores geográficos e históricos explicam isso?
2. Existe relação entre renda média e grau de instrução nos municípios analisados? Como você explicaria essa relação?
3. O envelhecimento populacional de Porto Alegre e Curitiba traz quais desafios para a cidade? E quais oportunidades?
4. Seus dados confirmam ou contradizem as hipóteses que você formulou antes de ver os números?
5. O que esses dados **não** mostram sobre o território? Que outras informações você gostaria de ter?

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

**Antes de rodar o código:** peça aos estudantes que formulem hipóteses — *"Qual município terá mais idosos? Por quê?"* — e anotem suas respostas. Após a execução, compare as hipóteses com os dados reais. Essa é a essência da **aprendizagem ativa**.

**Para personalizar:** os alunos podem substituir os municípios na lista `municipios` e atualizar os dados correspondentes para analisar sua própria cidade ou região. Os dados do Censo 2022 estão disponíveis gratuitamente em [sidra.ibge.gov.br](https://sidra.ibge.gov.br).

**Para baixar os gráficos:** no painel esquerdo do Colab, clique no ícone de pasta 📁, localize os arquivos `.png` gerados e clique com o botão direito → *Fazer download*.

> ⚠️ **Atenção:** o Google Colab apaga os arquivos gerados quando a sessão é encerrada. Baixe os gráficos antes de fechar o navegador, ou monte seu Google Drive com o comando abaixo para salvar automaticamente:
> ```python
> from google.colab import drive
> drive.mount('/content/drive')
> ```

---

## Fonte dos dados

IBGE. *Censo Demográfico 2022*. Rio de Janeiro: IBGE, 2023. Disponível em: <https://sidra.ibge.gov.br>. Acesso em: mar. 2026.
