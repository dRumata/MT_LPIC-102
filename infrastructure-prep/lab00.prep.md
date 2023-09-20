## LAB00-1. Подготовка стенда к выполнению практических работ.
1. Узнайте ip-адреса своих серверов на рабочем стенде.
2. **На серевре s1**. Добавьте записи о ip-адресах своих серверов в файл **/etc/hosts** 
Используйте свои ip и имена (имена серверов вы назначите на следующем шаге), примерный вид дополнительных строк:
```conf
172.16.110.101 s1.familia.local s1
172.16.110.102 s2.familia.local s2
172.16.110.103 s3.familia.local s3
```
   
3. Смените имена у своих серверов. Имена должны быть заданы по рекомендуемому шаблону:
```
Vm1 - s1.familia.local
Vm2 - s2.familia.local
Vm3 - s3.familia.local
```
Используйте `hostnamectl set-hostname`

4. **На сервере s1, s2, s3**. Исправьте отображение приглашения командной оболочки, так чтобы отображалось полное имя сервера, например в **.bashrc** добавить
```conf
export PS1="\[$(tput setaf 6)\]\t\[$(tput setaf 2)\]\[$(tput bold)\][\u@\H \[$(tput sgr0)\]\w]\\$ \[$(tput sgr0)\]"
```

5. **На сервере s1, s2, s3**. Определите запись истории команд таким образом, чтобы сохранялись дата и время в истории, например в **.bashrc** добавить 
```conf
HISTTIMEFORMAT='%D-%T '
```

6. **На серевре s1**. Создайте ключ аутентификации для подключения по **ssh** для пользователя **student** и настройте доступ по **ssh** с сервера **s1** на серверы **s2** и **s3** без использования ввода пароля.
Используйте команды `ssh-keygen` и `ssh-copy-id`

7. **На серевре s1**. Установите и сконфигурируйте все необходимое вам для работы дополнительное ПО на **s1**. 
Например
```
sudo dnf install mc neovim htop tmux nmap wireshark-cli gcc-c++ zsh -y
```

8. ***Опционально!*** Донастройте neovim для удобной работы(для student и для root настраивается отдельно):
```
git clone https://github.com/nvim-lua/kickstart.nvim.git ~/.config/nvim
nvim
```
9. ***Рекомендация!*** При работе на сервере **s1** через ssh (putty, powershell) рекомендуется использовать терминальный мультиплексор  tmux для возможности подключения к вашей сессии. Т.е. 1.Подключились к серверу, 2. Запустили tmux, 3. Работаем. Для удобства работы в tmux можно добавить файл ~/.tmux.conf с конфигурацией:
```conf
set -g mouse on
set -g status-style bg=black
set -g window-status-current-style bg=yellow,fg=black,bold
set -g status-right '#(curl "wttr.in/?format=3") '
set -g default-terminal "tmux-256color"

set -g status-interval 60
set -g status-left-length 30
set -g status-left '#[fg=green]#(cut -d " " -f 1-3 /proc/loadavg)#[default] #[fg=cyan]%H:%M#[default] '
```