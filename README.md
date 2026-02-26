# container03

## Цель работы 

Познакомиться с основами контейнеризации и подготовить рабочее место для выполнения следующих лабораторных работ.

## Задание

Установить Docker Desktop и проверить его работоспособность.

## Ход работы

### Выполнение

Создать репозиторий containers03 и склонировать его себе на компьютер.

Создать в папке containers03 файл Dockerfile со следующим содержимым:

```
nano Dockerfile

FROM debian:latest
COPY ./site/ /var/www/html/
CMD ["sh", "-c", "echo hello from $HOSTNAME"]
```

В той же папке проекта создайте папку site. В новой папке создайте файл index.html с произвольным содержимым.

```
mkdir site
cd site
echo "Hello, Docker!" >> index.html
```

### Запуск и тестирование

Открыть терминал в папке containers03 и выполнить команду:
```
docker build -t containers03 .
```
Потрачено времени:
```
Building 32.0s (7/7) FINISHED
```

Выполнить команду для запуска контейнера:
```
docker run --name containers03 containers03
```
Что было выведено в консоли?
```
hello from a4579675a81e
```

Удалить контейнер и запустите снова, выполнив команды:
```
docker rm containers03
docker run -ti --name containers03 containers03 bash
```

В открывшемся окне выполнить команды:
```
cd /var/www/html/
ls -l
```

Вывод в консоли:
```
total 4
-rwxr-xr-x 1 root root 15 Feb 26 19:25 index.html
```
Закрыть окно командой exit.

### Problems

mingw64 сохраняет некий cache консоли даже между сессиями, поэтому результат после первой неудачной
```
docker --version
```
выдает command not found даже после добавления в пути в ~/.bashrc, пока кэш не был почищен руками
```
hash -r
```

## Выводы

## Источники