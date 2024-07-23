``` python
from datetime import datetime

  

fecha_modificada = datetime(2003, 7, 14).date()

  

now = datetime.now().date()

  

# Día, mes y (año acortado)

print(fecha_modificada.strftime("%d/%m/%y"))

# Día, mes y (año completo)

print(fecha_modificada.strftime("%d/%m/%Y"))

  

# Horas, minutos y segundos

print(fecha_modificada.strftime("%H:%M:%S"))

  

# Día del año

print(fecha_modificada.strftime("%j"))

  

# Día de la semana

print(fecha_modificada.strftime("%A"))

  

# Nombre del mes (acortado/completo)

print(fecha_modificada.strftime("%h"))

print(fecha_modificada.strftime("%B"))

  

# Representación por defecto de la fecha y la hora en formato estandar según el pais configurado

print(fecha_modificada.strftime("%c"))

# Representación por defecto de solo la fecha en formato estandar según el pais configurado

print(fecha_modificada.strftime("%x"))

# Representación de las horas, minutos, segundos formato estandar

print(fecha_modificada.strftime("%X"))

# AM/PM

print(fecha_modificada.strftime("%p"))
```