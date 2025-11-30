# Unit testing — quick cheat sheet (MSTest / xUnit / NUnit)

Набор коротких команд для создания solution, библиотеки и тестовых проектов в .NET. Все команды выполняются в терминале; вместо `<...>` подставить свои имена.

---

## Требования

* Установлен .NET SDK (dotnet CLI).

---

## Быстрый порядок действий (шпаргалка)

```bash
# 1. Создать папку решения и перейти в неё
mkdir <solution-folder> && cd <solution-folder>

# 2. Создать solution (файл .sln)
dotnet new sln -o <solution-folder> && cd <solution-folder>

# 3. Создать библиотеку (исходный проект)
dotnet new classlib -o <library-folder>
# пример: dotnet new classlib -o PrimeService

# 4. Добавить библиотеку в solution
dotnet sln add <library-folder>/<library>.csproj
# пример: dotnet sln add PrimeService/PrimeService.csproj

# 5. Создать тестовые проекты (выбрать нужные шаблоны)
dotnet new mstest -o <test-folder-mstest>
dotnet new xunit   -o <test-folder-xunit>
dotnet new nunit   -o <test-folder-nunit>

# 6. Добавить зависимость теста на библиотеку (project reference)
dotnet add <test-project.csproj> reference <library-folder>/<library>.csproj
# пример: dotnet add PrimeService.Tests.MSTest/PrimeService.Tests.MSTest.csproj reference PrimeService/PrimeService.csproj

# 7. Добавить тестовый проект в solution
dotnet sln add <test-project.csproj>
# пример: dotnet sln add PrimeService.Tests.MSTest/PrimeService.Tests.MSTest.csproj

# 8. Удалить сгенерированный шаблонный тест (по желанию)
# bash:
rm -f <test-folder>/UnitTest1.cs
# cmd:
del <test-folder>\UnitTest1.cs

# 9. Восстановить зависимости (опционально)
dotnet restore

# 10. Запуск тестов
dotnet test <test-project.csproj>   # конкретный проект
dotnet test                         # все тесты в solution
```

---

## Что обозначают плейсхолдеры

* `<solution-folder>` — папка с решением (обычно имя репозитория).
* `<library-folder>` — папка с проектом библиотеки (например `PrimeService`).
* `<library>.csproj` — имя файла проекта библиотеки (обычно совпадает с папкой).
* `<test-folder>` / `<test-project.csproj>` — путь к тестовому проекту (например `PrimeService.Tests.MSTest/PrimeService.Tests.MSTest.csproj`).

---

## Короткие пояснения (одна строка про каждую команду)

* `dotnet new sln -o <dir>` — создать solution в папке.
* `dotnet new classlib -o <dir>` — создать проект библиотеки.
* `dotnet new mstest|xunit|nunit -o <dir>` — создать тестовый проект выбранного фреймворка.
* `dotnet sln add <proj.csproj>` — подключить проект к solution.
* `dotnet add <proj.csproj> reference <other.csproj>` — добавить project reference (тест → библиотека).
* `dotnet restore` — загрузить NuGet-пакеты (опционально).
* `dotnet test [<proj.csproj>]` — выполнить тесты (конкретного проекта или всё решение).

---

## Примечания

* В Windows пути обычно через `\`, в bash — через `/`. `dotnet` корректно работает с обоими стилями в большинстве окружений.
* Шаблонные тесты (`UnitTest1.cs`) можно удалить и создать свои тестовые файлы.
* `-o <folder>` автоматически создаёт папку при необходимости; если предпочитается текущая папка, опцию можно опускать.