# Лабораторная работа 1. Кто снизил активность и почему

Автор: Бузычков Никита Фёдорович.

## Файлы

| файл | что это |
|---|---|
| `01_analysis.ipynb` | рабочий ноутбук: загрузка сырых данных, аудит, препроцессинг, исследование, метрика активности, группы |
| `02_report.ipynb` | отчёт: читает файлы, сохранённые первым ноутбуком, строит итоговые графики и таблицы |
| `report.pdf` | собранный отчёт |
| `cleaning_log.csv` | журнал изменений данных, одна строка на решение |
| `campaign_list.csv` | итоговый список кампании: `client_id` и `group` |

Сырые данные в репозиторий не входят.

## Как запустить

1. Положите выданные файлы `clients.csv` и `transactions.csv` в папку `data/S03/` рядом с ноутбуками. Если они лежат в другом месте, поменяйте пути в первой ячейке кода `01_analysis.ipynb`, в константах `RAW_CLIENTS` и `RAW_TXN`:
   ```python
   RAW_CLIENTS = "data/S03/clients.csv"
   RAW_TXN = "data/S03/transactions.csv"
   ```
   
2. Установите библиотеки. `pyarrow` нужен для чтения и записи parquet:
   ```
   pip install pandas numpy matplotlib seaborn pyarrow jupyterlab "nbconvert[webpdf]"
   ```
3. Выполните рабочий ноутбук (около минуты). Он сохранит рядом с собой `clean_data.parquet`, `clients_clean.parquet`, `client_metrics.parquet`, `cleaning_log.csv` и `campaign_list.csv`:
   ```
   jupyter nbconvert --to notebook --execute --inplace 01_analysis.ipynb
   ```
4. Выполните отчёт. Он читает файлы из шага 3, поэтому запускается после рабочего ноутбука:
   ```
   jupyter nbconvert --to notebook --execute --inplace 02_report.ipynb
   ```
5. Соберите PDF командой из задания:
   ```
   jupyter nbconvert --to webpdf --no-input --execute 02_report.ipynb --output report.pdf
   ```
   Если nbconvert сообщит, что не найден Chromium, добавьте к команде `--allow-chromium-download`.

## Версии, на которых проверен запуск

Python 3.13.2, pandas 3.1.1, numpy 2.5.4, matplotlib 3.11.2, seaborn 0.13.2, pyarrow 26.0.1, nbconvert 7.17.2.
