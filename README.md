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
Os dados foram coletados por meio da API Entrez (NCBI), utilizando consultas ao banco PubMed Central (PMC) para obtenção dos artigos em formato XML. A extração foi realizada em Python com as bibliotecas `requests`, `BeautifulSoup`, `re` (Expressões Regulares) e `pandas`. Foram utilizadas expressões regulares e regras de validação para identificar os parâmetros experimentais de interesse. Quando necessário, será aplicada curadoria manual, conforme o conceito de *Sweat Equity* descrito por Steven Skiena.

| Nome da coluna | Descrição | Exemplo |
| :--- | :--- | :--- |
| **PMCID** | Identificador único do artigo no PubMed Central. | `PMC12956243` |
| **Titulo** | Título do artigo científico de origem. | `Anticonvulsant activity of compound X...` |
| **Target_Efeito_Protetor** | Variável Alvo (Classificação Híbrida Semântico-Numérica). Indica se o composto em teste demonstrou efeito anticonvulsivante/neuroprotetor significativo ("Sim" ou "Não"). | `Sim` |
| **Doses_Testadas_mg_kg** | Lista contendo as doses administradas do composto experimental (mg/kg). | `[50, 100, 200]` |
| **Latencias_Crises_M_SD_s** | Lista de tuplas no formato `(Média, Dispersão)` representando a latência para a primeira crise e seu respectivo Desvio Padrão (SD) ou Erro Padrão (SEM) em segundos. | `[(117.8, 12.12), (163.5, 35.2)]` |
| **Latencias_Morte_M_SD_s** | Lista de tuplas no formato `(Média, Dispersão)` representando a latência para o desfecho de óbito e seu respectivo SD/SEM em segundos. | `[(1411.0, 461.7), (1800.0, 0.0)]` |
| **Score_Racine_Teste** | Lista de scores máximos da Escala de Racine (0 a 6) atingidos **apenas** pelo grupo tratado com o composto experimental. | `[3, 4]` |
| **Trecho_Conclusao** | Fragmento de texto extraído das seções de Conclusão, Discussão ou Abstract utilizado pelo algoritmo de NLP para validação de contexto. | `The results suggest that compound X significantly increased the latency...` |

## Disponibilidade dos dados
O conjunto de dados estruturado está consolidado e disponível em dois formatos `.csv` e `.xlsx`. Os arquivos encontram-se disponíveis no seguinte link: https://drive.google.com/drive/folders/1z-ccp0WHS1WI2nzWEUvTUkL50rD7MMe4?usp=drive_link
