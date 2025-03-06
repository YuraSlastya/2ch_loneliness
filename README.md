# 2ch_loneliness
Взаимосвязь феномена одиночества и принадлежности к субкультуре анонимных имиджборд на примере пользователей сайта 2ch.hk

Чтобы просмотреть устройство кода и все таблицы с графиками, просто откройте файл 2ch_loneliness.ipynb.

А для собственноручного запуска необходимо, чтобы файл с кодом и данные об ответах респондентов находились в одной папке.

import csv
import random
import itertools

def generate_csv(filename, num_rows, num_cols, chunk_size=100_000):
    """Генерация CSV-файла построчно без загрузки в память"""
    headers = [f"column_{i}" for i in range(num_cols)]
    
    def random_row():
        return [random.randint(0, 1000000) for _ in range(num_cols)]
    
    with open(filename, "w", newline="") as f:
        writer = csv.writer(f)
        writer.writerow(headers)  # Записываем заголовки

        for _ in range(0, num_rows, chunk_size):
            chunk = (random_row() for _ in range(min(chunk_size, num_rows)))
            writer.writerows(chunk)  # Записываем чанками

# Пример использования: 10 млн строк, 10 столбцов
generate_csv("big_data.csv", num_rows=10_000_000, num_cols=10)
