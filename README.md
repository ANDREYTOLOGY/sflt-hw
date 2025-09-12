# Домашнее задание к занятию "`Резервное копирование`" - `Чернышов Андрей`

### Задание 1

`Скриншот команды rsync, которая создает зеркальную копию домашней директории пользователя в директорию /tmp/backup, исключает из синхронизации все директории, начинающиеся с точки (скрытые) и  подсчитывает хэш-суммы для всех файлов:`

![rsync-1](https://github.com/ANDREYTOLOGY/sflt-hw/blob/main/img/rsync-1.png)

`Скриншот содержимого директорий:`
![rsync-2](https://github.com/ANDREYTOLOGY/sflt-hw/blob/main/img/rsync-2.png)

### Задание 2

`Скриншот задачи резервного копирования crontab:`

![crontab](https://github.com/ANDREYTOLOGY/zabbixx-hw/blob/main/img/crontab.png)

`Листинг скрипта:`
```
#!/bin/bash

USER="asc"
SOURCE="/home/$USER"
DEST="/tmp/backup"
LOG="/var/log/home_backup.log"


echo "$(date): Начало резервного копирования домашней директории $USER" >> "$LOG"

if rsync -avh --checksum --delete "$SOURCE/" "$DEST/" >> "$LOG" 2>&1; then
    echo "$(date): Резервное копирование успешно завершено" >> "$LOG"
    logger -t backup "Резервное копирование домашней директории $USER выполнено успешно"
    exit 0
else
    echo "$(date): Ошибка при резервном копировании" >> "$LOG"
    logger -t backup "ОШИБКА: Резервное копирование домашней директории $USER не удалось"
    exit 1
fi
```
`Результат выполнения задачи:`
![var-log](https://github.com/ANDREYTOLOGY/zabbixx-hw/blob/main/img/var-log.png)
