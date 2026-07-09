cmake_minimum_required(VERSION 3.20)
project(maelstrom C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_executable(maelstrom src/main.c)
add_library(chess_core STATIC
    src/board.c
)
target_include_directories(chess_core PUBLIC include/)
# bada bene, la firma è PUBLIC, ciò significa che chess_core riceve automaticamente i file .h contenuti in include/
target_link_libraries(maelstrom PRIVATE chess_core)
# in questo caso la catena di dipendenze si ferma a chess_core, ciò significa che se da main.c vado a utilizzare
# le librerie contenute in include/ allora il compilatore in fase di linking mi darà dei problemi, poichè la
# visibilità è private
