# NLP

В задании на NLP треке нужно будет научиться делать комментарии менее токсичными.

Токсичность комментариев мы определяем с помощью нейросети. Пример загрузки модели в коде:
```
from transformers import AutoTokenizer, AutoModelForSequenceClassification
  
tokenizer = AutoTokenizer.from_pretrained("trained_roberta/")

model = AutoModelForSequenceClassification.from_pretrained("trained_roberta/")
```
\*для работы кода надо скачать и разархивировать модель (см. секцию [Загрузки](#загрузки)) и установить необходимые библиотеки

Модель получена дообучением многоязыковой RoBERTa: [исходная модель](https://huggingface.co/unitary/multilingual-toxic-xlm-roberta)

## Оценка качества
Для каждого исправленного комментария мы будем вычислять и усреднять следущую метрику:
* если сеть считает комментарий токсичным (вероятность больше 0.5), 0
* если сеть не считает комментарий токсичным, вычисляется близость исходного и измененного предложения (подробнее описано в [evaluation.pdf](./evaluation.pdf) )

Проверять исправленные комментарии мы будем скриптом [score.py](./score.py)

Пример команды запуска:
```
python3.7 score.py original.txt detoxified.txt --embeddings embeddings_with_lemmas.npz --model ./trained_roberta/ --score - 
```
\*для работы кода надо скачать и разархивировать модель и предобработанные эмбеддинги (см. секцию [Загрузки](#загрузки)) и установить необходимые библиотеки

## Загрузки
Модель и предобработанные эмбеддинги: [ссылка](https://disk.yandex.ru/d/9fAiLtgX-rMjtQ)

## Бейзлайны
Мы подготовили бейзлайны:
* [бейзлайн](./offline_baseline.ipynb) для оффлайн задачи
* [бейзлайн](./online_baseline) для онлайн задачи
