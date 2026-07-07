# Análise de Casos de Chikungunya — Brasil, Estados e Municípios

> Projeto de vigilância epidemiológica para acompanhamento de casos **notificados** e **prováveis** de Chikungunya no Brasil, com visualizações automatizadas em nível nacional, estadual e municipal.

---

## Sobre o projeto

A Chikungunya é uma arbovirose transmitida pelo mosquito *Aedes aegypti* e representa um desafio contínuo para a saúde pública brasileira. Monitorar a evolução dos casos ao longo do tempo e do espaço é essencial para orientar ações de vigilância, prevenção e resposta rápida.

Este repositório reúne dois notebooks em Python que transformam bases de dados brutas de vigilância em **relatórios visuais prontos para leitura**, sem que o usuário precise escrever uma única linha de código:

| Notebook | O que ele faz |
|---|---|
| `chik_analise_brasil_estados.ipynb` | Consolida os dados de todo o país, gera análises por Unidade Federativa (UF) e permite um recorte detalhado para um estado específico. |
| `chik_analise_municipio.ipynb` | Aprofunda a análise para um único município escolhido pelo usuário. |

Ao final da execução, os notebooks geram automaticamente **gráficos em alta resolução (.png)** e um **relatório consolidado em PDF**, prontos para serem compartilhados com equipes técnicas, gestores ou apresentados em reuniões.

> **Não é preciso ser programador para usar este projeto.** As instruções abaixo foram escritas para que qualquer pessoa — mesmo sem experiência em tecnologia — consiga instalar as ferramentas necessárias e rodar as análises.

---

## Outputs de análise

- **Mapa coroplético do Brasil**, colorindo cada estado de acordo com o número de casos prováveis;
- **Gráficos de barras** com a distribuição de casos por UF, por município e por semana epidemiológica;
- **Comparativos entre bases**: casos confirmados no SINAN *versus* exames positivos no GAL (RT-PCR);
- **Classificação final dos casos** (confirmado, descartado, em investigação) ao longo do tempo;
- **Tabelas resumo** prontas para impressão;
- **Relatório final em PDF**, com todos os gráficos organizados e identificados por página.

