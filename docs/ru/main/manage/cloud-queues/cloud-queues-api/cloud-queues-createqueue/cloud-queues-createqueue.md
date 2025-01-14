Запрос создает новую стандартную очередь или очередь FIFO. В запросе можно передать один или несколько атрибутов.

## Параметры запроса

**Атрибут**

Attribute.N.Name (ключ)

Attribute.N.Value (значение)

Карта атрибутов с соответствующими значениями.

Ниже перечислены имена, описания и значения специальных параметров запроса, которые `CreateQueue`использует действие:

- `DelaySeconds`\- Время в секундах, на которое задерживается доставка всех сообщений в очереди. Допустимые значения: целое число от 0 до 900 секунд (15 минут). По умолчанию: 0.
- `MaximumMessageSize`\- Максимальное количество байтов, которое может содержать сообщение, прежде чем VK Cloud SQS отклонит его. Допустимые значения: целое число от 1024 байтов (1 КиБ) до 262 144 байта (256 КиБ). По умолчанию: 262144 (256 КБ).
- `MessageRetentionPeriod`\- Продолжительность времени в секундах, в течение которого VK Cloud SQS сохраняет сообщение. Допустимые значения: целое число от 60 секунд (1 минута) до 1 209 600 секунд (14 дней). По умолчанию: 345 600 (4 дня).
- `Policy`\- Политика очереди.
- `ReceiveMessageWaitTimeSeconds`\- Время в секундах, в течение которого действие ожидает прибытия сообщения. Допустимые значения: целое число от 0 до 20 (секунд). По умолчанию: 0. `ReceiveMessage`
- `RedrivePolicy`\- Строка, которая включает параметры для функции очереди недоставленных сообщений исходной очереди в виде объекта JSON.

  - `deadLetterTargetArn`\- Имя ресурса VK Cloud (ARN) очереди недоставленных сообщений, в которую VK Cloud SQS перемещает сообщения после `maxReceiveCount`превышения значения.
  - `maxReceiveCount`\- Сколько раз сообщение доставлялось в исходную очередь до того, как оно было перемещено в очередь недоставленных сообщений. Когда `ReceiveCount`для сообщения превышает значение `maxReceiveCount`для очереди, VK Cloud SQS перемещает сообщение в очередь недоставленных сообщений.

- `VisibilityTimeout`\- Тайм-аут видимости очереди в секундах. Допустимые значения: целое число от 0 до 43 200 (12 часов). По умолчанию: 30.

Следующие атрибуты применяются только к шифрованию на стороне сервера :

- `KmsMasterKeyId`\- Идентификатор управляемого VK Cloud главного ключа клиента (CMK) для VK Cloud SQS или настраиваемого CMK.[](https://docs.aws.amazon.com/kms/latest/APIReference/API_DescribeKey.html#API_DescribeKey_RequestParameters)
- `KmsDataKeyReusePeriodSeconds`\- Время в секундах, в течение которого VK Cloud SQS может повторно использовать ключ данных для шифрования или расшифровки сообщений перед повторным вызовом VK Cloud KMS. Целое число, представляющее секунды, от 60 секунд (1 минута) до 86 400 секунд (24 часа). По умолчанию: 300 (5 минут). Более короткий период времени обеспечивает лучшую безопасность, но приводит к большему количеству обращений к KMS, за которые может взиматься плата после уровня бесплатного пользования.

Следующие атрибуты применяются только к очередям FIFO (first-in-first-out) :

- `FifoQueue`\- Обозначает очередь как FIFO. Допустимые значения: `true`и `false`. Если вы не укажете `FifoQueue`атрибут, VK Cloud SQS создаст стандартную очередь. Вы можете указать этот атрибут только во время создания очереди. Вы не можете изменить его для существующей очереди. Когда вы устанавливаете этот атрибут, вы также должны `MessageGroupId`явно указать для своих сообщений.
- `ContentBasedDeduplication`\- Включает дедупликацию на основе содержимого. Допустимые значения: `true`и `false`. Обратите внимание на следующее:

  - Каждое сообщение должно иметь уникальный `MessageDeduplicationId`.

    - Вы можете `MessageDeduplicationId`явно указать.
    - Если вы не можете предоставить `MessageDeduplicationId`и включить `ContentBasedDeduplication`для своей очереди, VK Cloud SQS использует хэш SHA-256 для генерации с `MessageDeduplicationId`использованием тела сообщения (но не атрибутов сообщения).
    - Если вы не предоставите `MessageDeduplicationId`и очередь не `ContentBasedDeduplication`установлена, действие завершится ошибкой.
    - Если очередь `ContentBasedDeduplication`установлена, вы `MessageDeduplicationId`отменяете сгенерированную.

  - Когда `ContentBasedDeduplication`действует, сообщения с идентичным содержимым, отправленные в течение интервала дедупликации, обрабатываются как дубликаты, и доставляется только одна копия сообщения.
  - Если вы отправляете одно сообщение с `ContentBasedDeduplication`включенным, а затем другое сообщение с таким `MessageDeduplicationId`же, как и сообщение, созданное для первого `MessageDeduplicationId`, два сообщения рассматриваются как дубликаты, и доставляется только одна копия сообщения.

## Элементы ответа

Служба возвращает следующий элемент.

**QueueUrl**

URL-адрес созданной очереди VK Cloud SQS.

Тип: Строка

## Ошибки

**AWS.SimpleQueueService.QueueDeletedRecently**

Вы должны подождать 60 секунд после удаления очереди, прежде чем вы сможете создать другую очередь с тем же именем.

Код состояния HTTP: 400

**QueueAlreadyExists**

Очередь с таким названием уже существует. VK Cloud SQS возвращает эту ошибку, только если запрос включает атрибуты, значения которых отличаются от значений существующей очереди.

Код состояния HTTP: 400

## Примеры

В следующем примере запроса создается новая очередь с именем `MyQueue`. Структура `AUTHPARAMS`зависит от подписи запроса API.

#### Образец запроса

```
https://sqs.ru-east-2.mcs.mail.ru/
?Action=CreateQueue
&QueueName=MyQueue
&Tag.Key=QueueType
&Tag.Value=Production
&Attribute.1.Name=VisibilityTimeout
&Attribute.1.Value=40
&Expires=2020-10-18T22:52:43PST
&Version=2012-11-05
&AUTHPARAMS
```

#### Образец ответа

```
<CreateQueueResponse>
    <CreateQueueResult>
        <QueueUrl>https://queue.mcs.mail.ru/123456789012/MyQueue</QueueUrl>
    </CreateQueueResult>
    <ResponseMetadata>
        <RequestId>7a62c49f-347e-4fc4-9331-6e8e7a96aa73</RequestId>
    </ResponseMetadata>
</CreateQueueResponse>
```

В следующем примере создается очередь задержки, которая скрывает каждое сообщение от потребителей в течение первых 45 секунд (пока сообщение находится в очереди), путем вызова действия CreateQueue с атрибутом DelaySeconds, установленным на 45 секунд.

### Важно

URL-адреса и имена очередей чувствительны к регистру.

#### Образец запроса

```
https://sqs.us-east-2.mcs.mail.ru/123456789012/MyQueue/
?Action=CreateQueue
&QueueName=MyQueue
&Attribute.1.Name=DelaySeconds
&Attribute.1.Value=45
&Expires=2020-12-20T22:52:43PST
&Version=2012-11-05
&AUTHPARAMS
```
