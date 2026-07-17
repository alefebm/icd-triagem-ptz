# Projeto ICD: Modelo de Triagem Preditiva de Fármacos Antiepilépticos

**Disciplina:** Introdução à Ciência de Dados  
**Professor:** Dr. Yuri Malheiros  

# 1ª FASE
## Integrantes da Equipe
1. Álefe Brito Monteiro
2. Antonio Jose Batista Salazar
3. Igor Barbosa Rodrigues de Oliveira
4. João Batista de Araújo Martins

## Tema do Projeto
Modernização da triagem (*screening*) preditiva de fármacos antiepilépticos utilizando dados publicados na literatura científica de pesquisas que aplicaram o modelo agudo de crises epilépticas (convulsões) induzidas por pentilenotetrazol (PTZ) em camundongos.

## Abordagem de Coleta dos Dados
Para garantir a consistência dos registros e evitar problemas complexos de compatibilidade, a nossa abordagem de coleta focará na extração automatizada de dados de uma única fonte primária: a **API do National Center for Biotechnology Information (NCBI)**, parte da Biblioteca Nacional de Medicina (NLM) dos EUA. O portal do NCBI/PubMed Central (PMC) é um repositório digital de artigos completos de livre acesso rico em dados biomédicos e farmacológicos, com uma API consolidada (o *Entrez*). Espera-se que ele sozinho já fornecerá dados suficientes para demonstrar a prova de conceito preditivo sobre o modelo PTZ. O uso de bases adicionais, como o *ScienceDirect*, está previsto apenas como uma expansão futura, caso haja necessidade de enriquecer o volume de dados.

Utilizaremos a linguagem Python (com as bibliotecas `requests` e `json`) para buscar e extrair informações de artigos científicos publicados sobre testes com o modelo PTZ. O objetivo é converter os dados textuais (não estruturados) em um formato estruturado (*Data Frame*) para o treinamento de um modelo preditivo de base (*baseline*). Durante a extração, teremos um cuidado especial em capturar não apenas as medidas de tendência central dos resultados (como a média da latência), mas também as medidas de dispersão (como o desvio ou erro padrão), garantindo a robustez estatística das *features*.

# 2ª FASE
## Descrição do conjunto de dados
Este conjunto de dados foi desenvolvido para servir como uma **baseline para modelos de predição de potencial anticonvulsivante de novos compostos bioativos**. O dataset contém informações extraídas de estudos científicos que avaliaram substâncias naturais, sintéticas ou semissintéticas utilizando o modelo experimental **de convulsão induzida por Pentilenotetrazol (PTZ) em camundongos**.

Os dados foram obtidos a partir da literatura científica e organizados em uma estrutura padronizada contendo informações sobre compostos testados, doses administradas, vias de administração e respostas farmacológicas observadas.

Devido à elevada heterogeneidade dos relatos experimentais encontrados na literatura (diferentes formas de apresentação de médias, desvios, medianas e critérios estatísticos), os dados quantitativos da proposta original foram transformados em **fenótipos binários de classificação**, permitindo a construção de uma matriz mais adequada para algoritmos de Machine Learning.

A classificação utilizada foi:

- `1` → presença de efeito anticonvulsivante/neuroprotetor estatisticamente validado;
- `0` → ausência de efeito terapêutico observado.

Dessa forma, o conjunto de dados permite a identificação de padrões associados ao potencial farmacológico de diferentes moléculas e pode ser utilizado como base para modelos preditivos de classificação de candidatos a novos fármacos antiepilépticos.

## Processo de coleta dos dados
Os dados foram coletados por meio da API Entrez (NCBI), utilizando consultas ao banco PubMed Central (PMC) para obtenção dos artigos em formato XML. Quando o texto completo não estava disponível, foram utilizados os resumos indexados no PubMed. A extração foi realizada em Python com as bibliotecas `requests`, `BeautifulSoup`, `re` (Expressões Regulares) e `pandas`. Foram utilizadas expressões regulares e regras de validação para identificar os parâmetros experimentais de interesse. Quando necessário, foi aplicada curadoria manual, conforme o conceito de *Sweat Equity* descrito por Steven Skiena.

# Dicionário de Dados
| Nome da coluna | Descrição | Exemplo |
|---|---|---|
| `pmid_pmc_referencia` | Identificador do artigo científico utilizado como fonte dos dados (PubMed ID ou PubMed Central ID). | `PMC702134` |
| `substancia_testada` | Nome da substância ou composto avaliado no experimento. | `cinnamic alcohol` |
| `dose_mg_kg` | Dose administrada da substância no modelo experimental, expressa em mg/kg. | `50.0` |
| `via_administracao` | Via utilizada para administração do composto no animal. | `i.p.` |
| `aumento_latencia_crise` | Indica se houve aumento significativo do tempo até a primeira crise epiléptica após o tratamento. Valor binário: 1 = sim; 0 = não. | `1` |
| `reducao_severidade_racine` | Indica se ocorreu redução significativa da severidade das crises avaliada pela escala de Racine. Valor binário: 1 = sim; 0 = não. | `0` |
| `protecao_contra_morte` | Indica se o composto apresentou proteção contra mortalidade induzida pelo modelo experimental. Valor binário: 1 = sim; 0 = não. | `1` |
| `target_anticonvulsivante` | Variável alvo do modelo de Machine Learning. Assume valor 1 quando o composto apresenta pelo menos um efeito anticonvulsivante positivo e 0 quando não apresenta efeito terapêutico observado. | `1` |

## Disponibilidade dos dados
O conjunto de dados estruturado está consolidado e disponível em dois formatos `.csv` e `.xlsx`. Os arquivos encontram-se disponíveis no seguinte link: https://drive.google.com/drive/folders/1z-ccp0WHS1WI2nzWEUvTUkL50rD7MMe4?usp=drive_link
