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
Можно создать целую структуру директорий одной командой с помощью флага `-p`    

### Копирование и перемещение

cp file.txt ~/my-dir (copy) — скопируй файл в другое место;  
mv file.txt ~/my-dir (move) — перемести файл или папку в другое место.  

### Чтение и редактирование текстовых файлов 

cat file.txt (concatenate and print) — распечатай содержимое текстового файла file.txt.  
echo "text" >> (file) - дописываем строку в конец файла    
echo "text" > (file) - полностью стираем файл и вносим новую строку  

### Удаление

rm about.html (remove) — удали файл about.html;  
rmdir images (remove directory) — удали папку images;  
rm -r second-project (remove + recursive) — удали папку second-project и всё, что она содержит.  

### Полезные возможности

Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами `(&&)`.
У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх `(↑)` и вниз `(↓)`.
Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать `Tab`. Если файл или папка есть в текущей директории, командная строка допишет путь сама.
Например, вы находитесь в папке dev. Начните вводить cd first и дважды нажмите Tab. Если папка first-project есть внутри dev, командная строка автоматически подставит её имя. Останется только нажать Enter.

## Работа с файлом настройки .gitconfig

Вы можете указать любую электронную почту и любое имя. Сделать это можно с помощью команды `git config` (configuration) с ключом `--global`  
В качестве значения user.name нужно указать своё имя или никнейм. Для настройки параметра user.email указывают электронную почту.
Все глобальные настройки Git хранит в файле .gitconfig в домашней директории. Команда запишет в этот файл указанные имя и почту. Чтобы убедиться в этом, можно вызвать команду для чтения файлов.
$ cat ~/.gitconfig 

## Установка SSH

ls -la .ssh/ # вывели список созданных ключей
Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
Теперь осталось проверить, что ключи действительно сгенерировались.
ls -a ~/.ssh 

## Привязываем SSH-ключ к GitHub  

скопировать содержимое ключа в буфер обмена:  
$ clip < ~/.ssh/id_rsa.pub  
для ed25519:  
$ clip < ~/.ssh/id_ed25519.pub  

## Создание репозитория  
 
Сделать папку репозиторием — git init  
«Разгитить» папку, если что-то пошло не так, — rm -rf .git  
Проверить состояние репозитория — git status  

## Связывание репозиториев

Проверьте правильность ключа с помощью следующей команды.  
$ ssh -T git@github.com  

Привязать удалённый репозиторий к локальному — git remote add  
```
$ cd ~/dev/first-project  
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git  
```
Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.  
Убедиться, что репозитории связаны, — `git remote -v`    
`git push -u origin main (or master)` — в первый раз загрузи все коммиты из локального репозитория в удалённый с названием origin.  
```
$ git remote -v    
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)  
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)   
```

В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.

git remote remove origin - удалить ошибочное связывание  

## Commit  

Команда `git add --all` подготовит к сохранению сразу все файлы.  
С помощью `git add .` можно добавить в репозиторий текущую папку со всеми файлами.  
Ключ -m позволяет присвоить коммиту сообщение.  
Сделать коммит можно командой git commit c ключом -m (message), который присваивает коммиту сообщение.  

Ещё раз о разнице между git add и git commit  
Сначала команда git add сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды git commit происходит само сохранение.  

Дополнить коммит новыми файлами — `git commit --amend --no-edit`. С опцией --amend команда commit не создаст новый коммит, а дополнит последний, просто добавив в него файл.    
Изменить сообщение коммита — `git commit --amend -m "Новое сообщение"`    
Убрать файл из staging поможет команда `git restore --staged (file)`. Допустим, вы создали или изменили какой-то файл и добавили его в список «на коммит» (staging area), но потом передумали включать его туда.  
Чтобы «сбросить» все файлы из staged обратно в untracked/modified, можно воспользоваться командой `git restore --staged .` (она сбросит всю текущую папку).  
Откатить коммит — `git reset --hard (commit hash)`      
Откатить изменения, которые не попали ни в staging, ни в коммит, — `git restore (file)`. Может быть так, что вы случайно изменили файл, который не планировали. Теперь он отображается в Changes not staged for commit (modified).    

