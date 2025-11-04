# Predição e Análise de Focos de Queimadas

Resumo curto  
Notebook principal: [predição_analise_focos_queimadas.ipynb](predição_analise_focos_queimadas.ipynb)

Descrição  
Este repositório contém um pipeline completo para extração, limpeza, análise exploratória, visualização e modelagem de focos de queimadas no Brasil, a partir dos microdados do INPE via basedosdados. O notebook realiza desde a consulta SQL até a comparação entre modelos (Logistic Regression, Random Forest, XGBoost, MLP).

Principais artefatos gerados
- Dataset raw salvo: `dados_queimadas.csv` (gerado por [predição_analise_focos_queimadas.ipynb](predição_analise_focos_queimadas.ipynb))  
- Dataset processado para modelos: `dados_processados_para_modelo.csv` (ver [`df_final`](TCC/predição_analise_focos_queimadas.ipynb))  
- Modelos e resultados: `resultados_cv_regressao_logistica.txt`, `resultados_cv_random_forest.txt`, `resultados_cv_xgboost.txt`, `resultados_cv_mlp.txt`  
- Modelo final (exemplo): `modelo_random_forest_final.pkl` (treinado como `modelo_rf_final` em [TCC/predição_analise_focos_queimadas.ipynb](TCC/predição_analise_focos_queimadas.ipynb))  
- Gráficos importantes: `evolucao_loss_ultimo_fold_mlp.png` e figuras geradas no notebook

Estrutura (relevante)
- [TCC/predição_analise_focos_queimadas.ipynb](TCC/predição_analise_focos_queimadas.ipynb) — notebook principal (extração → EDA → geração de amostras "não fogo" → modelagem)  
- [TCC/Readme.md](TCC/Readme.md) — README anterior (referência)  
- [Projeto Estabilidade de Crédito/credit_risk_model_stability.ipynb](Projeto Estabilidade de Crédito/credit_risk_model_stability.ipynb) — outro projeto no workspace (referência)  
- [Projeto Estabilidade de Crédito/README.md](Projeto Estabilidade de Crédito/README.md) — README do outro projeto

Fluxo resumido de execução
1. Executar a célula de instalação: `!pip install basedosdados` (no topo do notebook).  
2. Rodar consulta via [`basedosdados.read_sql`](TCC/predição_analise_focos_queimadas.ipynb) para obter os microdados (billing_id deve ser configurado).  
3. Salvar e carregar o CSV (`df` → limpeza → `df_limpo`) — variáveis: [`df`](TCC/predição_analise_focos_queimadas.ipynb), [`df_limpo`](TCC/predição_analise_focos_queimadas.ipynb).  
4. Gerar amostras negativas e construir dataset para modelagem (`df_final`) e salvar em `dados_processados_para_modelo.csv`.  
5. Treinar e validar modelos (Logistic, XGBoost, RandomForest, MLP) com validação cruzada e hold-out.  
6. Salvar métricas e modelos (`resultados_cv_*.txt`, `modelo_random_forest_final.pkl`).

Dependências principais
- Python 3.8+  
- pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, tensorflow, cuml, basedosdados, joblib

Como executar localmente (resumo)
1. Criar ambiente Python e instalar dependências:
   ```sh
   pip install basedosdados pandas numpy matplotlib seaborn scikit-learn xgboost tensorflow cuml joblib
   ```
2. Abrir e executar sequencialmente [TCC/predição_analise_focos_queimadas.ipynb](TCC/predição_analise_focos_queimadas.ipynb) no Jupyter ou VSCode.  
3. Ajustar `billing_id` para consultas via `basedosdados` antes de rodar a query.

Observações e recomendações rápidas
- O notebook cria amostras de "não fogo" artificialmente; considerar validação adicional com dados externos.  
- A variável `potencia_radiativa_fogo` é tratada como vazamento potencial em algumas etapas — foi testado com e sem ela; revisar esse ponto dependendo do objetivo.  
- Monitorar overfitting checando métricas de treino vs validação (o notebook já implementa `return_train_score=True` em CV e avaliação de folds).  
- Para reprodução em máquina sem GPU/TPU, ajustar treino de MLP (batch/epochs) ou usar apenas modelos CPU-friendly.

Referências no workspace
- Notebook principal: [TCC/predição_analise_focos_queimadas.ipynb](TCC/predição_analise_focos_queimadas.ipynb)  
- Outro projeto relacionado: [Projeto Estabilidade de Crédito/credit_risk_model_stability.ipynb](Projeto Estabilidade de Crédito/credit_risk_model_stability.ipynb)  
- README do outro projeto: [Projeto Estabilidade de Crédito/README.md](Projeto Estabilidade de Crédito/README.md)

Autor
- Marcos Vinicius da Silva

Licença e uso# Predição e Análise de Focos de Queimadas

Resumo  
Notebook principal: `predição_analise_focos_queimadas.ipynb`

## Visão Geral
Este projeto analisa e modela focos de queimadas no Brasil a partir de microdados do INPE (via basedosdados). O pipeline inclui extração, limpeza, EDA, visualizações temporais e espaciais, preparação de dados para modelagem e comparação de modelos preditivos.

## Autor
Marcos Vinicius da Silva

## Objetivos
- Extrair e consolidar dados de focos de queimadas.  
- Realizar limpeza e análise exploratória (sazonalidade, tendência e distribuição espacial).  
- Construir e comparar modelos de classificação para prever ocorrência de focos.  
- Gerar artefatos reproduzíveis (datasets processados, métricas e modelos salvos).

## Principais Saídas
- `dados_queimadas.csv` — dados brutos salvos.  
- `dados_processados_para_modelo.csv` — dataset final usado para modelagem.  
- `resultados_cv_*.txt` — métricas de validação cruzada por modelo.  
- `modelo_random_forest_final.pkl` — exemplo de modelo salvo.  
- Figuras e gráficos gerados no notebook (pasta `figures/`).

## Estrutura sugerida
- `predição_analise_focos_queimadas.ipynb` — notebook principal.  
- `data/` — dados brutos e processados.  
- `models/` — modelos serializados.  
- `results/` — arquivos de métricas e visualizações.  
- `README.md` — este arquivo.

## Dependências
- Python 3.8+  
- pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, tensorflow (opcional), basedosdados, joblib

Instalação mínima:
```sh
pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib basedosdados
```

## Como executar (resumo)
1. Ajuste credenciais/billing para consultas via `basedosdados` (se for usar a query).  
2. Abra o notebook `predição_analise_focos_queimadas.ipynb` no Jupyter ou VSCode.  
3. Execute as células na ordem: extração → limpeza → EDA → preparação de dados → modelagem → avaliação.  
4. Salve os artefatos (datasets, modelos e relatórios) nas pastas indicadas.

## Observações importantes
- Ao gerar amostras "não fogo" artificialmente, revise o balanceamento e a representatividade das classes.  
- Verifique leakage (por ex., potência radiativa) antes de treinar modelos.  
- Em ambientes sem GPU, ajuste parâmetros de treino de modelos pesados (MLP/XGBoost).

## Próximos passos recomendados
- Testar técnicas de balanceamento (SMOTE, undersampling).  
- Realizar explicabilidade (SHAP) para interpretar decisões do modelo.  
- Implementar monitoramento de desempenho em produção e atualização periódica do modelo.

## Autor
- Marcos Vinicius da Silva

## Licença
Dados públicos (INPE / basedosdados). Código: escolha uma licença (ex.: MIT) conforme necessário.
- Dados públicos (INPE / basedosdados). Ajustar licença do código conforme preferir.
