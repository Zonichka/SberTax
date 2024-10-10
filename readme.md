# SberTax

## Архитектура репозитория

### Основная модель веток:
1. **`main`**:
   - Главная стабильная ветка.
   - Только релизные версии проекта попадают сюда.
   - Ветка защищена, слияние происходит только через Pull Request (PR) с успешными тестами.

2. **`develop`**:
   - Основная ветка для активной разработки.
   - Сюда вливаются изменения с feature-веток после их завершения и успешного тестирования.
   - Периодически изменения из `develop` сливаются в `main`, когда готов новый релиз.
   - Должна содержать Docker-compose файл для поднятия всех сервисов в единой среде.

3. **`feature/*`**:
   - Ветки для каждой новой фичи или задачи.
   - Создаются от `develop` и после завершения работы сливаются обратно в `develop`.
   - Пример названия: `feature/api-endpoints`, `feature/data-processing`.

4. **`bugfix/*`**:
   - Ветки для исправления багов, изначально их нет.
   - Создаются от `develop` или, в случае критических ошибок на продакшне, от `main`.
   - После фикса баги вливаются обратно в соответствующую ветку (например, `develop` или `main`).

5. **`hotfix/*`**:
   - Ветки для срочных исправлений в продакшене, изначально их нет.
   - Создаются от `main`, исправления тестируются и затем вливаются обратно в `main` и `develop`.
   - Пример названия: `hotfix/critical-bug`.

6. **`release/*`**:
   - Ветки для подготовки релиза.
   - Когда фичи стабилизированы в `develop`, создается ветка `release/x.x.x` для подготовки новой версии.
   - После тестирования и исправлений изменения сливаются в `main`.


### Визуализация:
```bash
main <--- release <--- develop <--- feature/*
 ^          ^            ^             ^
 |          |            |             |
 hotfix     bugfix      feature       feature
```
