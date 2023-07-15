## Навигация

pwd (print working directory) — покажи, в какой я папке;  
ls (list directory contents) — покажи файлы и папки в текущей папке;  
ls -a — покажи также скрытые файлы и папки, названия которых начинаются с символа . ;  
cd first-project (change directory) — перейди в папку first-project;  
cd first-project/html — перейди в папку html, которая находится в папке first-project;  
cd .. — перейди на уровень выше, в родительскую папку;  
cd ~ — перейди в домашнюю директорию (/Users/Username);  
cd / — перейди в корневую директорию.

## Работа с файлами и папками

### Создание

touch index.html — создай файл index.html в текущей папке;  
touch index.html style.css script.js — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;  
mkdir second-project (make directory) — создай папку с именем second-project в текущей папке.  
Можно создать целую структуру директорий одной командой с помощью флага -p  

### Копирование и перемещение

cp file.txt ~/my-dir (copy) — скопируй файл в другое место;  
mv file.txt ~/my-dir (move) — перемести файл или папку в другое место.  

### Чтение

cat file.txt (concatenate and print) — распечатай содержимое текстового файла file.txt.  

### Удаление

rm about.html (remove) — удали файл about.html;  
rmdir images (remove directory) — удали папку images;  
rm -r second-project (remove + recursive) — удали папку second-project и всё, что она содержит.  

### Полезные возможности

Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (&&).
У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх (↑) и вниз (↓).
Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать Tab. Если файл или папка есть в текущей директории, командная строка допишет путь сама.
Например, вы находитесь в папке dev. Начните вводить cd first и дважды нажмите Tab. Если папка first-project есть внутри dev, командная строка автоматически подставит её имя. Останется только нажать Enter.

## Работа с файлом настройки .gitconfig

Вы можете указать любую электронную почту и любое имя. Сделать это можно с помощью команды git config (configuration) с ключом --global
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
Сделать коммит можно командой git commit c ключом -m (message), который присваивает коммиту сообщение.  

Ещё раз о разнице между git add и git commit  
Сначала команда git add сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды git commit происходит само сохранение.  

Дополнить коммит новыми файлами — `git commit --amend --no-edit`. С опцией --amend команда commit не создаст новый коммит, а дополнит последний, просто добавив в него файл.    
Изменить сообщение коммита — git commit --amend -m "Новое сообщение"  
Убрать файл из staging поможет команда git restore --staged (file). Допустим, вы создали или изменили какой-то файл и добавили его в список «на коммит» (staging area), но потом передумали включать его туда.  
Чтобы «сбросить» все файлы из staged обратно в untracked/modified, можно воспользоваться командой git restore --staged . (она сбросит всю текущую папку).  
Откатить коммит — git reset --hard (commit hash)    
Откатить изменения, которые не попали ни в staging, ни в коммит, — git restore (file). Может быть так, что вы случайно изменили файл, который не планировали. Теперь он отображается в Changes not staged for commit (modified).    

Просмотреть историю коммитов — git log  
q - выйти из логов  
Получить сокращённый лог — git log --oneline   

## Push

Отправить изменения на удалённый репозиторий — git push
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой.
В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push


## Статусы файлов в Git  

Статусы untracked/tracked, staged и modified  
состояние файла staged иногда называют indexed или cached  

