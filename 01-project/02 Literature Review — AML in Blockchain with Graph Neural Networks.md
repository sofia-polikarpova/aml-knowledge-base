Этот файл является центральным обзором литературы, используемой в дипломной работе. Он агрегирует все ключевые источники, на которые опирается теоретическая и практическая часть исследования, и служит точкой входа в базу знаний.

**1. Общая постановка задачи AML в блокчейне**

Weber et al., **"Anti-Money Laundering in Bitcoin: Experimenting with Graph Convolutional Networks"** https://arxiv.org/abs/1908.02591 Классическая работа по применению графовых моделей для AML в блокчейне. Используется для понимания базовых признаков, построения графа и ограничений Bitcoin-подобных датасетов.

Elliptic Dataset (AML Bitcoin Dataset) https://www.kaggle.com/ellipticco/elliptic-data-set Публичный размеченный датасет для задачи выявления illicit-активности. Используется как sandbox для первых экспериментов и анализа GNN.

**2. Graph Neural Networks: базовые модели**

Kipf, Welling, **"Semi-Supervised Classification with Graph Convolutional Networks"** https://arxiv.org/abs/1609.02907 Базовая архитектура GCN, лежащая в основе большинства последующих GNN-моделей.

Hamilton et al., **"Inductive Representation Learning on Large Graphs (GraphSAGE)"** https://arxiv.org/abs/1706.02216 Индуктивный подход, важный для задач с динамическими графами и near-real-time inference.

**3. Attention-механизмы в графах**

Veličković et al., **"Graph Attention Networks"** https://arxiv.org/abs/1710.10903 Вводит node-level attention в графах. Базовая статья для понимания GAT.

Vaswani et al., **"Attention Is All You Need"** https://arxiv.org/abs/1706.03762 Общая формализация attention (query, key, value), используемая при интерпретации attention в GNN.

**4. Heterogeneous и Multi-view графы**

Wang et al., **"Heterogeneous Graph Attention Network (HAN)"** https://arxiv.org/abs/1903.07293 Работа с графами, содержащими разные типы узлов и рёбер. Важна для учёта различного «веса» узлов (CEX, DEX, mixer).

Chen et al., **"EvolveGCN"** https://arxiv.org/abs/1902.10191 Temporal GNN для динамических графов. Используется для понимания multi-view и временных аспектов.

**5. Semi-supervised и Dual Attention подходы**

Liu et al., **"A Semi-supervised Graph Attentive Network for Financial Fraud Detection"** https://arxiv.org/abs/2003.01171 Основная архитектура, рассматриваемая в дипломной работе. Вводит multi-view представление и Dual Attention (node-level + edge-level).

Wu et al., **"A Comprehensive Survey on Graph Neural Networks"** https://arxiv.org/abs/1901.00596 Обзор существующих GNN-архитектур, включая attention-механизмы.

**6. Практические реализации и репозитории**

DGFraud-TF2 GitHub Repository https://github.com/safe-graph/DGFraud-TF2 Реализация SemiGNN и связанных алгоритмов. Используется как основа практической части диплома.

SemiGNN implementation (DGFraud-TF2) https://github.com/safe-graph/DGFraud-TF2/tree/main/algorithms/SemiGNN Исходный код SemiGNN для анализа и адаптации под блокчейн-задачу.

Kaggle Notebook: Transfer Learning / EvolveGCN for AML https://www.kaggle.com/code/diyang/transfer-learning-evolve-gcn-for-aml Пример практического применения temporal GNN для AML.

**7. Ethereum и смарт-контракты**

Ethereum Yellow Paper https://ethereum.github.io/yellowpaper/paper.pdf Формальное описание Ethereum-протокола.

ERC-20 Token Standard (EIP-20) https://eips.ethereum.org/EIPS/eip-20 Стандарт взаимодействия с не-нативными токенами.

Ethereum Fraud Detection Dataset https://www.kaggle.com/datasets/vagifa/ethereum-frauddetection-dataset Пример признаков адресов и транзакций в Ethereum.

**8. Связь с остальными заметками**

[[01 Project Overview]]
[[05 Graph Attention Network (GAT)]]
[[07 SemiGNN для задачи AML в блокчейне]]
[[08 DGFraud-T2 algorithms overview]]
[[09 Универсальный набор признаков для AML‑анализа в разных блокчейнах]]
[[11 Набор признаков для графовой нейросети AML на Ethereum]]
[[04 Dual Attention в графовых нейронных сетях]]
