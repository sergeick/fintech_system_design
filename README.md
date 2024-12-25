# Fintech Highload Microservice Architecture на Golang

## Описание Проекта

Этот проект представляет собой высоконагруженную финансовую систему, разработанную на основе микросервисной архитектуры с использованием Golang. Система предназначена для обработки финансовых транзакций в реальном времени, интеграции с платежными шлюзами, управления уведомлениями, а также предоставления аналитики и финансовой отчетности. Особое внимание уделено соответствию стандартам безопасности финансового сектора.

## Основные Возможности

- **Обработка Транзакций в Реальном Времени**: Обеспечивает быстрые и надежные финансовые операции.
- **Интеграция с Платежными Шлюзами**: Поддержка различных платежных систем для удобства пользователей.
- **Система Уведомлений**: Оповещения пользователей о статусе транзакций и других важных событиях.
- **Аналитика и Отчетность**: В режиме реального времени предоставляет финансовую аналитику и отчеты.
- **Безопасность**: Соответствие строгим стандартам безопасности финансового сектора.

## Архитектура Системы

![Architecture](./docs/diagrams/1_ architecture_map.png)
![API MAP](./docs/diagrams/2_api_endpoint_map.png)
![Client MAP](./docs/diagrams/3_client_map.png)
![Transaction MAP](./docs/diagrams/4_transaction_map.png)
![Deploy_MAP](./docs/diagrams/5_deploy_map.png)

Проект основан на микросервисной архитектуре, что обеспечивает масштабируемость и гибкость системы. Каждый сервис отвечает за свою конкретную функциональность, что позволяет легко добавлять новые возможности и поддерживать существующие.

## Микросервисы и Технологии

### Сервис Аутентификации
- **Язык**: Golang
- **Базы Данных**: PostgreSQL, Redis
- **Аутентификация**: JWT/OAuth 2.0
- **Безопасность**: bcrypt, SecureCookie

### Сервис Транзакций
- **Язык**: Golang
- **Базы Данных**: PostgreSQL
- **Сообщения**: Kafka (Sarama)
- **Интеграция**: Stripe API
- **Финансы**: decimal, go-money

### Сервис Уведомлений
- **Язык**: Golang
- **Кэширование**: Redis
- **Сообщения**: Kafka
- **Уведомления**: AWS SES/SNS
- **Логирование**: zap logger

### Сервис Профилей
- **Язык**: Golang
- **Базы Данных**: PostgreSQL (gorm), Redis
- **Тестирование**: testify

## Хранение Данных

- **PostgreSQL**: Для хранения транзакций, пользователей и финансовых данных с использованием ORM gorm.
- **Redis**: Для кэширования, управления сессиями и хранения временных данных с использованием go-redis.
- **S3**: Для хранения документов, отчетов и логов с использованием aws-sdk-go.
- **Kafka**: Для организации очередей сообщений и событийной архитектуры с использованием Sarama, AKHQ и Kafdrop.

## Инфраструктура и Инструменты

- **Облако и Контейнеризация**: AWS (ECS/EKS/RDS/S3/CloudWatch/Route53), Kubernetes, Docker Compose.
- **CI/CD и Автоматизация**: Jenkins, GitLab CI, Terraform, consul-api.
- **Мониторинг**: Prometheus (client_golang), Grafana, OpenTelemetry, X-Ray.
- **API Gateway**: Kong, gin-gonic/gin, go-kit, gRPC, protobuf.
- **Безопасность**: JWT, OAuth 2.0, SSL/TLS, Rate Limiting, viper.

## Обоснование Выбора Инструментов и Архитектуры

### Почему Микросервисная Архитектура?

Микросервисная архитектура предоставляет гибкость при масштабировании отдельных компонентов системы без необходимости масштабировать всю систему целиком. Это особенно важно для высоконагруженных приложений, где разные сервисы могут иметь различные требования к ресурсам и нагрузке. Также микросервисы облегчают независимую разработку, тестирование и развертывание, что ускоряет процесс разработки и улучшает стабильность системы.

### Выбор Golang