Просмотреть историю коммитов — git log  
q - выйти из логов  
Получить сокращённый лог — git log --oneline   

## Просматриваем изменения в файлах  

`git diff` эта команда сравнит последнюю закоммиченную версию файла с текущей (изменённой) версией. git diff не показывает изменения в staged-файлах — только в modified.  
Чтобы просмотреть изменения в staged, нужно использовать флаг --staged: `git diff --staged`.  
Передайте команде `git diff (first hash) (second hash)` хеши двух коммитов. Состояние файлов на момент первого переданного коммита будет сравниваться с состоянием файлов на момент второго.  

## Push

Отправить изменения на удалённый репозиторий — git push
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой.
В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push


## Статусы файлов в Git  

Статусы untracked/tracked, staged и modified  
состояние файла staged иногда называют indexed или cached       

## Игнорирование файлов в Git  
 
Чтобы Git игнорировал файлы и не пытался добавить их в репозиторий, нужно создать файл .gitignore и записать в него названия игнорируемых файлов. Правила из .gitignore применяются только к новым (untracked) файлам. Если файл уже попал в staging area или в коммит, то правила на него не распространяются.  
Если строка начинается с #, то это комментарий, и .gitignore не будет его учитывать.  
```
# для macOS    
`.DS_Store
```  
В таком случае Git будет игнорировать файлы с именем .DS_Store, причём не только в корне репозитория, но и во всех вложенных папках.  
Символ звёздочки `(*)` соответствует любой строке, включая пустую. Если такой символ используется в шаблоне в .gitignore, значит, файл будет проигнорирован вне зависимости от того, что будет на месте звёздочки.  
```
# игнорировать все файлы, которые заканчиваются на .jpeg    
*.jpeg    
# игнорировать все файлы "tmp" во всех подпапках папки docs    
docs/*/tmp 
``` 
`?` вопросительный знак соответствует одному любому символу.  
`file?.txt`  
`([…])` квадратные скобки  
Квадратные скобки, как и вопросительный знак, соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.  
```
# игнорировать файлы file0.txt, file1.txt и file2.txt  
# при этом не игнорировать file3.txt, file4.txt, ...  
file[0-2].txt
```  
В скобках можно либо перечислить символы ([abc]), либо задать диапазон ([a-z]).  
`(/)` - слеш  
Косая черта, или слеш (/), указывает на каталоги. Если шаблон в .gitignore начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.  
```
# игнорировать todo.txt в корне репозитория  
/todo.txt  
# для сравнения: spam.txt будет игнорироваться во всех папках  
spam.txt
```  
Если шаблон заканчивается слешем, то правило применится только к папке.  
```
# игнорировать папку build  
build/
```  
`(**)` парные звёздочки  
Функция парных звёздочек (**) похожа на функцию одинарной `(*)`. Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю). Одинарная может соответствовать только одной.  
```
# игнорировать файлы "docs/current/tmp", "docs/old/tmp",  
# а также "docs/old/saved/a/b/c/d/tmp"  
# и даже "docs/tmp", потому что ноль вложенных папок тоже подходит  
docs/**/tmp  
# игнорировать только "docs/current/tmp" и "docs/old/tmp"  
# файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило  
docs/*/tmp
```  
`(!)` восклицательный знак  
Любое правило в файле .gitignore можно инвертировать с помощью восклицательного знака (!).  
```
# игнорировать все JPEG-файлы  
*.jpeg  
# но только не мем с Doge  
!doge.jpeg
```

## Основы работы с ветками в Git  
Клонировать репозиторий — `git clone`. git clone автоматически связывает локальный репозиторий с удалённым.  
Просмотреть ветки проекта — `git branch`. Чтобы выйти из просмотра веток, может понадобиться Q!  
Создать ветку — `git branch (название_ветки)`  
Переключиться на другую ветку — git checkout %название_ветки%    

## Разные команды  
```
$ chmod +x check.sh # эта команда сделает файл исполняемым  
$ ./check.sh # эта команда исполнит скрипт  
```

 


