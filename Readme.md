# Predição e Análise de Focos de Queimadas no Brasil

Este projeto tem como objetivo analisar e prever focos de queimadas no Brasil utilizando dados públicos do INPE, integrados via [basedosdados](https://basedosdados.org/). O pipeline inclui extração, limpeza, análise exploratória, visualização geográfica e temporal, geração de amostras para modelagem e comparação de modelos preditivos.

## Estrutura do Projeto

- `predição_analise_focos_queimadas.ipynb`: Notebook principal com todo o pipeline de análise e modelagem.
- `dados_queimadas.csv`: Dados brutos extraídos da base INPE.
- `dados_processados_para_modelo.csv`: Dados tratados e balanceados para treinamento dos modelos.
- `resultados_cv_regressao_logistica.txt`, `resultados_cv_random_forest.txt`, `resultados_cv_mlp.txt`: Resultados da validação cruzada dos modelos.
- `comparacao_modelos_cv.txt`: Comparação final das métricas dos modelos.

## Principais Etapas

1. **Extração dos Dados**
   - Consulta SQL via `basedosdados` para obter informações detalhadas dos focos de queimadas, bioma, localização, condições meteorológicas e datas.

2. **Limpeza e Pré-processamento**
   - Substituição de valores inválidos.
   - Remoção de linhas com dados essenciais faltantes.
   - Criação de amostras negativas ("não fogo") para balanceamento.

3. **Análise Exploratória**
   - Estatísticas descritivas, verificação de nulos e duplicados.
   - Visualizações: distribuição temporal, espacial, sazonalidade, intensidade por bioma.

4. **Modelagem Preditiva**
   - Geração de dataset balanceado para classificação binária (fogo vs. não fogo).
   - Treinamento e validação cruzada de três modelos:
     - Regressão Logística (cuML)
     - Random Forest
     - MLP (Keras/TensorFlow)
   - Avaliação por acurácia, precisão, recall e F1-score.

5. **Comparação de Modelos**
   - Leitura automática dos resultados.
   - Geração de tabela comparativa e seleção do melhor modelo.

6. **Análise de Importância das Variáveis**
   - Feature importance do Random Forest para identificar os fatores mais relevantes.

## Como Executar

1. Instale as dependências:
   ```sh
   pip install basedosdados pandas numpy matplotlib seaborn scikit-learn tensorflow cuml
   ```
2. Configure o projeto de billing do Google Cloud para consultas SQL públicas.
3. Execute o notebook `predição_analise_focos_queimadas.ipynb` sequencialmente.

## Resultados Esperados

- Visualizações claras sobre onde, quando e por que ocorrem queimadas.
- Modelos preditivos comparados por validação cruzada.
- Identificação dos principais fatores que influenciam a ocorrência de fogo.

## Limitações e Próximos Passos

- O balanceamento entre classes é artificial (amostras negativas geradas).
- O pipeline pode ser expandido para incluir variáveis climáticas externas e séries temporais mais avançadas.
- Testar outros algoritmos e técnicas de feature engineering.

## Autor

Marcos Vinicius da Silva

---

**Resumo:**  
Este projeto oferece uma abordagem completa para análise e predição de queimadas, combinando ciência de dados, visualização e machine learning, com código aberto e dados públicos.