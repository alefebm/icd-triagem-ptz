# Projeto ICD: Modelo de Triagem Preditiva de Fármacos Antiepilépticos

**Disciplina:** Introdução à Ciência de Dados  
**Professor:** Dr. Yuri Malheiros  

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
