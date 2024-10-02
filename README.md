# $${\color{lightblue}2D-Platformer-Engine}$$
De grunnleggende filene som trengs for å lage et raylib prosjekt. Prosjektet er satt opp for å kunne bruke src og include mapper og bruker Cmake for compiling.

## CMake compiling
````
1  mkdir build && cd build

2  cmake .. -Wno-dev

3  cmake --build .
````

Dette skal compile programmet og legge en .exe fil under ./build/debug

Flytt *.exe filen til source dir - eks. _2D-Platformer-Engine_


## Nye mapper/dir
Legg til nye mapper som inneholder *.cpp eller *.h filer i _CMakeList.txt_ på denne måten:
````
include_directories(
    "${PROJECT_SOURCE_DIR}/include"

    "${PROJECT_SOURCE_DIR}/include/NY-MAPPE"
)
file(GLOB all_SRCS
    "${PROJECT_SOURCE_DIR}/include/*.h"
    "${PROJECT_SOURCE_DIR}/src/*.cpp"

    "${PROJECT_SOURCE_DIR}/src/NY-MAPPE/*.cpp"
)

````