Golang выбран из-за его высокой производительности, поддержки параллелизма и эффективного использования ресурсов. Он отлично подходит для разработки микросервисов, требующих обработки большого количества запросов с минимальной задержкой. Кроме того, богатая стандартная библиотека и активное сообщество делают Golang идеальным выбором для разработки надежных и масштабируемых сервисов.

#### Сравнение Golang с Другими Языками

| Язык       | Производительность | Поддержка Параллелизма | Сообщество | Простота Разработки |
|------------|---------------------|------------------------|------------|---------------------|
| **Golang** | Высокая             | Отличная               | Активное    | Прост в изучении    |
| **Java**   | Высокая             | Хорошая                | Большое     | Сложнее             |
| **Node.js**| Средняя             | Ограниченная           | Большое     | Очень просто        |
| **Python** | Ниже                | Ограниченная            | Очень большое | Очень просто     |

**Почему Golang?** В сравнении с Java и Python, Golang обеспечивает лучшую производительность и эффективность использования ресурсов, что критично для высоконагруженных систем. В отличие от Node.js, который основан на однопоточном модели, Golang предлагает превосходную поддержку параллелизма, что позволяет эффективно обрабатывать множество одновременных запросов.

### Почему PostgreSQL и Redis?

**PostgreSQL** выбран как основная реляционная база данных благодаря своей стабильности, мощным возможностям обработки данных и поддержке сложных запросов. Он идеально подходит для хранения критически важных данных, таких как транзакции и информация о пользователях.

**Redis** используется для кэширования и управления сессиями, что значительно повышает производительность системы за счет сокращения времени доступа к часто используемым данным. Его поддержка структур данных в памяти обеспечивает быстрый доступ и манипуляцию данными.

#### Сравнение PostgreSQL и Альтернатив

| База Данных | Производительность | Масштабируемость | Поддержка ACID | Сообщество | Легкость Настройки |
|-------------|---------------------|-------------------|----------------|------------|--------------------|
| **PostgreSQL** | Высокая             | Хорошая           | Да             | Активное    | Средняя            |
| **MySQL**      | Высокая             | Хорошая           | Частично       | Очень активное | Легче              |
| **MongoDB**    | Средняя             | Отличная          | Нет            | Очень активное | Средняя            |

**Почему PostgreSQL?** Хотя MySQL проще в настройке и также предлагает высокую производительность, PostgreSQL предоставляет более продвинутые возможности для обработки данных и гарантирует полное соответствие ACID, что критично для финансовых приложений. В отличие от MongoDB, PostgreSQL лучше подходит для систем, требующих сложных транзакций и целостности данных.

### Использование Kafka для Сообщений

Kafka выбран для реализации очередей сообщений и событийной архитектуры из-за его высокой пропускной способности, надежности и способности обрабатывать большие объемы данных в реальном времени. Это позволяет эффективно организовать взаимодействие между микросервисами и обеспечивает надежную доставку сообщений.

#### Сравнение Kafka с Другими Системами Сообщений

| Система Сообщений | Пропускная Способность | Надежность | Легкость Интеграции | Сообщество |
|-------------------|-------------------------|------------|---------------------|------------|
| **Kafka**         | Очень высокая           | Высокая    | Хорошая             | Большое    |
| **RabbitMQ**      | Средняя                 | Высокая    | Очень хорошая       | Большое    |
| **Apache Pulsar** | Высокая                 | Высокая    | Хорошая             | Растущее   |

**Почему Kafka?** В отличие от RabbitMQ, который лучше подходит для задач с меньшей пропускной способностью, Kafka обеспечивает значительно более высокую пропускную способность и масштабируемость. Apache Pulsar является перспективной альтернативой, но Kafka уже имеет более зрелую экосистему и лучшее сообщество поддержки.

### Инфраструктура на AWS с Kubernetes

Использование облачных сервисов AWS в сочетании с Kubernetes обеспечивает масштабируемость и гибкость инфраструктуры. Kubernetes позволяет автоматизировать развертывание, масштабирование и управление контейнерами, что упрощает эксплуатацию и повышает устойчивость системы. AWS предоставляет надежные и масштабируемые сервисы, необходимые для работы высоконагруженных приложений.

#### Сравнение Kubernetes на AWS с Другими Облачными Платформами

