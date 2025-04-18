## Objetivo do Projeto

O intuito deste projeto é realizar a **detecção de corações anômalos** com base no dataset **ECG5000**, que contém eletrocardiogramas (ECGs) classificados em diferentes tipos de batimentos cardíacos.

---

## Sobre o Dataset

O dataset **ECG5000** é composto por registros de eletrocardiogramas contendo **140 pontos temporais** por amostra. As classes representadas no conjunto de dados são:

- **Normal (N)**
- **R-on-T Premature Ventricular Contraction (R-on-T PVC)**
- **Premature Ventricular Contraction (PVC)**
- **Supra-ventricular Premature or Ectopic Beat (SP or EB)**
- **Unclassified Beat (UB)**

A distribuição das amostras é a seguinte:

- 2.627 amostras Normais  
- 1.590 R-on-T PVC  
- 175 SP or EB  
- 86 PVC  
- 22 UB

---

## Preparação dos Dados

Durante a análise inicial:

- **Não foram encontrados dados faltantes**
- A **diferença entre valores mínimos e máximos** foi considerada aceitável

O dataset foi:

- Adaptado para o formato de **série temporal**
- Separado entre **corações normais** e **outros tipos**
- Dividido em **pastas de treinamento e validação**

---

## Arquitetura do Modelo

O modelo adotado foi baseado em **LSTM (Long Short-Term Memory)**, uma rede recorrente ideal para tarefas com dados sequenciais e séries temporais. Utilizamos uma estratégia de **autoencoder LSTM**, que permite:

- Codificar os sinais em uma forma comprimida (encoding)
- Decodificar esses sinais reconstruindo-os o mais próximo possível do original

A atualização dos pesos é feita com base no **erro entre o sinal de entrada e o sinal reconstruído**, forçando a rede a aprender os padrões normais.

### 🔧 Camadas da Rede

A arquitetura do modelo é composta por:

- Camadas de codificação: LSTM com 128, 64, 32 e 16 unidades
- Camadas de decodificação: LSTM com 16, 32, 64 e 128 unidades
- Camada **Dropout** para evitar overfitting

---

##  Estratégia de Treinamento

Durante o treinamento, **apenas corações normais foram utilizados**. O objetivo foi fazer com que a LSTM aprendesse exclusivamente os padrões esperados de um coração saudável.

A ideia central é que, ao tentar reconstruir um coração **anômalo**, o modelo apresentará maior dificuldade, gerando um **erro de reconstrução (MAE)** mais alto.

---

##  Resultados

Após o treinamento:

- O **Erro Absoluto Médio (MAE)** foi usado como métrica para definir um **limiar de anomalia**
- O modelo obteve:
  - **Acurácia de 94%**
  - **Sensibilidade de 100%**, métrica extremamente relevante no contexto da saúde


