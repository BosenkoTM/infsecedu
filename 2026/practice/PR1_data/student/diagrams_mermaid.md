# Mermaid-шаблоны для ПР1

Все итоговые рисунки в отчёте должны храниться как Mermaid-код.

## 1. Контекстная схема

```mermaid
flowchart LR
    Student["Обучающийся"]
    Teacher["Педагог"]
    Admin["Администрация"]
    LMS["LMS"]
    Journal["Электронный журнал"]
    DB[("Локальная БД")]
    Cloud["Файловое облако"]
    External["Внешний сервис"]

    Student --> LMS
    Teacher --> LMS
    Teacher --> Journal
    Admin --> DB
    DB --> Journal
    Teacher --> Cloud
    Student --> External
```

## 2. Доверительные границы

```mermaid
flowchart TB
    subgraph EXT["Внешняя зона"]
        User["Внешний пользователь"]
        Provider["Внешний сервис"]
    end
    subgraph CLOUD["Облачные сервисы"]
        LMS["LMS"]
        EJ["Электронный журнал"]
    end
    subgraph SCHOOL["Внутренняя сеть"]
        DB[("База контингента")]
        AdminPC["АРМ администрации"]
    end
    User --> LMS
    Provider --> LMS
    AdminPC --> DB
    DB --> EJ
    EXT -. граница 1 .- CLOUD
    CLOUD -. граница 2 .- SCHOOL
```

## 3. Цепочка сценария угрозы

```mermaid
flowchart LR
    S["Источник угрозы"] --> V["Уязвимость"]
    V --> E["Событие"]
    E --> A["Актив"]
    A --> C["Последствие"]
    C --> R["Риск"]
```

## 4. Жизненный цикл обработки риска

```mermaid
flowchart LR
    Identify["Выявить"] --> Assess["Оценить"]
    Assess --> Prioritize["Приоритизировать"]
    Prioritize --> Treat["Обработать"]
    Treat --> Residual["Оценить остаточный риск"]
    Residual --> Monitor["Контролировать"]
    Monitor --> Identify
```

## 5. Роли

```mermaid
flowchart TD
    Director["Руководитель"]
    RiskOwner["Владелец риска"]
    SysAdmin["Системный администратор"]
    Teacher["Педагог"]
    DPO["Ответственный за организацию обработки ПДн"]
    Director --> RiskOwner
    RiskOwner --> SysAdmin
    RiskOwner --> DPO
    Teacher -->|сообщает об инциденте| RiskOwner
```

## 6. Шаблон диаграммы конкретного риска

```mermaid
sequenceDiagram
    participant U as Пользователь
    participant S as Сервис
    participant D as Хранилище данных
    participant A as Администратор
    U->>S: штатное действие
    S->>D: чтение/запись
    Note over U,S: Здесь студент отмечает уязвимость
    U-->>S: нежелательное/ошибочное действие
    S-->>A: событие журналирования
```
