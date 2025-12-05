# task-manager
# GUESS Accounting System 

**Web-приложение для автоматизации бухгалтерского учета в розничном магазине**  
*Автоматизация финансовых операций, управление товарами, налоговые отчеты*  
[![C4 Model](https://img.shields.io/badge/C4-Model-blue.svg)](https://c4model.com/) 
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.0-green.svg)](https://spring.io/projects/spring-boot) 
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0.3-yellow.svg)](https://spec.openapis.org/oas/v3.0.3)

## Описание системы

**GUESS** обслуживает **бухгалтера, кассира, менеджера** и интегрируется с **ФНС, банком, email-сервисами** для:
- ACID-гарантии финансовых операций
- Real-time отчетов (<5 сек)
- JWT + RBAC безопасности
- Горизонтальной масштабируемости

## Архитектура C4 Model

### C1: System Context (Уровень 1)
**Акторы:** Бухгалтер, Кассир, Менеджер, Администратор  
**Внешние системы:** ФНС (HTTPS+mTLS), Банк (REST+OAuth2), Email (SMTP) [file:23]

### C2: Containers (Уровень 2)
React Frontend → Spring Boot API → PostgreSQL + Redis + RabbitMQ

### C3: Backend Components (Уровень 3)
Controllers → Services → Repositories + Security (JWT)


## Технологический стек

| Компонент | Технология | Версия | Обоснование |
|-----------|------------|--------|-------------|
| **Backend** | Spring Boot | 3.0+ | ACID, Enterprise-ready, 250+ starters [file:23] |
| **Frontend** | React | 18 | TypeScript, экосистема, DevTools [file:23] |
| **Database** | PostgreSQL | 14 | ACID, Foreign Keys, Referential Integrity [file:23] |
| **Cache** | Redis | 7.0 | Real-time дашборды (<3ms) [file:23] |
| **Queue** | RabbitMQ | 3.12 | Асинхронные отчеты, DLQ [file:23] |
| **API** | OpenAPI 3.0.3 | - | Swagger UI, CodeGen [file:23] |

## Быстрый старт

1. Клонировать репозиторий
git clone https://github.com/3-IAIT-109/GUESS-Accounting.git
cd GUESS-Accounting

2. Сгенерировать документацию и код
chmod +x generate_docs.sh
./generate_docs.sh

3. Запустить (после настройки .env)
docker-compose up -d postgres redis rabbitmq
cd generated-server && ./mvnw spring-boot:run


## Структура проекта

GUESS-Accounting/
├── README.md # Документация
├── generate_docs.sh # Автогенерация C4 + OpenAPI → код
├── docs/
│ └── c4-diagrams/ # Structurizr PNG/SVG
├── api-specification/
│ └── openapi.yaml # REST API спецификация
├── src/
│ └── structurizr/ # C4 модель (DSL/Java)
├── generated-server/ # Spring Boot сервер (автогенерация)
├── frontend/ # React 18 + TypeScript
└── docker-compose.yml # PostgreSQL + Redis + RabbitMQ

## API Документация

- **OpenAPI спецификация**: [api-specification/openapi.yaml](api-specification/openapi.yaml)
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **REST Endpoints**:
POST /api/v1/sales # Создать продажу
GET /api/v1/products # Список товаров
POST /api/v1/tax-reports # Налоговый отчет
POST /api/v1/auth/login # JWT аутентификация

##  Генерация артефактов

**Автоматический конвейер Model-Driven Development:**

./generate_docs.sh
undefined
Structurizr DSL → C4 Diagrams (PNG/SVG)
OpenAPI YAML → Spring Boot Server Code
PlantUML → Class Diagrams
## Производительность & Масштабируемость

БЕЗ Redis: 130ms на дашборд
С Redis: <3ms (40x быстрее!)

**Горизонтальное масштабирование:**
Spring Boot API (3 pod) → PgBouncer → PostgreSQL (Read Replica)
Redis Cluster → RabbitMQ Cluster


## Безопасность

- **ACID транзакции**: PostgreSQL Foreign Keys + Triggers
- **mTLS**: Интеграция с ФНС 
- **OAuth2**: Банк API 

## Требования (по приоритетам)

| Требование | Статус | Приоритет |
|------------|--------|-----------|
| ACID гарантии | ✅ PostgreSQL | **КРИТИЧНО** |
| Real-time отчеты | ✅ Redis | **ВЫСОКИЙ** |
| JWT + RBAC | ✅ Spring Security | **КРИТИЧНО** |
| Интеграция ФНС/Банк | ✅ OpenAPI | **ВЫСОКИЙ** |

## Авторы

**Студенты группы 3-ИАИТ-109**  
- Казаков Н.Д.  
- Стенькин М.А.  

**Преподаватели:**  
- Волхонский А.Н.  
- Тюгашев А.А.  

**Самарский государственный технический университет, 2025**
