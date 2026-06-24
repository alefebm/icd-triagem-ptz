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
Este conjunto de dados reúne informações extraídas da literatura científica sobre os efeitos de substâncias com potencial anticonvulsivante e neuroprotetor avaliadas no modelo experimental de crises induzidas por pentilenotetrazol (PTZ) em camundongos. Os dados serão utilizados como base para futuras análises estatísticas e desenvolvimento de modelos preditivos aplicados à descoberta de fármacos.

Cada observação representa informações extraídas da literatura científica relacionadas ao efeito de substâncias experimentais sobre parâmetros de proteção contra crises convulsivas e mortalidade. Os dados estruturados incluem medidas temporais associadas ao aparecimento das crises e à morte dos animais, bem como uma variável categórica que indica a presença ou ausência de efeito protetor.

## Processo de coleta dos dados
A coleta dos dados foi realizada por meio de técnicas de Web Scraping implementadas em Python, em ambiente Jupyter Notebook. Inicialmente, foi utilizada a API Entrez do National Center for Biotechnology Information (NCBI) para recuperar artigos científicos do repositório PubMed Central (PMC), que disponibiliza o texto completo dos artigos em formato XML.

A busca foi limitada a estudos experimentais envolvendo crises induzidas por pentilenotetrazol em camundongos e compostos com potencial anticonvulsivante ou neuroprotetor. Os arquivos XML obtidos foram processados utilizando a biblioteca BeautifulSoup com o interpretador nativo `html.parser`, permitindo a extração do conteúdo textual dos artigos.

As informações quantitativas foram identificadas por meio de Expressões Regulares (Regular Expressions), capazes de reconhecer padrões matemáticos relacionados às latências convulsivas e aos tempos até a morte. Para aumentar a qualidade dos dados, foi implementada uma estratégia baseada em lista negra (blacklist), excluindo automaticamente valores provenientes de grupos controle ou de fármacos padrão, como diazepam, fenitoína e valproato.

Em conformidade com o conceito de Sweat Equity, apresentado por Steven Skiena em The Data Science Design Manual, optou-se por uma abordagem híbrida entre automação e curadoria humana. O processo automatizado é responsável pela extração das variáveis quantitativas, enquanto a identificação e classificação das substâncias testadas serão realizadas manualmente em etapa posterior, garantindo maior confiabilidade e qualidade ao conjunto de dados.

## Dicionário de Dados
| Nome da coluna                        | Descrição                                                                                                      | Exemplo     |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ----------- |
| **pmcid_referencia**                  | Identificador do artigo científico na base PubMed Central (PMC).                                               | PMC6269576  |
| **substancia_testada**                | Nome da substância avaliada experimentalmente. Inicialmente mantida vazia para posterior preenchimento manual. | Naringenina |
| **media_latencia_primeira_crise**     | Média do tempo até o aparecimento da primeira crise convulsiva, em segundos.                                   | 76,0        |
| **desvio_erro_padrao_primeira_crise** | Desvio padrão ou erro padrão associado à latência da primeira crise, em segundos.                              | 2,5         |
| **media_latencia_morte**              | Média do tempo até a morte dos animais, em segundos.                                                           | 1800,0      |
| **desvio_erro_padrao_morte**          | Desvio padrão ou erro padrão associado ao tempo até a morte, em segundos.                                      | 0,0         |
| **protecao_target**                   | Indica se a substância apresentou efeito anticonvulsivante/neuroprotetor.                                      | Sim         |

## Disponibilidade dos dados
O arquivo .xlsx contendo os dados coletados encontra-se disponível no seguinte link: https://docs.google.com/spreadsheets/d/1B-RZQIMEeKE7j7OJTgCbtLA0r48hItP7/edit?usp=drive_link&ouid=104361187681590337862&rtpof=true&sd=true

OBS: O arquivo disponibilizado corresponde à versão consolidada do banco de dados após a etapa de extração automatizada. A coluna referente à substância testada será posteriormente complementada por meio de curadoria manual especializada.
