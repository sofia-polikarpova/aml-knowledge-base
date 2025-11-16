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

### Процесс обучения
```
Сырые данные → Построение графа → Сбор информации по мета-путям → 
Attention агрегация → Классификация
```

## Требования к данным

### Обязательные поля
```python
required_fields = [
    'transaction_hash',    # Уникальный ID транзакции
    'from_address',        # Адрес отправителя
    'to_address',          # Адрес получателя
    'amount',              # Сумма транзакции
    'timestamp',           # Временная метка
    'is_contract_interaction' # Флаг вызова контракта
]
```

### Дополнительные поля (рекомендуемые)
```python
recommended_fields = [
    'gas_used',           # Использованный газ
    'gas_price',          # Цена газа
    'block_number',       # Номер блока
    'transaction_fee'     # Комиссия транзакции
]
```

### Формат данных
```csv
transaction_hash,from_address,to_address,amount,timestamp,is_contract
0xabc...,0x123...,0x456...,1.5,1678901234,false
0xdef...,0x456...,0x789...,2.0,1678901267,true
```

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
