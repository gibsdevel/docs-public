## Структура конфигурации Terraform

Конфигурация Terraform состоит из файлов с расширением ".tf", в которых описываются настройки провайдеров, ресурсы, запрашиваются и выводятся данные. 

Обычно под каждый проект создается отдельный рабочий каталог/папка, в который добавляются файлы с описанием конфигурации инфраструктуры. Для удобвства файлы разделяют по типам ресурсов:
- `main.tf` - содержит настройки необходимых провайдеров Terraform
- `variables.tf` - переменные, которые используются в конфигурации. Вынесение часто изменяемых параметров в переменные позволяет легко менять конфигурацию инфраструктуры для нового проекта.
- `network.tf` - описание облачной сети.
- `kubernetes.tf` - описание ресурсов Kubernetes.

Синтаксис языка Terraform состоит из нескольких базовых элементов.

``` bash
resource "mcs_kubernetes_cluster" "mycluster" {
      name = "terracluster"
}

<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}

```

**Блоки (blocks)** являются контейнерами для другого контента и обычно описывают конфигурацию какого-то объекта, например ресурса.
Блоки имею **типы (block type)**, могут иметь **метки (block labels)** и **тело блока (block body)** состоящее из любого количества **аргументов (arguments)** и вложенных блоков.  Аргументы состоят из имени и значения. Они используются внутри блоков.
**Выражения (expressions)** представляют значение либо буквально, либо путем ссылки и объединения других значений. Они отображаются как значения для аргументов или внутри других выражений.

Язык Terraform является декларативным, описывающим намеченную цель, а не шаги по достижению этой цели. Порядок блоков и файлов, в которые они организованы, как правило, не имеют значения; Terraform учитывает только неявные и явные взаимосвязи между ресурсами при определении порядка операций.

Обычно в конфигурации используются:
 - ```terraform и required_providers``` - необходимые для работы Terraform провайдеры. Настройка необходимых провайдеров описана в этой [статье](статья Настройка провайдера terraform для VK CS и OpenStack).
 - ```resource "resource_type" "resource_rame" {}``` - описывает создаваемый [ресурс](https://www.terraform.io/language/resources/syntax), например: сеть, подсеть, кластер Kubernetes или кластер базы данных. 
 - ```data "data_type" "data_name" ```- позволяет использовать [данные](https://www.terraform.io/language/data-sources), указанные вне конфигурации Terraform, которые существуют в облаке или локально. Например: флейвор ВМ, шаблон/версия кластера и тд.
 - ```variable "image_id" {}``` - [входные переменные](https://www.terraform.io/language/values/variables). Используются для вынесения параметров создаваемых ресурсов вне основной конфигурации.
 - ```output "instance_ip_addr" {}``` - [выходные переменные](https://www.terraform.io/language/values/outputs). Выводят данные в коммандную строку.

Для определения последовательности создания ресурсов и их зависимостей используется блок **depends_on**, в котором указывается ресурс от которого зависит создаваемый ресурс.
``` bash
depends_on = [
    mcs_kubernetes_cluster.k8s-cluster,
]
```