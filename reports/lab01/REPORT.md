# Лабораторная работа 01

Репозиторий: https://github.com/n9s6sstd5h-blip/lab01

Исходное задание: https://github.com/tp-labs/lab01

## Важное про полноту вывода

Полный вывод каждой выполненной команды сохранён без сокращений в каталоге [logs](logs). В таблице ниже для каждой команды дана отдельная ссылка на полный лог. В отчёте также приведены ключевые результаты по пунктам задания.

## Окружение

Работа выполнялась локально на macOS в каталоге `/Users/igorivanov/Documents/lab01`. Boost был скачан через `wget`, распакован в `/Users/igorivanov/boost_1_69_0` и собран из чистого дерева. Финальная успешная сборка выполнена после повторной распаковки архива командой:

`./b2 toolset=clang cxxflags='-std=c++03' link=static variant=release threading=multi -j4 stage`

Причина явного `-std=c++03`: Boost 1.69 старый, а современный Apple clang при стандартной сборке падал на устаревших конструкциях Boost.MPL. Неудачные попытки также сохранены полностью в логах `017`, `024`, `031` и `038`; финальная чистая сборка с кодом 0 находится в `045_build_boost_cpp03_clean.log`.

## Ответы по homework

1. Boost скачан через `wget`: полный вывод в [008_wget_boost.log](logs/008_wget_boost.log).
2. Архив распакован в `/Users/igorivanov/boost_1_69_0`: финальная чистая распаковка в [043_extract_boost_clean_cpp03.log](logs/043_extract_boost_clean_cpp03.log).
3. Количество файлов в `/Users/igorivanov/boost_1_69_0` без вложенных директорий: `12`.
4. Количество файлов с вложенными директориями: `61191`.
5. Распределение типов файлов:

```text
headers    15803
cpp    13774
other    31614
```

6. Полные пути до `any.hpp`:

```text
/Users/igorivanov/boost_1_69_0/boost/fusion/include/any.hpp
/Users/igorivanov/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
/Users/igorivanov/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
/Users/igorivanov/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
/Users/igorivanov/boost_1_69_0/boost/proto/detail/any.hpp
/Users/igorivanov/boost_1_69_0/boost/type_erasure/any.hpp
/Users/igorivanov/boost_1_69_0/boost/hana/fwd/any.hpp
/Users/igorivanov/boost_1_69_0/boost/hana/any.hpp
/Users/igorivanov/boost_1_69_0/boost/any.hpp
/Users/igorivanov/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
```

7. Все файлы, где встречается `boost::asio`, выведены полностью в [015_find_boost_asio_refs.log](logs/015_find_boost_asio_refs.log). Лог содержит полный список без сокращений.
8. Boost собран из чистого проекта: успешный полный лог в [045_build_boost_cpp03_clean.log](logs/045_build_boost_cpp03_clean.log).
9. Статические библиотеки перенесены в `/Users/igorivanov/boost-libs`: полный вывод в [046_copy_static_libs_cpp03.log](logs/046_copy_static_libs_cpp03.log). Всего перенесено 36 файлов `.a`.
10. Размер каждого файла в `/Users/igorivanov/boost-libs` приведён полностью в [047_du_each_static_lib_cpp03.log](logs/047_du_each_static_lib_cpp03.log).
11. Топ-10 самых тяжёлых статических библиотек:

```text
$ cd /Users/igorivanov
$ du -h boost-libs/* | sort -hr | head -10
2.9M	boost-libs/libboost_wave.a
2.5M	boost-libs/libboost_log.a
2.2M	boost-libs/libboost_log_setup.a
1.5M	boost-libs/libboost_math_tr1f.a
1.4M	boost-libs/libboost_unit_test_framework.a
1.4M	boost-libs/libboost_test_exec_monitor.a
1.4M	boost-libs/libboost_math_tr1l.a
1.4M	boost-libs/libboost_math_tr1.a
1.1M	boost-libs/libboost_regex.a
1.1M	boost-libs/libboost_locale.a

[exit code: 0]
```

