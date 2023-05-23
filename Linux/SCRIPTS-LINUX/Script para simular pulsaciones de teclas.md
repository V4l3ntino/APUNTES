----
- Tags: #Linux #Script #simular-teclas
----------
```bash
#!/bin/bash

xdotool type "Hellow World" # escribir la palabra
sleep 5
xdotool key --clearmodifiers "ctrl+alt+F2" 2>/dev/null #presionar una combinación de teclas
```



