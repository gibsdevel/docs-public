Новая версия PostgreSQL 13 содержит существенные улучшения систем индексирования и поиска данных, которые полезны при работе с большими БД.

В список улучшений входит:

- Экономия места и прирост производительности индексов. Теперь PostgreSQL 13 может эффективно работать с дублирующимися данными в индексах B-tree. Это снизит количество места при этом улучшит общую производительность запросов.
- Инкрементальная сортировка, при которой уже отсортированные данные из более раннего шага выполнения запроса могут ускорить работу сортировки на более позднем шаге.
- Меньшее время ответа для запросов, которые используют агрегацию и секционирование;
- лучшее планирование запросов при использовании расширенной статистики.
- Оптимизация процессов ежедневного администрирования — удобство работы с управлением данных.
- Параллелизация очистки (vacuuming).

Еще больше о PostgreSQL 13 вы можете прочитать [здесь](https://www.postgresql.org/docs/13/release-13.html).