# counter_cpp

- Создаем репозиторий на github.
- Создаем проект на ПК в CLion.
- Создаем папку для клонирования из github.
  В эту папку направляем git bush, правая кнопка и Open Git Bush in here.
- Клонируем в эту папку репозиторий
  git clone https://github.com/dmwgulladmin/counter_cpp.git
  Переносим содержимое склонированого репозитория в папку проекта (фактически привязываем git к проекту), папку с клонируемым репозиторием можно удалить.
- Принцип работы с коммитами:

  *) Создаем ветку для задачи, в CLion можно использовать инструментарий "Git Branches" (правый нижний угол) или
  git branch feature-branch

  *) Переход на созданную ветку
  git switch CC-001

  *) Выполныем поставленную задачу.

  *) Создаем коммит, можно использовать инструменты CLion
  или
  git add .
  или
  git add filename

  *)
  git commit -m "Ваше сообщение коммита"

  *) Коммит оформляем как
  ISSUE#: SEC-001: Название задачи.
  Description: Описание решения задачи.

  *) Делаем push на github, т.к. CLion неродной эта опция в инструментах не работает, делаем через git
  git push origin branch-name

  *) На github мержим в главную ветку ветку задачи, после чего на ПК делаем pull
  git pull

  *) Переходим в основную ветку, делаем новую задачу, как описано выше.

Возможнык проблемы с Github.

Отказ принимать новые ветки.

Решение:

Зашел в другом браузере.


----------

Чтобы установить SDL в среде разработки CLion, нужно выполнить несколько шагов, включая установку SDL, настройку проекта и подключение необходимых библиотек. Вот пошаговое руководство по установке SDL на CLion:

Шаг 1: Установка SDL

Загрузка SDL:

Перейдите на официальный сайт SDL: libsdl.org.

Найдите последнюю версию SDL (например, SDL 2.0) и скачайте архив для вашей операционной системы.

! Особенность скачивайте версию для VS SDL2-devel-2.30.7-VC.zip.

Установка на операционную систему:

Windows:

Распакуйте скачанный архив в удобное место, например, C:\SDL2.  (В этом случае c:\SDL2_2_30_7\)

Шаг 2: Настройка проекта в CLion

Теперь, когда SDL установлен, нужно настроить проект в CLion для использования библиотеки.

Создание нового проекта или открытие существующего проекта:

Запустите CLion и создайте новый проект на CMake или откройте существующий.

Настройка CMakeLists.txt:

Откройте файл CMakeLists.txt в вашем проекте.

Добавьте следующие строки, чтобы включить SDL в ваш проект:

cmake_minimum_required(VERSION 3.15)

project(MySDLProject)

set(CMAKE_CXX_STANDARD 14)

# Укажите путь к SDL2

if (WIN32)

    set(SDL2_PATH "C:/SDL2")

    set(SDL2_INCLUDE_DIR "${SDL2_PATH}/include")

    set(SDL2_LIB_DIR "${SDL2_PATH}/lib/x64")

elseif(APPLE)

    find_package(SDL2 REQUIRED)

    set(SDL2_INCLUDE_DIR "/usr/local/include/SDL2")

    set(SDL2_LIB_DIR "/usr/local/lib")

elseif(UNIX)

    find_package(SDL2 REQUIRED)

endif()

include_directories(${SDL2_INCLUDE_DIR})

# Укажите путь к исполняемым файлам

link_directories(${SDL2_LIB_DIR})

add_executable(MySDLProject main.cpp)

# Связывание SDL2 библиотеки с вашим проектом

if(WIN32)

    target_link_libraries(MySDLProject SDL2main SDL2)

else()

    target_link_libraries(MySDLProject SDL2)

endif()

Добавление пути к заголовочным файлам и библиотекам:

Для Windows: укажите путь, где вы распаковали SDL, например, C:/SDL2.

Шаг 3: Проверка и запуск

Создайте простой пример программы с использованием SDL:

Создайте файл main.cpp с примером, чтобы убедиться, что SDL работает:

#include <SDL.h>
#include <iostream>

int main(int argc, char* argv[]) {
    if (SDL_Init(SDL_INIT_VIDEO) < 0) {
        std::cerr << "SDL не удалось инициализировать! SDL Ошибка: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_Window* window = SDL_CreateWindow("Пример SDL в CLion", SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED, 800, 600, SDL_WINDOW_SHOWN);
    if (window == nullptr) {
        std::cerr << "Не удалось создать окно! SDL Ошибка: " << SDL_GetError() << std::endl;
        SDL_Quit();
        return 1;
    }

    SDL_Delay(3000); // Задержка на 3 секунды

    SDL_DestroyWindow(window);
    SDL_Quit();
    return 0;
}


Запустите сборку и выполните проект:

Нажмите на кнопку сборки (Build) в CLion.

После успешной сборки выполните проект (Run).

Дополнительные шаги для Windows:

Если вы получаете ошибки при запуске исполняемого файла (например, SDL2.dll not found), скопируйте SDL2.dll из папки lib/x64 SDL в папку с исполняемым файлом вашего проекта (обычно cmake-build-debug или cmake-build-release).

Готово!

Теперь ваш проект в CLion настроен для использования SDL, и вы можете начать разработку с использованием этой библиотеки.