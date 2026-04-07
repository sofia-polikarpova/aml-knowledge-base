Этот репозиторий содержит заметки, эксперименты и код для дипломного проекта по анализу блокчейн-транзакций с использованием графовых нейронных сетей (GNN) для задачи Anti-Money Laundering (AML) на датасете Elliptic.  
  
## Цель проекта  
  
Цель работы — выявление подозрительных или мошеннических адресов в графе транзакций блокчейна с помощью моделей на графах.  
  
## Структура репозитория  
  
### `04-code/`  
Основные эксперименты, ноутбуки и заметки по моделям:  
- `12 Elliptic — GCN Baseline [Experiment.md](https://vk.com/away.php?to=https%3A%2F%2FExperiment.md&utf=1)`  
- `13 Elliptic — Graph Attention Network (GAT) [Experiment.md](https://vk.com/away.php?to=https%3A%2F%2FExperiment.md&utf=1)`  
- `14 Elliptic — Hierarchical Attention Network (HAN) [Experiment.md](https://vk.com/away.php?to=https%3A%2F%2FExperiment.md&utf=1)`  
- `15 Elliptic — SemiGNN experiment (3000-node subgraph).md`  
- `16 Elliptic — GCN, GAT, HAN [Comparison.md](https://vk.com/away.php?to=https%3A%2F%2FComparison.md&utf=1)`  
- `GNN_Elliptic.ipynb`  
- `GAT_Elliptic.ipynb`  
- `HAN_Elliptic.ipynb`  
- `SemiGNN_Elliptic.ipynb`  
- `all_models.ipynb`  
  
## Какие модели рассматриваются  
  
В проекте сравниваются четыре GNN-архитектуры:  
- GCN  
- GAT  
- HAN  
- SemiGNN  
  
## Датасет  
  
В основе экспериментов лежит датасет Elliptic с транзакциями Bitcoin.  
  
Используются файлы:  
- `elliptic_txs_features.csv`  
- `elliptic_txs_edgelist.csv`  
- `elliptic_txs_classes.csv`  
  
## Экспериментальная постановка  
  
В проекте используется:  
- общий предобработанный подграф для сравнения моделей;  
- разбиение на train / validation / test;  
- учёт дисбаланса классов;  
- подбор threshold по validation;  
- метрики, подходящие для несбалансированной бинарной классификации:  
- Precision  
- Recall  
- F1-score  
- PR-AUC  
- ROC-AUC  
- Accuracy  
  
## Как запускать ноутбуки  
  
Рекомендуемый порядок:  
1. Подготовка данных.  
2. Запуск отдельных ноутбуков по моделям.  
3. Сравнение результатов в `all_models.ipynb`.  
4. Изучение markdown-заметок в `04-code/` для интерпретации и выводов.  
  
## Примечания  
  
- В проекте особое внимание уделяется false positives, recall для класса illicit и корректному сравнению моделей.  
- Использование подграфа позволяет уменьшить нагрузку на память и сделать эксперименты воспроизводимыми в ноутбуках.  
- Ноутбук сравнения следует рассматривать как основной сводный файл проекта.  
