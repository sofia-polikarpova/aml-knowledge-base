## Money Laundering Detection: Табличный подход

## Обзор модели

### Основная информация
- **Тип:** Классическая ML модель
- **Данные:** Табличные данные с готовыми признаками
- **Источник:** [Kaggle Dataset - PaySim](https://www.kaggle.com/datasets/ealaxi/paysim1)
- **Применение:** Обнаружение мошенничества в мобильных платежах

##  Признаки модели

### Полный список признаков (11 полей)

| Признак          | Тип         | Описание                      | Применимость к блокчейну |
| ---------------- | ----------- | ----------------------------- | ------------------------ |
| `step`           | int         | Временной шаг (1 шаг = 1 час) | Требует адаптации        |
| `type`           | categorical | Тип операции                  | Аналоги в блокчейне      |
| `amount`         | float       | Сумма транзакции              | Прямая аналогия          |
| `nameOrig`       | string      | ID отправителя                | Адрес кошелька           |
| `oldbalanceOrg`  | float       | Баланс отправителя до         | Доступно в блокчейне     |
| `newbalanceOrig` | float       | Баланс отправителя после      | Доступно в блокчейне     |
| `nameDest`       | string      | ID получателя                 | Адрес кошелька           |
| `oldbalanceDest` | float       | Баланс получателя до          | Доступно в блокчейне     |
| `newbalanceDest` | float       | Баланс получателя после       | Доступно в блокчейне     |
| `isFraud`        | bool        | Целевая переменная            | Аналогичная задача       |
| `isFlaggedFraud` | bool        | Флаг мошенничества            | Правило-based подход     |

## Адаптация для блокчейна

### Прямо применимые признаки
```python
direct_mapping = {
    'type': 'transaction_type',           # Тип транзакции
    'amount': 'value',                    # Сумма
    'nameOrig': 'from_address',           # Отправитель
    'nameDest': 'to_address',             # Получатель
    'isFraud': 'is_suspicious'            # Целевая переменная
}
```

### Требующие адаптации
```python
adaptive_features = {
    'step': 'block_timestamp',           # Временные метки
    'balance_features': 'wallet_balance', # Балансы кошельков
    'isFlaggedFraud': 'custom_rules'      # Кастомные правила
}
```

### Новые признаки для блокчейна
```python
blockchain_specific = {
    'gas_used',           # Использованный газ
    'transaction_fee',    # Комиссия
    'contract_interaction', # Взаимодействие с контрактом
    'transaction_age',     # Возраст кошелька
    'transaction_frequency' # Частота транзакций
}
```

## Техническая реализация

### Алгоритмы машинного обучения
```python
from sklearn.ensemble import RandomForestClassifier
from xgboost import XGBClassifier
from sklearn.svm import SVC

models = {
    'random_forest': RandomForestClassifier(),
    'xgboost': XGBClassifier(),
    'svm': SVC()
}
```

### Пайплайн обработки
```python
pipeline = Pipeline([
    ('preprocessor', DataPreprocessor()),
    ('feature_selector', FeatureSelector()),
    ('classifier', RandomForestClassifier())
])
```

## Сравнительные характеристики

### Преимущества
- Простота реализации
- Быстрое обучение и предсказание
- Хорошая интерпретируемость
- Низкие требования к ресурсам

### Ограничения
- Не учитывает транзакционные связи
- Ограничено для сложных схем мошенничества
- Требует feature engineering
- Менее эффективно для графовых данных

##  Применение в дипломе

### Роль в системе
- **Бейзлайн модель** для сравнения с DGFraud-T2
- **Быстрая проверка** простых случаев мошенничества
- **Дополнительный детектор** в ансамбле моделей

### Ожидаемые результаты
- **Accuracy:** 85-90% на простых случаях
- **Training time:** минуты вместо часов
- **Inference speed:** миллисекунды на транзакцию

##  Реализация

### Пример кода
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Загрузка и подготовка данных
data = pd.read_csv('blockchain_transactions.csv')
X = data[features]
y = data['is_suspicious']

# Обучение модели
X_train, X_test, y_train, y_test = train_test_split(X, y)
model = RandomForestClassifier()
model.fit(X_train, y_train)

# Оценка качества
accuracy = model.score(X_test, y_test)
```

## Ссылки

### Ресурсы
- [Официальный датасет на Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)
- [Документация по признакам](https://www.kaggle.com/datasets/ealaxi/paysim1)

### Связанные заметки
- [[02-models/README|Модели]] - Обзор всех моделей
- [[DGFraud-T2]] - Основная модель для сравнения
- [[03-data/README|Данные]] - Подготовка данных

---
