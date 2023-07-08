## Навигация

pwd (от англ. print working directory, «показать рабочую папку») — покажи, в какой я папке;  
ls (от англ. list directory contents, «отобразить содержимое директории») — покажи файлы и папки в текущей папке;  
ls -a — покажи также скрытые файлы и папки, названия которых начинаются с символа . ;  
cd first-project (от англ. change directory, «сменить директорию») — перейди в папку first-project;  
cd first-project/html — перейди в папку html, которая находится в папке first-project;  
cd .. — перейди на уровень выше, в родительскую папку;  
cd ~ — перейди в домашнюю директорию (/Users/Username);  
cd / — перейди в корневую директорию.

## Работа с файлами и папками

### Создание

touch index.html (англ. touch, «коснуться») — создай файл index.html в текущей папке;  
touch index.html style.css script.js — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;  
mkdir second-project (от англ. make directory, «создать директорию») — создай папку с именем second-project в текущей папке.  
Можно создать целую структуру директорий одной командой с помощью флага -p  

### Копирование и перемещение

cp file.txt ~/my-dir (от англ. copy, «копировать») — скопируй файл в другое место;  
mv file.txt ~/my-dir (от англ. move, «переместить») — перемести файл или папку в другое место.  

### Чтение

cat file.txt (от англ. concatenate and print, «объединить и распечатать») — распечатай содержимое текстового файла file.txt.  

### Удаление

rm about.html (от англ. remove, «удалить») — удали файл about.html;  
rmdir images (от англ. remove directory, «удалить директорию») — удали папку images;  
rm -r second-project (от англ. remove, «удалить» + recursive, «рекурсивный») — удали папку second-project и всё, что она содержит.  

### Полезные возможности

Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (&&).
У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх (↑) и вниз (↓).
Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать Tab. Если файл или папка есть в текущей директории, командная строка допишет путь сама.
Например, вы находитесь в папке dev. Начните вводить cd first и дважды нажмите Tab. Если папка first-project есть внутри dev, командная строка автоматически подставит её имя. Останется только нажать Enter.

## Работа с файлом настройки .gitconfig

Вы можете указать любую электронную почту и любое имя. Сделать это можно с помощью команды git config (от англ. configuration — «конфигурация», «настройка») с ключом --global
В качестве значения user.name нужно указать своё имя или никнейм. Для настройки параметра user.email указывают электронную почту.
Все глобальные настройки Git хранит в файле .gitconfig в домашней директории. Команда запишет в этот файл указанные имя и почту. Чтобы убедиться в этом, можно вызвать команду для чтения файлов.
$ cat ~/.gitconfig 

## Установка SSH

ls -la .ssh/ # вывели список созданных ключей
Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
Теперь осталось проверить, что ключи действительно сгенерировались.
ls -a ~/.ssh 

## Связывание репозиториев

скопировать содержимое ключа в буфер обмена:  
$ clip < ~/.ssh/id_rsa.pub  
для ed25519:  
$ clip < ~/.ssh/id_ed25519.pub  

Проверьте правильность ключа с помощью следующей команды.  
$ ssh -T git@github.com  

Привязать удалённый репозиторий к локальному — git remote add  
Убедиться, что репозитории связаны, — git remote -v  

$ git remote -v    
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)  
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)   

В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.

git remote remove origin - удалить ошибочное связывание

## Commit

Сделать папку репозиторием — git init  
«Разгитить» папку, если что-то пошло не так, — rm -rf .git  
Проверить состояние репозитория — git status  
Команда git add --all подготовит к сохранению сразу все файлы.  
С помощью git add . можно добавить в репозиторий текущую папку со всеми файлами.  
Ключ -m позволяет присвоить коммиту сообщение.  
Сделать коммит можно командой git commit c ключом -m (от англ. message — «сообщение»), который присваивает коммиту сообщение.  

Ещё раз о разнице между git add и git commit  
Сначала команда git add сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды git commit происходит само сохранение.  

Просмотреть историю коммитов — git log  

## Push

Отправить изменения на удалённый репозиторий — git push
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой.
В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push


# Шпаргалка markdown

## Выделение текста

Вы можете выделять текст в markdown с помощью символов `_` или `*`. Например:

Пример _курсива_ и **жирного** текста.

## Заголовки

Заголовки можно создавать с помощью символа `#`. Чем больше `#`, тем меньше заголовок. Например:

# Заголовок первого уровня
## Заголовок второго уровня
### Заголовок третьего уровня

## Выделение кода

Чтобы выделить текст как код, поместите его в тройные кавычки `````. 

```
mkdir my_project
cd my_project
git init
```
Это лишь некоторые функции markdown. 