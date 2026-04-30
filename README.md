# UML Lab 2 — Focus Planning System

## Introduction

Це веб-сайт, який допомагає починаючим підприємцям сфокусуватися на головному.
Система дозволяє обрати одну цільову аудиторію, визначити основну проблему
та автоматично створити план дій на 7 днів.



## Functional Requirements

* FR-01: Сайт працює без реєстрації
* FR-02: Користувач може обрати лише одну ціль
* FR-03: Користувач вводить свою проблему
* FR-04: Система аналізує проблему
* FR-05: Система генерує план на 7 днів
* FR-06: Користувач може зберегти план



## Use Case Diagram

```mermaid
flowchart LR
    User((Користувач))

    subgraph System[Focus Planning System]
        UC1[Вибір цілі]
        UC2[Введення проблеми]
        UC3[Аналіз проблеми]
        UC4[Генерація плану]
        UC5[Збереження плану]
    end

    User --> UC1
    User --> UC2
    User --> UC4
    User --> UC5

    UC4 --> UC3
```



## Class Diagram

```mermaid
classDiagram

class UserInput {
  +goal : String
  +problem : String
}

class Analyzer {
  +analyze(problem) : String
}

class PlanGenerator {
  +generatePlan(goal, problem) : List
}

class Plan {
  +tasks : List
  +copy() : void
}

class Storage {
  +save(data) : void
  +load() : data
}

UserInput --> Analyzer
Analyzer --> PlanGenerator
PlanGenerator --> Plan
Plan --> Storage
```



## Sequence Diagram

```mermaid
sequenceDiagram

participant User
participant UI
participant Analyzer
participant Generator
participant Plan

User ->> UI: Вводить дані
UI ->> Analyzer: analyze(problem)
Analyzer -->> UI: результат

UI ->> Generator: generatePlan(goal, problem)
Generator ->> Plan: create tasks
Plan -->> UI: tasks

UI -->> User: показ плану
```



## Traceability Matrix

| Requirement | Use Case | Classes                       | Sequence |
| ----------- | -------- | ----------------------------- | -------- |
| FR-01       | —        | —                             | —        |
| FR-02       | UC1      | UserInput                     | —        |
| FR-03       | UC2      | UserInput                     | —        |
| FR-04       | UC3      | Analyzer                      | —        |
| FR-05       | UC4      | PlanGenerator, Plan, Analyzer | SD-01    |
| FR-06       | UC5      | Plan, Storage                 | —        |
