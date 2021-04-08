```SHELL
# gdb tutorial

# attach source code
objdump -h .o
# output debug info, and designate path to find source code
# format: /dir + /realtive/path/to/.cpp
dir /path/to/source/dir
set subtitleddir /origin/path /replaced path
# replace /path/in/symbol with /path/on/debug/pc
```
