# Каким должен быть хороший коммит

### Формат

```bash
    <type>[optional scope]: <description>

    [optional body]

    [optional footer]
```

Пример: `feat(auth): добавить OAuth-авторизацию через Google`

#### **Компоненты:**
- **Тип** (обязательно):  
  Указывает категорию изменения. Основные типы:
  - `feat` — новая функциональность.
  - `fix` — исправление бага.
  - `refactor` — изменение кода без добавления функциональности/исправления (например, оптимизация).
  - `docs` — обновление документации.
  - `test` — изменения в тестах.
  - `chore` — вспомогательные задачи (обновление конфигов, зависимостей).
  - `style` — правки форматирования (пробелы, отступы).
  - `revert` — отмена предыдущего коммита.

- **Область** (опционально):  
  Уточняет, какой модуль/компонент затронут (например, `api`, `ui`, `database`).  
  Если изменение глобальное, область можно опустить: `fix: исправить пагинацию`.

- **Описание**:  
  Кратко (до 50 символов) объясняет суть изменения в **императиве** (как приказ):  
  ❌ `добавлена валидация` → ✅ `добавить валидацию полей формы`.

---

### Многострочные коммиты

Если требуется детализация, добавьте описание после пустой строки:

```text
feat(profile): добавить загрузку аватара

- Реализован компонент UploadAvatar
- Добавлена валидация форматов (PNG, JPEG)
- Обновлены тесты
```

---

### Плохие коммиты

- ❌ Расплывчатые сообщения: `починил баг`, `еще правки`.
- ❌ Коммиты с множеством несвязанных изменений (нарушают принцип атомарности).
- ❌ Переносы строк в заголовке.

**так делать не надо**

### Хорошие коммиты

- ✅ `fix(api): устранить ошибку CORS для endpoint /v1/products`  
- ✅ `docs: обновить README с примерами использования`  
- ✅ `refactor(auth): вынести валидацию токена в отдельный сервис`  

---

## Установка хука

1. **Добавить папку .githooks/ в корень проекта**

2. **Установить путь к папке со скриптами**

```bash
    git config core.hooksPath .githooks
```

*Если используется Unix-подобная система, также напишите:*

```bash
    chmod +x .githooks/*
```

---

**Эта версия хука не поддерживает многострочные коммиты**

Чтобы добавить поддержку многострочных коммитов, измените регулярное выражение:

```bash
    regex = r"^(feat|fix|refactor|docs|test|chore|style|revert)(\(.+\))?: .+(\n)(\n+.*)*$"
```

Либо используйте команду с отключением проверки git-хуков:

 ```bash
  git commit --no-verify
 ```