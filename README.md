# 🍦 Projeto Gelato Mágico — Previsão de Vendas com Azure ML

## 📘 Visão Geral
Este projeto foi desenvolvido para a **sorveteria Gelato Mágico**, localizada em uma cidade litorânea, com o objetivo de **prever a quantidade de sorvete vendida com base na temperatura média do dia**.

A solução foi construída **integralmente na interface gráfica do Azure Machine Learning Studio**, utilizando o recurso de **Automated Machine Learning (AutoML)**, com integração nativa ao **MLflow** e deploy em **endpoint online gerenciado (tempo real)**.

---

## 🧠 Objetivos do Projeto
- Treinar um modelo de **regressão preditiva** com Azure AutoML.
- Registrar e versionar o modelo utilizando **MLflow**.
- Implantar o modelo em **endpoint online gerenciado (real time)**.

---

## ☁️ Arquitetura da Solução

**Componentes Principais:**
- **Azure Machine Learning Workspace** — ambiente de orquestração.
- **Azure Storage (Blob)** — armazenamento do dataset CSV.
- **Azure AutoML (UI)** — treinamento sem código.
- **MLflow (integrado)** — rastreamento e versionamento.
- **Managed Online Endpoint** — deploy e inferência em tempo real.

---

## 🧾 Dataset
**Arquivo:** `GelatoMagico-Vendas.csv`  
**Campos:**
| Campo | Tipo | Descrição |
|--------|------|------------|
| Day | integer | Dia do mês |
| Month | string | Nome do mês curto |
| Temp | integer | Temperatura média do dia (°C) |
| Sells | integer | Quantidade de sorvetes vendidos |

**Exemplo:**

| Day | Month | Temp | Sells |
| --- | ----- | ---- | ----- |
| 01 | JAN | 28 | 170 |
| 02 | JAN | 29 | 190 |

---

## ⚙️ Etapas do Projeto (Interface do Azure ML)

### 1️⃣ Preparação
1. Acesse o portal [Azure ML Studio](https://ml.azure.com).
2. Crie ou selecione um Workspace (ex: `ws-gelato-magico`).
3. Conecte um **Azure Blob Storage** como Datastore.

### 2️⃣ Dataset
1. Vá em **Assets → Datasets → + Create dataset → From local file**.
2. Faça upload de `GelatoMagico-Vendas.csv`.
3. Configure os tipos de coluna.
4. Salve como **gelato-vendas:v1**.

### 3️⃣ AutoML (Regressão)
1. **Automated ML → + New job**
2. Dataset: `gelato-vendas:v1`
3. Task type: **Regression**
4. Target column: `Quantidade_Vendida`
5. Primary metric: `R2_score`
6. Validation: 5-fold cross-validation
7. Compute: `cpu-cluster-gelato`
8. Execute (Run)

### 4️⃣ Registro do Modelo
- Após o treino, abra o **Job AutoML**.
- Selecione o melhor modelo do *leaderboard*.
- Clique em **Register model → modelo-vendas-gelato**.

### 5️⃣ Deploy em Tempo Real
- Acesse **Assets → Models → modelo-vendas-gelato**.
- Clique em **Deploy → Deploy to Online Endpoint**.
- Nome: `gelato-online-endpoint`
- Tipo: `Standard_F2s_v2`
- Teste o endpoint via UI com:
  ```json
  {"data":[{"Temperatura_Media": 33.5}]}
  ```

---

## 🧩 Reprodutibilidade e Governança
- Todos os experimentos e modelos são **versionados automaticamente**.
- O **MLflow** integrado ao Workspace gerencia métricas, parâmetros e artefatos.
- Cada run do pipeline gera logs e snapshots reexecutáveis.
- Use **tags** e **versões** em datasets, jobs e modelos.

---

## 📈 Métricas Esperadas
| Métrica | Descrição | Meta Esperada |
|----------|------------|----------------|
| R² | Coeficiente de determinação | ≥ 0.85 |
| RMSE | Erro quadrático médio | ≤ 10% da média de vendas |

---

## 🧰 Tecnologias Utilizadas
- Azure Machine Learning Studio (UI)
- Azure AutoML
- MLflow (integrado)
- Azure Storage (Blob)
- Managed Online Endpoints

---

## 👨‍💻 Equipe / Responsáveis
**Projeto:** Gelato Mágico — Previsão de Vendas  
**Especialista Azure ML:** _Bruno César F. Silva_  
**Cliente:** Sorveteria Gelato Mágico  
**Data:** Novembro de 2025  

---

## 📜 Licença
Este projeto é disponibilizado sob a licença **MIT** — sinta-se livre para adaptar e reutilizar, desde que citada a fonte.

---

## 💡 Recursos Úteis
- [Azure Machine Learning Studio](https://ml.azure.com)
- [Documentação do Azure AutoML](https://learn.microsoft.com/azure/machine-learning/concept-automated-ml)
- [Deploy de modelos com Managed Online Endpoints](https://learn.microsoft.com/azure/machine-learning/how-to-deploy-managed-online-endpoints)
- [MLflow e Azure ML Integration](https://learn.microsoft.com/azure/machine-learning/how-to-use-mlflow)

---
