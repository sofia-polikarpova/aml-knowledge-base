## DGFraud-T2: Графовая нейронная сеть для обнаружения мошенничества

## Архитектура модели

### Основные компоненты
```python
class DGFraudT2:
    def __init__(self):
        self.graph_builder = HeterogeneousGraphBuilder()
        self.meta_paths = predefined_meta_paths
        self.attention_mechanism = DualAttention()
        self.classifier = MLPClassifier()
```

### Механизм Dual Attention
1. **Node-level Attention** - взвешивание важности соседей
2. **Meta-path-level Attention** - взвешивание важности мета-путей

Подробная работа механизма: [[04 Dual Attention в графовых нейронных сетях]].

### Процесс обучения
```
Сырые данные → Построение графа → Сбор информации по мета-путям → 
Attention агрегация → Классификация
```

**Требования к данным для GNN и Attention-моделей в AML-задаче**

Данная заметка описывает требования к данным для обучения графовых нейронных сетей (GNN) с механизмами attention (GAT, Dual Attention, HAN, SemiGNN) в рамках AML-задачи анализа блокчейн-транзакций.

Ключевая идея: **модели не обучаются на сырых транзакциях**, а используют граф и агрегированные признаки узлов и рёбер, из которых формируется «важность» (attention).

  

**Исходные транзакционные данные (сырьё)**

Используются для построения графа и вычисления признаков.

**Непосредственно в модель не подаются.**

**Обязательные поля**

```python
required_transaction_fields = [

    'transaction_hash',        # Уникальный ID транзакции
    'from_address',            # Адрес отправителя (узел-источник)
    'to_address',              # Адрес получателя (узел-назначение)
    'amount',                  # Сумма транзакции
    'timestamp',               # Временная метка
    'is_contract_interaction'  # Флаг взаимодействия с контрактом
] 
```

**Дополнительные поля (рекомендуемые)**

```python
recommended_transaction_fields = [

    'gas_used',        # Использованный gas
    'gas_price',       # Цена gas
    'transaction_fee', # Комиссия транзакции
    'block_number'     # Номер блока
]
```  

**Признаки узлов (Node Features)**

Формируются путём агрегации транзакций для каждого адреса.

**Используются для node-level attention.**

```python
node_features = [

    # Финансовые признаки
    'current_balance',         # Текущий баланс адреса
    'total_incoming_volume',   # Суммарный входящий объём
    'total_outgoing_volume',   # Суммарный исходящий объём

    # Поведенческие признаки
    'num_incoming_txs',        # Количество входящих транзакций
    'num_outgoing_txs',        # Количество исходящих транзакций
    'avg_transaction_amount',  # Средняя сумма транзакции 
    'in_out_ratio',            # Отношение входящих к исходящим

    # Временные признаки
    'address_lifetime',        # Время жизни адреса
    'avg_time_between_txs',    # Средний интервал между транзакциями

    # Семантические признаки
    'is_contract',             # Контракт / EOA
    'entity_type'              # Тип сущности (CEX, DEX, Mixer, User, Unknown)
]
```

Если набор node features ограничен, attention-механизм не способен корректно формировать важность узлов.

**Признаки рёбер (Edge Features)**

Описывают характер взаимодействия между двумя узлами.

**Используются для edge-level (relation) attention.**

```python
edge_features = [

    'amount',                 # Сумма транзакции
    'tx_count',               # Количество транзакций между узлами
    'time_delta',             # Временной интервал между транзакциями
    'direction',              # Направление перевода
    'interaction_type'        # Тип взаимодействия (transfer, swap, deposit и т.д.)
]
```

**Использование признаков в модели**

```python
attention_inputs = {

    'node_level_attention': 'node_features',
    'edge_level_attention': 'edge_features'

}
```

Механизм attention не задаёт «важность» заранее, а обучается выделять значимые узлы и связи **исключительно на основе предоставленных признаков**.

### Формат данных
```csv
transaction_hash,from_address,to_address,amount,timestamp,is_contract
0xabc...,0x123...,0x456...,1.5,1678901234,false
0xdef...,0x456...,0x789...,2.0,1678901267,true
```
## Вывод

Сырые транзакции являются лишь источником данных.

Реальное обучение GNN происходит на агрегированных node и edge features.

Качество, полнота и семантическая насыщенность признаков напрямую определяют интерпретируемость и эффективность attention.
## Мета-пути для блокчейн-анализа

### Базовые мета-пути
1. **Прямые переводы**
   ```
   Wallet → Transaction → Wallet
   ```

2. **Через смарт-контракты**
   ```
   Wallet → Transaction → Contract → Transaction → Wallet
   ```

3. **Транзакционные цепочки**
   ```
   Wallet → Transaction → Wallet → Transaction → Wallet
   ```

### Специализированные мета-пути для AML
4. **Кольцевые переводы**
   ```
   Wallet_A → Wallet_B → Wallet_C → Wallet_A
   ```

5. **Быстрые последовательные транзакции**
   ```
   Wallet → Transaction₁ → Wallet → Transaction₂ → Wallet
   ```

## Технические характеристики

### Вычислительные требования
```yaml
Минимальные:
  RAM: 16 GB
  GPU: NVIDIA GTX 1080 (8GB)
  Storage: 50 GB

Рекомендуемые:
  RAM: 32+ GB  
  GPU: NVIDIA RTX 3080 (12GB)
  Storage: 100+ GB
```

### Производительность
- **Время обучения:** 2-6 часов 
- **Инференс:** 50-100 мс на транзакцию
- **Масштабируемость:** до 1M+ узлов в графе

##  Адаптация для блокчейн-данных

## Ожидаемые результаты

### Метрики качества
- **Precision:** > 90%
- **Recall:** > 85% 
- **F1-Score:** > 87%

### Преимущества для диплома
- Обнаружение сложных мошеннических схем
- Адаптивность к новым типам атак
- Автоматическое обучение признаков
- Интерпретируемость результатов

## Реализация

### Используемые библиотеки
```python
import torch
import dgl
import numpy as np
from dgfraud import DGFraudT2
```

### Пример использования
```python
# Инициализация модели
model = DGFraudT2(meta_paths=blockchain_meta_paths)

# Обучение
model.fit(train_graph, labels)

# Предсказание
predictions = model.predict(test_graph)
```

## Ссылки и ресурсы

### Официальные ресурсы
- [GitHub репозиторий DGFraud](https://github.com/safe-graph/DGFraud)

### Связанные заметки
- [[02-models/README|Модели]] - Обзор моделей
- [[Money Laundering Detection]] - Сравнение с другой моделью
- [[03-data/README|Данные]] - Подготовка данных для модели
- [[04-code/README|Код]] - Тестирование модели

---
