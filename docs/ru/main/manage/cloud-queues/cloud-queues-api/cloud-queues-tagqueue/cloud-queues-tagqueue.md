Добавьте теги распределения затрат в указанную очередь VK Cloud  SQS.

При использовании тегов очереди учитывайте следующие рекомендации:

- Не рекомендуется добавлять в очередь более 50 тегов.
- Теги не имеют семантического значения. VK Cloud  SQS интерпретирует теги как символьные строки.
- Теги чувствительны к регистру.
- Новый тег с ключом, идентичным ключу существующего тега, перезаписывает существующий тег.

## Параметры запроса

QueueUrl

URL-адрес очереди.

Тип: Строка

Обязательно: Да

Тег

Tag.N.Key (ключ)

Tag.N.Value (значение)

Список тегов, которые нужно добавить в указанную очередь.

Тип: строка для сопоставления строк

Обязательно: Да

## Примеры

Этот пример иллюстрирует одно использование TagQueue.

#### Запрос образца

```
https://sqs.ru-east-2.mcs.mail.ru/123456789012/MyQueue/
?Action=TagQueue
&Tag.Key=QueueType
&Tag.Value=Production
&Expires=2020-10-18T22:52:43PST
&Version=2012-11-05
&AUTHPARAMS
```

#### Образец ответа

```
<TagQueueResponse>
   <ResponseMetadata>
      <RequestId>a1b2c3d4-e567-8901-23f4-g5678901hi23</RequestId>
   </ResponseMetadata>
</TagQueueResponse>
```
