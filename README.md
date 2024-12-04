# Телеграмм бот для отслеживания процесса обучения

Бот собирает от каждого ученика информацию, его планы на спринт.
Спринт составляет одну неделю.
Ежедневно описывает в боте проделанную работу по обучению.

Бот будет отправлять запрос в личный чат каждому ученику. Всего 2 вида запросов:
1. Сбор планов на спринт по понедельникам в 10.00.
2. Сбор информации по пройденному материалу, каждый день в 18.00.

#### Функционал пользователя:

Идентификация и авторизация пользователя в боте
Ежедневный запрос ботом от пользователя информации о пройденным темах и времени на их изучение
Запись в google таблицу (базу данных) ежедневного отчета
Запрос ботом, каждую неделю, планов на спринт
Запись в google таблицу (базу данных) планов на спринт
Отображение статистики по обучению

#### Функционал администратора

Идентификация и авторизация администратора в боте
Управление пользователями (добавить пользователя, удалить пользователя)

Стек технологий:
- Python 3.11
- TeleBot(pyTelegramBotAPI) в синхронной реализации -> [дока](https://pytba.readthedocs.io/ru/latest/quick_start.html)
- Sqlite3
- APScheduler

## Запуск проекта

### Fork

1. Делаем fork репозитория к себе в аккаунт: Справа вверху жмем кнопку
```
fork -> Create fork
```
2. Клонируем репозиторий из своего аккаунта локально на компьютер
```bash
git clone <ссылка на ваш форк репозитория>
```
3. Привязываем оригинальный репозиторий к своему
```bash
cd <каталог репозитория>
git remote add <привязка к репозиторию> <ссылка на ваш форк репозитория>
git fetch <привязка к репозиторию>
```
Клонированный репозиторий имеет одну привязку к удаленному репозиторию "origin". Чтобы иметь привязку и к оригинальному репозиторию, нужно добавить ещё одни привязку.

### Подготовка виртуального окружения

Так как проектом предусмотрено применение версии Python 3.11, то можете воспользоваться менеджером управления версий [pyenv](https://github.com/pyenv/pyenv)

Устанавливаем pyenv
Для Linux
```bash
curl https://pyenv.run | bash
```
Для MacOS установите через brew
```shell
brew update
brew install pyenv
```
Fork для [Windows](https://github.com/pyenv-win/pyenv-win)
```PowerShell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
```

Настраиваем среду оболочки для pyenv
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```

Переходим в папку с проектом и устанавливаем версию python 3.11 локально
```bash
pyenv local 3.11
```

Создаем виртуальное окружение в каталог ".venv", находясь в папке проекта
```bash
python -m venv .venv
```

Проверяем правильно ли подтянулась версия python
```bash
pyenv version
```

Активируем среду виртуального окружения
Для UNIX подобных систем (Linux, MacOS)
```bash
source .venv/bin/activate
```
Для Windows
```shell
.venv\Scripts\activate
```
В Pycharm выбираем интерпретатор python из виртуальной среды

Запускаем рекурсивную установку пакетов проекта
```bash
pip install -r requirements.txt
```

Проверяем список установленных проектов
```bash
pip list
```

Создаем файл .env в каталоге проекта и копируем туда свой token бота, по аналогии с файлом .env.example

Устанавливаем настройки pre-commit
```bash
pre-commit install
```
При этом будет настроена проверка кода по установленным правилам из файла .pre-commit-config.yaml и подтянется линтер ruff по правилам из файла pyproject.toml

### Pull request

Для работы над своей задачей сделайте ветвление на локальной машине от ветки main на ветку вида feature/<идентификатор задачи>\_<краткое описание>
```bash
git branch feature/<идентификатор задачи>\_<краткое описание задачи>
```

Переключаемся на ветку своей задачи
```bash
git checkout feature/<идентификатор задачи>\_<краткое описание задачи>
```

После завершения задачи и ее проверки делаем commit
```bash
git add <добавляемые файлы>
git commit -m "свой commit"
```
При этом pre-commit запустит проверку согласно про писаных правил, и не даст провести commit при выявленных нарушениях

Пушим изменения из своей ветки на origin репозиторий
```bash
git push origin feature/<идентификатор задачи>\_<краткое описание задачи>
```

Заходим на страницу оригинального репозитория в GitHub и создам Pull Request на основе созданной нами ветви.
Обычно github уже видит созданную ветвь, и сам предлагает создать Pull Request к ней.

Отписываем в чате, что сделали Pull Request.

Для закрытия Pull Request нужно ответить на все комментарии и закрыть комментарии по кнопке resolve conversation.
