# Lua 5.3.6 Native Package for C++

This is a **NuGet package** that provides **Lua 5.3.6** binaries and headers for **native C++** development on Windows. By installing this package, you can seamlessly integrate Lua scripting into your MSBuild-based C++ projects without manual include, library, or DLL copying tasks.

## Key Features

- **Lua 5.3.6** support: Headers (`lua.h`, `lauxlib.h`, `lualib.h`) and compiled binaries (`lua53.dll`, `lua53.lib` or `liblua53.a`)
- **Automatic linker configuration**: A `.targets` file is included that sets up library paths and dependencies
- **Post-build DLL copy**: `lua53.dll` is copied to your output folder (e.g., `Debug` or `Release`) so you can run your project right away
- **Native package**: Marked with `<packageType name="native" />` to avoid .NET framework warnings
- **Compatible** with Visual Studio 2017 or later, and can be used in x64 (and optionally x86) builds

## Installation

**Visual Studio**  
- Right-click your project → **Manage NuGet Packages…**  
- Select your package source (nuget.org or a local feed)  
- Search for **Lua53Package** (or whichever ID you used) and **Install**  

**Command Line**  
- nuget install Lua53Package
- or
- dotnet add package Lua53Package

## Usage

1. **Include the Lua headers**:

~~~cpp
#include <lua.h>
#include <lauxlib.h>
#include <lualib.h>
~~~

2. **Linking**  
   - No manual config needed — the included `.targets` automatically adds `AdditionalIncludeDirectories` and `AdditionalLibraryDirectories`  
   - `lua53.dll` gets copied to your build output folder on build completion  
   - If you have x86 builds, ensure you place the 32-bit DLL and import lib in `lib\native\x86`

3. **Example**:

~~~cpp
#include <lua.h>
#include <lauxlib.h>
#include <lualib.h>
#include <iostream>

int main()
{
    lua_State* L = luaL_newstate();
    luaL_openlibs(L);

    const char* script = "print('Lua 5.3.6 is running in C++!')";
    if (luaL_dostring(L, script) != LUA_OK) {
        std::cerr << lua_tostring(L, -1) << std::endl;
        lua_pop(L, 1);
    }

    lua_close(L);
    return 0;
}
~~~

## Requirements

- **Visual Studio 2017** or newer (or an MSBuild-compatible environment)  
- **Windows (x64 or x86)**  
- **Lua 5.3.6** binaries included (MIT license)

## License

Lua 5.3.6 is distributed under the [MIT license](https://www.lua.org/license.html). This package redistributes the Lua binaries as provided by the Lua authors, with no modifications. Use is subject to the same MIT terms.

## Contributing

- Fork this package’s repository if available  
- Update `.nuspec` or `.targets` for improvements (e.g., new Lua versions)  
- Submit a pull request or contact the maintainer for more details

## Contact

- Official Lua website: [lua.org](https://www.lua.org/)  
- Maintainer: [Your Name / Organization]  
- Issues and pull requests are welcome
