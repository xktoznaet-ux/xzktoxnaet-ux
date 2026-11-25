# Практическая работа: Git Stash, Reset и Revert

Выполнены задания **1.3, 2.6 и 2.7**.

## 1.3. Временно сохраняем работу через Git Stash

Файлы:
- `task_1_3/main.py`
- `task_1_3/students.py`

Команды:

```bash
git init
git add main.py
git commit -m "Initial commit"
git switch -c feature-students
# В main.py добавлена строка: print("Add student feature")
# Создан students.py со строкой: students = []
git status
git stash push -u -m "unfinished students feature"
git status
git stash list
git stash pop
git status
```

**Ответ:** опция `-u` нужна, потому что `students.py` — новый, ещё не отслеживаемый Git файл. Обычный `git stash` по умолчанию не сохраняет такие файлы.

## 2.6. Практика A: Reset

Файл: `task_2_6/app.py`.

Созданы две версии и два коммита:

```bash
git add app.py
git commit -m "Add version 1"
git add app.py
git commit -m "Add version 2"
git log --oneline
git reset --soft HEAD~1
git status
git log --oneline
```

**Результат `--soft`:** последний коммит отменён, но изменения второй версии остались в Staging Area (подготовлены к коммиту).

Для сравнения выполните в отдельном тестовом репозитории:

```bash
git reset --mixed HEAD~1
```

**Разница:** `--mixed` тоже перемещает ветку на предыдущий коммит, но убирает изменения из Staging Area. Сами изменения остаются в рабочем файле.

## 2.7. Практика B: Revert

Файл: `task_2_7/app.py`.

Созданы три последовательных коммита с разными изменениями. Затем отменён последний коммит:

```bash
git log --oneline
git revert HEAD
git log --oneline
```

**Ответ:** старый коммит остаётся в истории, потому что `git revert` не удаляет его и не переписывает историю. Команда создаёт новый коммит, который вносит обратные изменения. Это удобно для опубликованных коммитов в общей ветке.