## Хвост успешной сборки Boost

```text
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include/_stdio.h:298:1: note: 'vsprintf' has been explicitly marked deprecated here
  298 | __deprecated_msg("This function is provided for compatibility reasons only.  Due to security concerns inherent in the design of sprintf(3), it is highly recommended that you use vsnprintf(3) instead.")
      | ^
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include/sys/cdefs.h:227:48: note: expanded from macro '__deprecated_msg'
  227 |         #define __deprecated_msg(_msg) __attribute__((__deprecated__(_msg)))
      |                                                       ^
12 warnings generated.
clang-darwin.archive bin.v2/libs/wave/build/clang-darwin-21.0/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_wave.a
common.copy stage/lib/libboost_wave.a
...updated 646 targets...

[exit code: 0]
```

## Размеры всех статических библиотек

```text
$ cd /Users/igorivanov
$ du -h boost-libs/* | sort -h
4.0K	boost-libs/libboost_atomic.a
4.0K	boost-libs/libboost_exception.a
4.0K	boost-libs/libboost_stacktrace_noop.a
4.0K	boost-libs/libboost_system.a
 12K	boost-libs/libboost_stacktrace_basic.a
 20K	boost-libs/libboost_stacktrace_addr2line.a
 24K	boost-libs/libboost_timer.a
 40K	boost-libs/libboost_random.a
 44K	boost-libs/libboost_context.a
 48K	boost-libs/libboost_coroutine.a
 52K	boost-libs/libboost_date_time.a
 92K	boost-libs/libboost_prg_exec_monitor.a
 92K	boost-libs/libboost_type_erasure.a
112K	boost-libs/libboost_container.a
116K	boost-libs/libboost_chrono.a
140K	boost-libs/libboost_math_c99.a
140K	boost-libs/libboost_math_c99l.a
144K	boost-libs/libboost_math_c99f.a
168K	boost-libs/libboost_filesystem.a
176K	boost-libs/libboost_thread.a
180K	boost-libs/libboost_contract.a
208K	boost-libs/libboost_iostreams.a
480K	boost-libs/libboost_wserialization.a
712K	boost-libs/libboost_serialization.a
772K	boost-libs/libboost_graph.a
908K	boost-libs/libboost_program_options.a
1.1M	boost-libs/libboost_locale.a
1.1M	boost-libs/libboost_regex.a
1.4M	boost-libs/libboost_math_tr1.a
1.4M	boost-libs/libboost_math_tr1l.a
1.4M	boost-libs/libboost_test_exec_monitor.a
1.4M	boost-libs/libboost_unit_test_framework.a
1.5M	boost-libs/libboost_math_tr1f.a
2.2M	boost-libs/libboost_log_setup.a
2.5M	boost-libs/libboost_log.a
2.9M	boost-libs/libboost_wave.a

[exit code: 0]
```

## Полные логи команд

