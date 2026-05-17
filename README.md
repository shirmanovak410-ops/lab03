# Lab03
## Tutorial
В рамках выполнения данной лабораторной работы мною были выполнены все команды из tutorial:
1) Скопирован репозиторий из lab02:
```bash
$ git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03
Клонирование в «projects/lab03»...
remote: Enumerating objects: 19, done.
remote: Counting objects: 100% (19/19), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 19 (delta 2), reused 12 (delta 0), pack-reused 0 (from 0)
Получение объектов: 100% (19/19), готово.
Определение изменений: 100% (2/2), готово.
$ cd projects/lab03
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
```
2) Выполнена ручная компиляция:
```bash
$ g++ -std=c++11 -I./include -c sources/print.cpp
$ nm print.o | grep print
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000026 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
```
```bash
$ ar rvs print.a print.o
ar: создаётся print.a
a - print.o
```
```bash
$ g++ -std=c++11 -I./include -c examples/example1.cpp
$ g++ example1.o print.a -o example1
$ ./example1 && echo
hello
```
```bash
$ g++ -std=c++11 -I./include -c examples/example2.cpp
$ nm example2.o
0000000000000000 V DW.ref.__gxx_personality_v0
                 U __gxx_personality_v0
0000000000000000 T main
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct


$ ./example2
cat log.txt && echo
hello
```
3) Создан CMakeLists.txt:
```bash
$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)
project(print)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_executable(example1 ${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 ${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
target_link_libraries(example1 print)
target_link_libraries(example2 print)
```
4) Произведена автоматическая сборка проекта и протестированы функции файлов examples:
```bash
$ cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
ksu@skalab3:~/shirmanovak410-ops/workspace/projects/lab03$ cmake --build _build --target example1
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[100%] Linking CXX executable example1
[100%] Built target example1
ksu@skalab3:~/shirmanovak410-ops/workspace/projects/lab03$ cmake --build _build --target example2
[ 50%] Built target print
[ 75%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
```
5) Скопирован CMakeLists.txt из репозитория лабы и выполнена сборка с его помощью:
```bash
$ cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/include
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake

$ tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
```
6) Этот CMakeLists.txt закоммичен на данный репозиторий
## Homework 03
1) Были скопированы необходимые папки для выполнения ДЗ в исходный репозиторий:
```bash
$ cd ~/shirmanovak410-ops/workspace/projects/lab03
$ git clone https://github.com/tp-labs/lab03.git ~/temp_tp_lab03
$ cp -r ~/temp_tp_lab03/formatter_lib .
$ cp -r ~/temp_tp_lab03/formatter_ex_lib .
$ cp -r ~/temp_tp_lab03/solver_lib .
$ cp -r ~/temp_tp_lab03/solver_application .
```
2) Созданы недостающие CMakeLists.txt в папках formatter_lib, formatter_ex_lib, solver_lib:
```bash
$ cat > formatter_lib/CMakeLists.txt << 'EOF'
> add_library(formatter STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/formatter.cpp)
target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
$ cat > formatter_ex_lib/CMakeLists.txt << 'EOF'
> add_library(formatter_ex STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(formatter_ex formatter)
EOF
$ cat > solver_lib/CMakeLists.txt << 'EOF'
> add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/solver.cpp)
target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
```
3) Созданы недостающие CMakeLists.txt в папках hello_world_application и solver_application:
```bash
$ cat > hello_world_application/CMakeLists.txt << 'EOF'
> add_executable(hello_world hello_world.cpp)
target_link_libraries(hello_world formatter_ex)
EOF
$ cat > solver_application/solver.cpp << 'EOF
>  #include <iostream>

#include "formatter_ex.h"
#include "solver.h"

int main()
{
    float a = 0;
    float b = 0;
    float c = 0;

    std::cin >> a >> b >> c;

    float x1 = 0;
    float x2 = 0;

    try
    {
        solve(a, b, c, x1, x2);

        formatter(std::cout, "x1 = " + std::to_string(x1));
        formatter(std::cout, "x2 = " + std::to_string(x2));
    }
    catch (const std::logic_error& ex)
    {
        formatter(std::cout, ex.what());
    }

    return 0;
}
> EOF
```
4) Обновлён CMakeLists.txt (основной):
```bash
$ cat > CMakeLists.txt << 'EOF'
> cmake_minimum_required(VERSION 3.10)
project(print)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
> add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)
> add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
> add_executable(solver solver_application/solver.cpp)
target_link_libraries(solver formatter_ex solver_lib)

add_executable(hello_world hello_world_application/hello_world.cpp)
target_link_libraries(hello_world formatter_ex)
> install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
> install(TARGETS solver hello_world
    RUNTIME DESTINATION bin
)
EOF
)
```
5) Проекты был собраны и протестированы:
 ```bash
$ rm -rf _build
$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.9s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ksu/shirmanovak410-ops/workspace/projects/lab03/_build
$ cmake --build _build
[ 10%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 20%] Linking CXX static library libprint.a
[ 20%] Built target print
[ 30%] Building CXX object solver_lib/CMakeFiles/solver_lib.dir/sources/solver.cpp.o
[ 40%] Linking CXX static library libsolver_lib.a
[ 40%] Built target solver_lib
[ 50%] Building CXX object formatter_lib/CMakeFiles/formatter.dir/sources/formatter.cpp.o
[ 60%] Linking CXX static library libformatter.a
[ 60%] Built target formatter
[ 70%] Building CXX object formatter_ex_lib/CMakeFiles/formatter_ex.dir/sources/formatter_ex.cpp.o
[ 80%] Linking CXX static library libformatter_ex.a
[ 80%] Built target formatter_ex
[ 90%] Building CXX object CMakeFiles/solver.dir/solver_application/solver.cpp.o
[100%] Linking CXX executable solver
[100%] Built target solver
$ ./_build/solver
1 -3 2
Formatter: x1 = 1.000000
Formatter: x1 = 1.000000
Formatter: x2 = 2.000000
Formatter: x2 = 2.000000
```
```bash
$ cmake --build _build
[ 16%] Built target print
[ 33%] Built target solver_lib
[ 50%] Built target formatter
[ 66%] Built target formatter_ex
[ 83%] Built target solver
[ 91%] Building CXX object CMakeFiles/hello_world.dir/hello_world_application/hello_world.cpp.o
[100%] Linking CXX executable hello_world
[100%] Built target hello_world
$ ./_build/hello_world
Formatter: hello, world!
```