Tudo isso pode ser gerado para o **Brasil como um todo**, para **um estado específico** ou para **um município específico**, bastando ajustar algumas variáveis simples no início do código (explicado na seção [Como usar](#-como-usar)).

---

## Fontes de dados utilizadas

| Sigla | Nome completo | O que fornece |
|---|---|---|
| **SINAN** | Sistema de Informação de Agravos de Notificação | Casos notificados e classificação final (confirmado, descartado, em investigação) |
| **GAL** | Gerenciador de Ambiente Laboratorial | Resultados de exames laboratoriais (RT-PCR), incluindo exames realizados e positivos |

> **Atenção — dados sensíveis.** As bases do SINAN e do GAL contêm informações de saúde e não são distribuídas junto a este repositório. Cada usuário deve obter suas próprias bases de dados, respeitando as normas de acesso e proteção de dados de sua instituição (LGPD, sigilo em saúde, etc.). O código foi feito para ler arquivos com nomes e estrutura específicos — veja a seção [Estrutura de arquivos esperada](#-estrutura-de-arquivos-esperada).

---

## Tecnologias usadas

O projeto foi desenvolvido em **Python**, dentro de **Jupyter Notebook**, utilizando as seguintes bibliotecas:

| Biblioteca | Para que serve no projeto |
|---|---|
| [pandas](https://pandas.pydata.org/) | Leitura, limpeza e cruzamento das bases de dados |
| [numpy](https://numpy.org/) | Cálculos numéricos (ex.: taxas de positividade) |
| [matplotlib](https://matplotlib.org/) | Construção dos gráficos e tabelas visuais |
| [seaborn](https://seaborn.pydata.org/) | Estilização e paletas de cores dos gráficos |
| [geopandas](https://geopandas.org/) | Construção do mapa coroplético do Brasil |
| [scipy](https://scipy.org/) | Funções estatísticas de apoio (ajuste de curvas, regressões) |
| [dbfread](https://dbfread.readthedocs.io/) | Leitura de arquivos `.dbf` (formato nativo do SINAN) |
| [openpyxl](https://openpyxl.readthedocs.io/) | Leitura e escrita de arquivos `.xlsx` |
| [reportlab](https://www.reportlab.com/) | Geração automática dos relatórios em PDF |
| [tabulate](https://pypi.org/project/tabulate/) | Formatação de tabelas |

Não é necessário conhecer essas bibliotecas para usar o projeto — elas trabalham em segundo plano quando o código é executado.

---

## Instalação

### 1. Pré-requisitos

Antes de começar, você precisa ter instalado em seu computador:

1. **Python** (versão 3.9 ou superior) — [baixar aqui](https://www.python.org/downloads/)
2. **Jupyter Notebook** ou **JupyterLab** (ambiente onde os arquivos `.ipynb` são executados)
3. **Git** (opcional, apenas se for clonar o repositório pela linha de comando) — [baixar aqui](https://git-scm.com/downloads)
4. **Editor de código**, que pode ser o VS Code, Anaconda ou Google Colab (utilizado online, não precisa de instalação)

### 2. Baixar o projeto

**Opção A — Sem usar linha de comando (recomendado para quem não é da área técnica):**
1. Clique no botão verde **"Code"** na página do repositório no GitHub;
2. Selecione **"Download ZIP"**;
3. Extraia o arquivo ZIP em uma pasta de fácil acesso no seu computador.

**Opção B — Usando Git (para usuários com experiência técnica):**
```bash
git clone https://github.com/seu-usuario/nome-do-repositorio.git
cd nome-do-repositorio
```

### 3. Instalar as bibliotecas necessárias

Abra o **Prompt de Comando** (Windows), **Terminal** (Mac/Linux) ou o **Anaconda Prompt**, navegue até a pasta do projeto e execute:

```bash
pip install pandas numpy matplotlib seaborn scipy dbfread openpyxl geopandas reportlab tabulate
```

> 💡 Esse comando instala, de uma só vez, todas as ferramentas que os notebooks precisam para funcionar. É necessário ter conexão com a internet apenas nesta etapa.

### 4. Abrir os notebooks

Ainda no terminal, dentro da pasta do projeto, execute:

```bash
jupyter notebook
```

Isso abrirá o Jupyter no seu navegador. Basta clicar no arquivo `.ipynb` desejado para começar.

---

## 📁 Estrutura de arquivos esperada

Para que os notebooks funcionem corretamente, os seguintes arquivos devem estar **na mesma pasta** dos notebooks antes da execução:

```
📦 pasta-do-projeto
 ┣ 📜 chik_analise_brasil_estados.ipynb
 ┣ 📜 chik_analise_municipio.ipynb
 ┣ 📜 CHIKON_*.dbf                          (bases brutas do SINAN, uma por UF/período)
 ┣ 📜 chikungunya_analise_RTPCR.xlsx        (base do GAL)
 ┣ 📜 municipios_brasil.xlsx                (tabela de códigos IBGE dos municípios)
 ┗ 📜 brazil-states.geojson                 (malha geográfica dos estados, para o mapa)
```

Os arquivos intermediários e finais (planilhas tratadas, gráficos `.png` e relatórios `.pdf`) são gerados automaticamente pelo próprio código dentro de novas pastas, como `Chikungunya_brasil_graficos/`.

---

## Como usar

1. Coloque os arquivos de dados na pasta do projeto, conforme descrito acima;
2. Abra o notebook desejado no Jupyter;
3. Ajuste as variáveis de filtro logo no início do código. Por exemplo, para analisar um estado específico:

   ```python
   nome_estado = 'Mato Grosso do Sul'   # Nome do estado
   filtro_estado = 50                   # Código IBGE da UF
   data_analise = '01/07/2026'          # Data de referência dos dados
   ```

   Ou, para analisar um município específico:

   ```python
   nome_municipio = 'Dourados'   # NÃO usar acento
   mun_sinan = 500370            # Código IBGE (SINAN)
   mun_gal = nome_municipio.upper()
   populacao = 220_367           # População do município, usada em cálculos de taxa
   data_dados = '01/07/2026'
   ```

4. Execute as células do notebook em ordem, de cima para baixo (no menu do Jupyter: **Cell → Run All**, ou célula por célula com `Shift + Enter`);
5. Ao final, os gráficos estarão salvos em uma pasta específica (ex.: `Chikungunya_Mato Grosso do Sul_graficos/`) e um relatório em PDF será gerado automaticamente nessa mesma pasta.

---

## Como contribuir

Contribuições são muito bem-vindas, seja você da área de dados, epidemiologia ou apenas alguém com uma boa ideia de melhoria!

1. Faça um **fork** deste repositório;
2. Crie uma branch para sua alteração:
   ```bash
   git checkout -b minha-melhoria
   ```
3. Faça suas alterações e registre-as:
   ```bash
   git commit -m "Descrição clara da alteração realizada"
   ```
4. Envie sua branch para o GitHub:
   ```bash
   git push origin minha-melhoria
   ```
5. Abra um **Pull Request** descrevendo o que foi alterado e por quê.

**Sugestões de contribuição especialmente bem-vindas:**
- Novas visualizações ou indicadores epidemiológicos;
- Melhorias na performance do processamento de dados;
- Documentação e exemplos adicionais para usuários não técnicos;
- Correção de bugs ou tratamento de exceções nos scripts.

Se preferir, também é possível contribuir apenas relatando problemas (*issues*) ou sugestões, sem a necessidade de submeter código.

---

## Licença

Este projeto está disponível sob os termos que forem definidos pelo mantenedor do repositório. Recomenda-se incluir uma licença de código aberto (como [MIT](https://opensource.org/licenses/MIT) ou [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.html)) para deixar claro como o código pode ser usado, modificado e distribuído.

> A **licença do código** é independente da **confidencialidade dos dados de saúde** utilizados como insumo. Mesmo que o código seja aberto, os dados do SINAN e do GAL devem continuar sendo tratados conforme a legislação vigente de proteção de dados e sigilo em saúde.

---

## Créditos

Algoritmos originalmente desenvolvidos por **Dengue Brazil**, com foco em apoiar a vigilância epidemiológica de arboviroses no país.
