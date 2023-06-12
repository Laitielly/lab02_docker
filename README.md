# Лабораторная работа 2

Максимальная оценка: 10

Ожидаемая оценка: 8 - 10

## Задачи лабораторной работы:

- Использовать имеющееся приложение (курсовую/лабораторную). - **Выполнено**

&emsp; &emsp;  Использован генетический алгоритм для задачи knapsack 0-1 из лабораторной работы. 

&emsp; &emsp;  Файл [main.py](https://github.com/Laitielly/lab02_docker/blob/main/main.py) - алгоритм. Файл [test](https://github.com/Laitielly/lab02_docker/tree/main/test) - файл с тестами. Файлы в этой папке называть ТОЛЬКО следующим образом:

&emsp;&emsp;&emsp;     1. [p01_c.txt](https://github.com/Laitielly/lab02_docker/blob/main/test/p01_c.txt) - файл с общей вместимостью рюкзака

&emsp;&emsp;&emsp;     2. [p01_p.txt](https://github.com/Laitielly/lab02_docker/blob/main/test/p01_p.txt) - файл со стоимостями предметов

&emsp;&emsp;&emsp;     3. [p01_w.txt](https://github.com/Laitielly/lab02_docker/blob/main/test/p01_w.txt) - файл с весом каждого предмета


&emsp;&emsp; Если хотите использовать свою папку test, то примаунтите её с помощью команды (после сборки образа):

```
docker run -v <your path>/test:/test laitielly/knapsack01:latest
```

&emsp;&emsp; Вывод формата вывода на экран + файл [outs.txt](https://github.com/Laitielly/lab02_docker/blob/main/outs.txt):
```
Time: 0.44604
Total weight: 749
Total profit: 1454
ID of items: [0, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 1]
```


- Собрать Docker образ этого приложения с использованием [Dockerfile](https://github.com/Laitielly/lab02_docker/blob/main/Dockerfile.txt). - **Выполнено**

![Скрин1](https://github.com/Laitielly/labs_docker/blob/main/images_docker/pic1_lab2.png)

- Запушить [Docker образ](https://hub.docker.com/r/laitielly/knapsack01/tags) в [Docker Hub](https://hub.docker.com/u/laitielly). - **Выполнено**

- Настроить [Github Actions](https://github.com/Laitielly/lab02_docker/blob/main/.github/workflows/start.yml) для автоматического билда и пуша образа при изменении кода. - **Выполнено**

- Настроить запуск линтера (статический анализатор кода) в пайплайне сборки. - **Выполнено**

Использую pylint. Пока анализирую только main.py, но одной из команд 

```
pylint --rcfile=.pylintrc <directory_name>
pylint $(pwd)
find . -type f -name "*.py" -exec pylint -j 0 --exit-zero {} \;
```
можно запустить проверку на всех *.py файлах.

- Развернуть приложение на тестовом сервере или локальной машине в рамках пайплайна.  - **Выполнено**

&emsp;&emsp; Развернут Runner на Mac OS. Запускается в [start.yaml](https://github.com/Laitielly/lab02_docker/blob/main/.github/workflows/start.yml).

```
  localrun:
    needs: build
    runs-on: self-hosted
    
    steps:
      - uses: actions/checkout@v3
      - name: pull and run
        run: |
          docker pull laitielly/knapsack01:latest
          docker run laitielly/knapsack01:latest
```

Скачивается на локалхост образ. Его можно запускать дальше на машине.

## Требования:

- Работа должна быть выполнена индивидуально. - **Выполнено**
- Студенты могут использовать любой язык программирования для приложения. - **Выполнено**
- Образ должен быть опубликован в публичном репозитории Docker Hub. - **Выполнено**
- Github Actions должен быть настроен на использование официальных действий Docker (например, docker/build-push-action). - **Выполнено**
- Приложение должно успешно проходить проверку линтера (статического анализатора кода). - **Выполнено**
- Развертывание приложения должно быть выполнено на тестовом сервере или локальной машине с использованием соответствующих инструментов и технологий. - **Выполнено**

## Команды в помощь

### Развернуть самостоятельно
```
cd <your path>
docker build . -t <name>:latest -f Dockerfile.txt
```

### Скачать и развернуть на локальной машине:

- Загружаем образ с Docker Hub 
```
docker pull laitielly/knapsack01:latest
```
- Создаем контейнер
```
docker run -v <your path>/test:/test laitielly/knapsack01:latest
```
- Запускаем контейнер
```
docker start -a -i <CONTAINER ID>
```
**Доп команда:** Узнать ID контейнера:
```
docker ps -a
```
