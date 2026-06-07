# Отчет по лабораторной работе №1
## Тема: Изучение утилит для разработки проектов

**Выполнил:** Игорь Иванов  
**Дата выполнения:** 07.06.2026  
**Среда выполнения:** macOS, Apple clang 21.0.0  
**Репозиторий с файлами:** https://github.com/n9s6sstd5h-blip/lab01

---

## 1. Выполнение туториала

### 1.1. Проверка окружения

**Команда:**
```bash
git --version
```
**Вывод:**
```text
git version 2.50.1 (Apple Git-155)
```

**Команда:**
```bash
g++ --version
```
**Вывод:**
```text
Apple clang version 21.0.0 (clang-2100.1.1.101)
Target: arm64-apple-darwin25.5.0
Thread model: posix
```

**Команда:**
```bash
make --version
```
**Вывод:**
```text
GNU Make 3.81
Copyright (C) 2006  Free Software Foundation, Inc.
```

**Команда:**
```bash
wget --version
```
**Вывод:**
```text
GNU Wget 1.25.0 built on darwin25.2.0.
```

**Команда:**
```bash
openssl version
```
**Вывод:**
```text
OpenSSL 3.6.2 7 Apr 2026 (Library: OpenSSL 3.6.2 7 Apr 2026)
```

---

### 1.2. Настройка переменных окружения

**Команда:**
```bash
export GITHUB_USERNAME=n9s6sstd5h-blip
export LAB_NUMBER=01
alias edit=vim
```

**Команда:**
```bash
echo $GITHUB_USERNAME
```
**Вывод:**
```text
n9s6sstd5h-blip
```

**Команда:**
```bash
echo $LAB_NUMBER
```
**Вывод:**
```text
01
```

---

### 1.3. Создание структуры директорий

**Команда:**
```bash
mkdir -p ${GITHUB_USERNAME}/workspace
cd ${GITHUB_USERNAME}/workspace
pwd
```
**Вывод:**
```text
/Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace
```

**Команда:**
```bash
cd ..
pwd
```
**Вывод:**
```text
/Users/igorivanov/Documents/lab01/n9s6sstd5h-blip
```

**Команда:**
```bash
mkdir -p workspace/tasks/
mkdir -p workspace/projects/
mkdir -p workspace/reports/
cd workspace
pwd
```
**Вывод:**
```text
/Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace
```

---

### 1.4. Подготовка отчета

**Команда:**
```bash
export LAB_NUMBER=01
git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
```
**Вывод:**
```text
$ cd /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace
$ git clone https://github.com/tp-labs/lab01 tasks/lab01
Cloning into 'tasks/lab01'...

[exit code: 0]
```

**Полный вывод:** [git_clone.log](git_clone.log)

**Команда:**
```bash
mkdir reports/lab${LAB_NUMBER}
cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
cd reports/lab${LAB_NUMBER}
pwd
```
**Вывод:**
```text
/Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/reports/lab01
```

---

## 2. Выполнение домашнего задания

### Задание 1. Скачать библиотеку boost

**Команда:**
```bash
wget -O boost_1_69_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
```

**Полный вывод:** [wget.log](wget.log)

---

### Задание 2. Разархивировать boost

**Команда:**
```bash
tar -xzf boost_1_69_0.tar.gz -C /Users/igorivanov
```

**Результат:** архив распакован в каталог `/Users/igorivanov/boost_1_69_0`.

---

### Задание 3. Подсчет файлов без вложенных директорий

**Команда:**
```bash
tar -tzf boost_1_69_0.tar.gz | awk '$0 !~ /\/$/ {n=split($0,a,"/"); if (n==2) c++} END{print c}'
```
**Вывод:**
```text
12
```

---

### Задание 4. Подсчет файлов с вложенными директориями

**Команда:**
```bash
tar -tzf boost_1_69_0.tar.gz | awk '$0 !~ /\/$/ {c++} END{print c}'
```
**Вывод:**
```text
61191
```

---

### Задание 5. Подсчет по типам файлов

**Заголовочные файлы (.h, .hpp, .hxx):**
```bash
tar -tzf boost_1_69_0.tar.gz | awk '$0 !~ /\/$/ && ($0 ~ /\.h$/ || $0 ~ /\.hpp$/ || $0 ~ /\.hxx$/) {c++} END{print c}'
```
**Вывод:**
```text
15208
```

**Файлы .cpp:**
```bash
tar -tzf boost_1_69_0.tar.gz | awk '$0 !~ /\/$/ && $0 ~ /\.cpp$/ {c++} END{print c}'
```
**Вывод:**
```text
13774
```

