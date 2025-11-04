# Predição e Análise de Focos de Queimadas

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

## Licença
Dados públicos (INPE / basedosdados). Código: escolha uma licença (ex.: MIT) conforme necessário.