| Облачная Платформа | Поддержка Kubernetes | Интеграция с Сервисами | Масштабируемость | Стоимость    |
|--------------------|----------------------|------------------------|-------------------|--------------|
| **AWS EKS**        | Отличная             | Широкая                | Высокая           | Высокая      |
| **GCP GKE**        | Отличная             | Широкая                | Высокая           | Средняя      |
| **Azure AKS**      | Отличная             | Широкая                | Высокая           | Средняя      |

**Почему AWS EKS?** Хотя GKE и AKS предлагают схожие возможности, AWS EKS обеспечивает лучшую интеграцию с другими сервисами AWS, такими как RDS, S3 и Route53, что делает его более предпочтительным выбором для комплексных высоконагруженных систем. Кроме того, AWS обладает более глобальной инфраструктурой, что способствует улучшенной доступности и отказоустойчивости.

### CI/CD и Автоматизация с Jenkins и Terraform

Jenkins и GitLab CI используются для организации непрерывной интеграции и доставки, что обеспечивает быстрое и надежное развертывание изменений в коде. Terraform выбран для управления инфраструктурой как кодом, что позволяет легко воспроизводить окружение и управлять изменениями инфраструктуры.

#### Сравнение Jenkins и GitLab CI с Другими CI/CD Инструментами

| CI/CD Инструмент | Гибкость | Поддержка Плагинов | Простота Использования | Сообщество |
|------------------|----------|--------------------|------------------------|------------|
| **Jenkins**      | Очень высокая | Огромное              | Сложнее                | Большое    |
| **GitLab CI**    | Высокая     | Хорошая               | Простой                | Большое    |
| **CircleCI**     | Высокая     | Средняя               | Очень простой          | Большое    |
| **Travis CI**    | Средняя     | Средняя               | Простой                | Большое    |

**Почему Jenkins и Terraform?** Jenkins предлагает непревзойденную гибкость и огромный выбор плагинов, что делает его идеальным для сложных CI/CD процессов. GitLab CI интегрируется непосредственно с репозиториями кода, упрощая процесс развертывания. Terraform, в свою очередь, обеспечивает мощное управление инфраструктурой как кодом, поддерживая множество провайдеров и позволяя легко масштабировать и изменять инфраструктуру.

### Мониторинг и Безопасность

Prometheus и Grafana используются для мониторинга производительности системы и визуализации метрик, что позволяет своевременно обнаруживать и реагировать на возможные проблемы. OpenTelemetry и AWS X-Ray обеспечивают детальное отслеживание запросов и диагностику производительности микросервисов. Безопасность реализована через JWT, OAuth 2.0, SSL/TLS и другие инструменты, что обеспечивает защиту данных и соответствие стандартам финансового сектора.

#### Сравнение Prometheus и Grafana с Другими Инструментами Мониторинга

| Инструмент Мониторинга | Производительность | Гибкость | Простота Настройки | Сообщество |
|------------------------|---------------------|----------|--------------------|------------|
| **Prometheus**         | Высокая             | Отличная | Средняя            | Большое    |
| **Grafana**            | Высокая             | Отличная | Простая            | Большое    |
| **Datadog**            | Высокая             | Высокая  | Очень простая      | Большое    |
| **New Relic**          | Высокая             | Высокая  | Очень простая      | Большое    |

**Почему Prometheus и Grafana?** В отличие от коммерческих решений вроде Datadog и New Relic, Prometheus и Grafana являются открытыми и гибкими инструментами, которые можно настраивать под конкретные нужды проекта без дополнительных затрат. Они хорошо интегрируются с Kubernetes и другими компонентами системы, предоставляя мощные возможности для мониторинга и визуализации.

## Заключение

Выбор микросервисной архитектуры и используемых технологий обоснован необходимостью создания масштабируемой, надежной и производительной системы, способной обрабатывать высокие нагрузки и обеспечивать безопасность данных. Использование Golang, PostgreSQL, Redis, Kafka и современных облачных инструментов позволяет достичь высоких стандартов качества и соответствовать требованиям современного финансового сектора.

## Контакты

Если у вас есть вопросы или предложения, пожалуйста, свяжитесь со мной Telegram @sergei_x100
