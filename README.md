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
Este conjunto de dados reúne informações experimentais extraídas de artigos científicos publicados no PubMed Central (PMC) sobre compostos avaliados no modelo agudo de crises induzidas por pentilenotetrazol (PTZ) em camundongos. O objetivo é estruturar um banco de dados contendo parâmetros farmacológicos relevantes para estudos de compostos com potencial anticonvulsivante e neuroprotetor.

## Processo de coleta dos dados
Os dados foram coletados por meio da API Entrez (NCBI), utilizando consultas ao banco PubMed Central (PMC) para obtenção dos artigos em formato XML. A extração foi realizada em Python com as bibliotecas requests, BeautifulSoup, re e pandas. Foram utilizadas expressões regulares e regras de validação para identificar os parâmetros experimentais de interesse. Quando necessário, será aplicada curadoria manual, conforme o conceito de Sweat Equity descrito por Steven Skiena.

## Dicionário de Dados
| Nome da coluna                        | Descrição                                                                                      | Exemplo    |
| ------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------- |
| **pmcid_referencia**                  | Identificador do artigo no PubMed Central.                                                     | PMC4142302 |
| **substancia_testada**                | Nome do composto experimental avaliado.                                                        | α-Pinene   |
| **dose_mg_kg**                        | Dose administrada ao grupo experimental (mg/kg).                                               | 200        |
| **media_latencia_primeira_crise**     | Média da latência para a primeira crise (segundos).                                            | 82.5       |
| **desvio_erro_padrao_primeira_crise** | Desvio padrão ou erro padrão da média da primeira crise (segundos).                            | 4.1        |
| **media_latencia_morte**              | Média da latência para a morte (segundos).                                                     | 1800       |
| **desvio_erro_padrao_morte**          | Desvio padrão ou erro padrão da média da latência para a morte (segundos).                     | 0.0        |
| **protecao_target**                   | Indica se o composto apresentou efeito anticonvulsivante/neuroprotetor no modelo experimental. | Sim        |

## Disponibilidade dos dados
O arquivo .xlsx contendo os dados coletados encontra-se disponível no seguinte link: 
