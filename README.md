# Boosty media downloader (windows)

- Приложение скачает весь **_доступный вам_** медиаконтент со страницы автора на boosty.to;

- Приложение предназначено для скачивания **_вашего контента_** с **_вашей страницы boosty_**, 
автор не несет ответственность за нецелевое использование приложения;

- **Это не хак-тул**! Приложение скачает только тот контент, к которому вы имеете доступ на сайте boosty.to.


## Как это работает

Приложение создаст папку с названием, совпадающим с user_name автора на boosty и:

- В случае синхронизации по медиа (storage_type: media):
Скачает все доступные фото, видео и аудио (в раздельные директории). Приложение скачает контент в самом высоком из доступных разрешений. При повторном запуске,
уже скачанный контент будет игнорироваться, а новый добавляться в соответствующие директории.
- В случае синхронизации по постам (storage_type: post):
Создаст папку posts, в которую будет синхронизироваться список постов. Один пост - одна папка. Название папки совпадает с ID поста. 
Внутри папки поста будут созданы директории для фото, видео и аудио и синхронизация в них будет производится аналогично storage_type: media.
Так же в каждой паке поста будет создан файл contents.txt - в него будет записываться текст поста.

Не переименовывайте и не удаляйте файлы и директории, созданные приложением, иначе при следующей синхронизации они будут скачаны снова.


## Установка и запуск

### Конфигурация
- Откройте config.yml 
- Введите корневую директорию для синхронизации в file -> sync_dir
- Если хотите скачать закрытый контент, заполните auth -> cookie и auth -> authorization*
- Установите необходимый способ синхронизации в content -> storage_type (media или post)
- Если какой-то из типов контента вам не нужен, удалите (или закомментируйте с помощью #) соответствующую строчку в списке content -> collect
- Если лог синхронизации нужно сохранять в файл, заполните блок logging


*Cookie и Authorization можно найти с помощью инструментов разработчика в вашем браузере:

#### Пример для chrome:
- Перейдите на вашу страницу на boosty.to
- Нажимте клавишу `F12`
- Обновите страницу с помощью `Shift + F5`
- Перейдите в раздел Network 
- Прокрутите страницу вниз
- В списке запросов, выберите пункт post/
- В блоке Request Headers найдите Authorization и Cookie, а затем скопируйте их в соответствующие поля в config.yml 

**Держите содержимое этих параметров в секрете!**

Если через какое-то время приложение перестало скачивать контент, попробуйте обновить значения полей в конфиге, по схеме выше.


### 1. Запуск сборки (рекомендуется)

- #### Перейдите на [страницу релизов](https://github.com/lowfc/boosty_downloader/releases)
- #### Скачайте последний релиз и распакуйте в удобную для вас папку
- #### Заполните конфиг:
Заполните конфиг по инструкции из блока [Конфигурация](#Конфигурация)
- #### Запустите:
Запустите двойным щелчком, или через терминал. Следуйте инструкциям.

#### Для того, что бы синхронизировать конкретный пост:
1. установите режим синхронизации по постам (storage_type: post);
2. запустите программу с параметром -p <id поста>

Например:

```shell
./boosty_downloader.exe -p e87f6e1b-67ab-4fd0-9633-f8efe4ad1990
```

### 2. Запуск распакованного проекта

Запускайте с python версии 3.10 или выше.

- #### Создайте venv:
```shell
python3 -m venv .\venv
```

- #### Активируйте venv:
```shell
.\venv\Scripts\activate
```

- #### Установите зависимости:
```shell
pip install -r requirements.txt
```

- #### Заполните конфиг:
Заполните конфиг по инструкции из блока [Конфигурация](#Конфигурация)

- #### Запустите и следуйте инструкциям:
```shell
python main.py
```