**Остальные файлы:**
```bash
tar -tzf boost_1_69_0.tar.gz | awk '$0 !~ /\/$/ && !($0 ~ /\.h$/ || $0 ~ /\.hpp$/ || $0 ~ /\.hxx$/ || $0 ~ /\.cpp$/) {c++} END{print c}'
```
**Вывод:**
```text
32209
```

---

### Задание 6. Поиск файла any.hpp

**Команда:**
```bash
find /Users/igorivanov/boost_1_69_0 -type f -name "any.hpp" | sort
```

**Найдено файлов:** 10  
**Полный список:** [any_list.txt](any_list.txt)

---

### Задание 7. Поиск упоминаний boost::asio

**Команда:**
```bash
grep -R "boost::asio" /Users/igorivanov/boost_1_69_0
```

**Количество найденных строк:** 17424  
**Полный вывод:** [asio_list.txt](asio_list.txt)

---

### Задание 8. Компиляция boost

Перед финальной сборкой каталог `/Users/igorivanov/boost_1_69_0` был удален и распакован заново, поэтому сборка выполнялась из чистого проекта.

**Команда:**
```bash
cd /Users/igorivanov/boost_1_69_0
./bootstrap.sh
```

**Полный вывод:** [bootstrap.log](bootstrap.log)

**Команда:**
```bash
./b2 toolset=clang cxxflags='-std=c++03' link=static variant=release threading=multi -j4 stage
```
**Итог:**
```text
clang-darwin.archive bin.v2/libs/wave/build/clang-darwin-21.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_wave.a
common.copy stage/lib/libboost_wave.a
...updated 646 targets...

[exit code: 0]
```

**Полный лог компиляции:** [compilation.log](compilation.log)

---

### Задание 9. Перенос библиотек

**Команда:**
```bash
mkdir -p /Users/igorivanov/boost-libs
find /Users/igorivanov/boost_1_69_0/stage/lib -type f -name "*.a" -exec cp {} /Users/igorivanov/boost-libs/ \;
```

**Результат:** перенесено 36 статических библиотек.

---

### Задание 10. Размер каждого файла

**Команда:**
```bash
du -h /Users/igorivanov/boost-libs/* | sort -h
```

**Полный список:** [lib_sizes.txt](lib_sizes.txt)

---

### Задание 11. Топ-10 самых тяжелых файлов

**Команда:**
```bash
du -h /Users/igorivanov/boost-libs/* | sort -hr | head -10
```
**Вывод:**
```text
2.9M	/Users/igorivanov/boost-libs/libboost_wave.a
2.5M	/Users/igorivanov/boost-libs/libboost_log.a
2.2M	/Users/igorivanov/boost-libs/libboost_log_setup.a
1.5M	/Users/igorivanov/boost-libs/libboost_math_tr1f.a
1.4M	/Users/igorivanov/boost-libs/libboost_unit_test_framework.a
1.4M	/Users/igorivanov/boost-libs/libboost_test_exec_monitor.a
1.4M	/Users/igorivanov/boost-libs/libboost_math_tr1l.a
1.4M	/Users/igorivanov/boost-libs/libboost_math_tr1.a
1.1M	/Users/igorivanov/boost-libs/libboost_regex.a
1.1M	/Users/igorivanov/boost-libs/libboost_locale.a
```

**Полный вывод:** [top10.txt](top10.txt)

**Команда:**
```bash
du -sh /Users/igorivanov/boost-libs
```
**Вывод:**
```text
22M    /Users/igorivanov/boost-libs
```

---

## 3. Публикация отчета

**Команда:**
```bash
git add REPORT.md any_list.txt asio_list.txt compilation.log lib_sizes.txt top10.txt git_clone.log wget.log bootstrap.log README.md .gitignore
git commit -m "Reformat lab01 report"
git push origin main
```

**Ссылка на отчет:** https://github.com/n9s6sstd5h-blip/lab01/blob/main/REPORT.md

---

## 4. Выводы

| Категория | Количество |
|-----------|------------|
| Файлов в корне boost | 12 |
| Всего файлов в boost | 61 191 |
| Заголовочных файлов | 15 208 |
| Файлов .cpp | 13 774 |
| Прочих файлов | 32 209 |
| Упоминаний boost::asio | 17 424 |
| Статических библиотек | 36 |

Boost 1.69 успешно скомпилирован из чистого проекта. Для совместимости со старым кодом Boost на современном Apple clang был явно указан стандарт `-std=c++03`.  
Общий размер перенесенных статических библиотек: **22 МБ**.  
Самая тяжелая библиотека: **libboost_wave.a** (2.9 МБ).

Все большие листинги вынесены в отдельные файлы в репозитории.
