# README #

lua-standalone is a simple launcher application written in C for launching Lua scripts by using the official Lua API.

### How do I build lua-standalone? ###

Currently the repository only contains project files for Visual Studio 2012. A CMake build file will be added soon,
as there's no reason to limit the application to Microsoft Windows.

### How does lua-standalone work? ###

Currently the application will search for a folder with the name 'lua' in the current directory. Inside the folder
it will search for a 'main.lua' file from which it tries to call the function 'main(args)' All arguments with which
lua-standalone was called will be forwarded to Lua in the form of a table.

The repository currently contains the officially Lua 5.1 runtime as well as the LuaJIT runtime. The idea behind that was 
to statically link the debug build of lua-standalone against the Lua 5.1 runtime and the release build against the
LuaJIT runtime as some Lua IDEs (For example Openworlds [Decoda](http://unknownworlds.com/decoda/)) have trouble debugging
Lua scripts when the LuaJIT runtime is used.

### Future plans ###

* Let the user specify what Lua file to run instead of always running './lua/main.lua'
* Adding CMake build files

### Windows Example of using lua-standalone ###

The following Lua script (main.lua):

```
#!lua

function main(args)
 printf("running lua-standalone example!")
 for i, arg in ipairs(args) do
  print("Argument " .. i .. ". : " .. arg")
 end
 printf("finished running lua-standalone example!")
end
```

will produce the following output if it is placed in './lua/'

```
#!
lua-standalone.exe totally a test
 running lua-standalone example!
 Argument 1. totally
 Argument 2. a
 Argument 3. test
 finished running lua-standalone example!
```
