# lua-cmake

Automatically download and define a cmake-library for lua

## Example usage

```CMake
# CMakeLists.txt

cmake_minimum_required(VERSION 3.20)
project(MyProject VERSION 1.0.0 LANGUAGES C)

include(FetchContent)
FetchContent_Declare(
  lua-cmake
  GIT_REPOSITORY https://github.com/Marth1nus/lua-cmake
  GIT_TAG        master
)
set(LUA_VERSION "5.4.7") # optional specify version
FetchContent_MakeAvailable(lua-cmake)

add_executable(MyProject main.c)
target_link_libraries(MyProject PRIVATE lua)
```

```C
// main.c
#include "lua.h"
#include "lualib.h"
#include "lauxlib.h"

int main()
{
  lua_State *L = luaL_newstate();
  luaL_openlibs(L);
  lua_dostring(L, "print('Hello from lua')");
  lua_close(L);
}
```

## Compile Lua

To create `./lua` and `./luac`

```sh
mkdir -p build
cd build
cmake -DLUA_VERSION="5.4.7" -DLUA_EXECUTABLES=ON ..
cmake --build .
```