| N | Command | Full output |
|---:|---|---|
| 001 | `git clone https://github.com/n9s6sstd5h-blip/lab01.git /Users/igorivanov/Documents/lab01` | [001_git_clone_user.log](logs/001_git_clone_user.log) |
| 002 | `export GITHUB_USERNAME=n9s6sstd5h-blip; printf '%s\n' "${GITHUB_USERNAME}"` | [002_export_github_username.log](logs/002_export_github_username.log) |
| 003 | `export LAB_NUMBER=01; printf '%s\n' "${LAB_NUMBER}"` | [003_export_lab_number.log](logs/003_export_lab_number.log) |
| 004 | `pwd` | [004_pwd_workspace.log](logs/004_pwd_workspace.log) |
| 005 | `pwd` | [005_pwd_user_dir.log](logs/005_pwd_user_dir.log) |
| 006 | `git clone https://github.com/tp-labs/lab01 tasks/lab01` | [006_clone_assignment.log](logs/006_clone_assignment.log) |
| 007 | `mkdir -p reports/lab01 && cp tasks/lab01/README.md reports/lab01/REPORT.md` | [007_copy_assignment_readme.log](logs/007_copy_assignment_readme.log) |
| 008 | `wget -O boost_1_69_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz` | [008_wget_boost.log](logs/008_wget_boost.log) |
| 009 | `rm -rf boost_1_69_0 boost-libs` | [009_remove_old_boost.log](logs/009_remove_old_boost.log) |
| 010 | `tar -xzf /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/boost_1_69_0.tar.gz` | [010_extract_boost.log](logs/010_extract_boost.log) |
| 011 | `find boost_1_69_0 -maxdepth 1 -type f | wc -l` | [011_count_top_level_files.log](logs/011_count_top_level_files.log) |
| 012 | `find boost_1_69_0 -type f | wc -l` | [012_count_all_files.log](logs/012_count_all_files.log) |
| 013 | `printf 'headers '; find boost_1_69_0 -type f \( -name '*.h' -o -name '*.hpp' -o -name '*.ipp' \) | wc -l; printf 'cpp '; find boost_1_69_0 -type f -name '*.cpp' | wc -l; printf 'other '; find boost_1_69_0 -type f ! \( -name '*.h' -o -name '*.hpp' -o -name '*.ipp' -o -name '*.cpp' \) | wc -l` | [013_count_file_types.log](logs/013_count_file_types.log) |
| 014 | `find "$(pwd)/boost_1_69_0" -name any.hpp` | [014_find_any_hpp.log](logs/014_find_any_hpp.log) |
| 015 | `grep -R -l 'boost::asio' boost_1_69_0` | [015_find_boost_asio_refs.log](logs/015_find_boost_asio_refs.log) |
| 016 | `./bootstrap.sh` | [016_bootstrap_boost.log](logs/016_bootstrap_boost.log) |
| 017 | `./b2 link=static variant=release threading=multi -j4 stage` | [017_build_boost_clean.log](logs/017_build_boost_clean.log) |
| 018 | `mkdir -p boost-libs && find boost_1_69_0/stage/lib -type f -name '*.a' -exec cp {} boost-libs/ \;` | [018_copy_static_libs.log](logs/018_copy_static_libs.log) |
| 019 | `du -h boost-libs/* | sort -h` | [019_du_each_static_lib.log](logs/019_du_each_static_lib.log) |
| 020 | `du -h boost-libs/* | sort -hr | head -10` | [020_top10_static_libs.log](logs/020_top10_static_libs.log) |
| 021 | `rm -rf boost_1_69_0 boost-libs` | [021_remove_failed_boost_tree.log](logs/021_remove_failed_boost_tree.log) |
| 022 | `tar -xzf /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/boost_1_69_0.tar.gz` | [022_extract_boost_clean_retry.log](logs/022_extract_boost_clean_retry.log) |
| 023 | `./bootstrap.sh` | [023_bootstrap_boost_clean_retry.log](logs/023_bootstrap_boost_clean_retry.log) |
| 024 | `./b2 toolset=clang link=static variant=release threading=multi -j4 stage` | [024_build_boost_clang_clean.log](logs/024_build_boost_clang_clean.log) |
| 025 | `mkdir -p boost-libs && find boost_1_69_0/stage/lib -type f -name '*.a' -exec cp {} boost-libs/ \;` | [025_copy_static_libs_after_success.log](logs/025_copy_static_libs_after_success.log) |
| 026 | `du -h boost-libs/* | sort -h` | [026_du_each_static_lib_after_success.log](logs/026_du_each_static_lib_after_success.log) |
| 027 | `du -h boost-libs/* | sort -hr | head -10` | [027_top10_static_libs_after_success.log](logs/027_top10_static_libs_after_success.log) |
| 028 | `rm -rf boost_1_69_0 boost-libs` | [028_remove_second_failed_boost_tree.log](logs/028_remove_second_failed_boost_tree.log) |
| 029 | `tar -xzf /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/boost_1_69_0.tar.gz` | [029_extract_boost_clean_final.log](logs/029_extract_boost_clean_final.log) |
| 030 | `./bootstrap.sh` | [030_bootstrap_boost_clean_final.log](logs/030_bootstrap_boost_clean_final.log) |
| 031 | `./b2 toolset=clang cxxflags='-Wno-enum-constexpr-conversion' link=static variant=release threading=multi -j4 stage` | [031_build_boost_clang_warning_flag_clean.log](logs/031_build_boost_clang_warning_flag_clean.log) |
| 032 | `mkdir -p boost-libs && find boost_1_69_0/stage/lib -type f -name '*.a' -exec cp {} boost-libs/ \;` | [032_copy_static_libs_final.log](logs/032_copy_static_libs_final.log) |
| 033 | `du -h boost-libs/* | sort -h` | [033_du_each_static_lib_final.log](logs/033_du_each_static_lib_final.log) |
| 034 | `du -h boost-libs/* | sort -hr | head -10` | [034_top10_static_libs_final.log](logs/034_top10_static_libs_final.log) |
| 035 | `rm -rf boost_1_69_0 boost-libs` | [035_remove_third_failed_boost_tree.log](logs/035_remove_third_failed_boost_tree.log) |
| 036 | `tar -xzf /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/boost_1_69_0.tar.gz` | [036_extract_boost_clean_without_wave.log](logs/036_extract_boost_clean_without_wave.log) |
| 037 | `./bootstrap.sh` | [037_bootstrap_boost_without_wave.log](logs/037_bootstrap_boost_without_wave.log) |
| 038 | `./b2 toolset=clang --without-wave link=static variant=release threading=multi -j4 stage` | [038_build_boost_without_wave_clean.log](logs/038_build_boost_without_wave_clean.log) |
| 039 | `mkdir -p boost-libs && find boost_1_69_0/stage/lib -type f -name '*.a' -exec cp {} boost-libs/ \;` | [039_copy_static_libs_without_wave.log](logs/039_copy_static_libs_without_wave.log) |
| 040 | `du -h boost-libs/* | sort -h` | [040_du_each_static_lib_without_wave.log](logs/040_du_each_static_lib_without_wave.log) |
| 041 | `du -h boost-libs/* | sort -hr | head -10` | [041_top10_static_libs_without_wave.log](logs/041_top10_static_libs_without_wave.log) |
| 042 | `rm -rf boost_1_69_0 boost-libs` | [042_remove_boost_tree_for_cpp03.log](logs/042_remove_boost_tree_for_cpp03.log) |
| 043 | `tar -xzf /Users/igorivanov/Documents/lab01/n9s6sstd5h-blip/workspace/boost_1_69_0.tar.gz` | [043_extract_boost_clean_cpp03.log](logs/043_extract_boost_clean_cpp03.log) |
| 044 | `./bootstrap.sh` | [044_bootstrap_boost_cpp03.log](logs/044_bootstrap_boost_cpp03.log) |
| 045 | `./b2 toolset=clang cxxflags='-std=c++03' link=static variant=release threading=multi -j4 stage` | [045_build_boost_cpp03_clean.log](logs/045_build_boost_cpp03_clean.log) |
| 046 | `mkdir -p boost-libs && find boost_1_69_0/stage/lib -type f -name '*.a' -exec cp {} boost-libs/ \;` | [046_copy_static_libs_cpp03.log](logs/046_copy_static_libs_cpp03.log) |
| 047 | `du -h boost-libs/* | sort -h` | [047_du_each_static_lib_cpp03.log](logs/047_du_each_static_lib_cpp03.log) |
| 048 | `du -h boost-libs/* | sort -hr | head -10` | [048_top10_static_libs_cpp03.log](logs/048_top10_static_libs_cpp03.log) |
