```python
from datetime import datetime

import time

import asyncio

  
  
  

async def task(name:str, duration: int):

    print(f"Tarea: {name}. Duración: {duration}s. Inicio: {datetime.now()}")

    await asyncio.sleep(duration)

    print(f"Tarea: {name}. Fin: {datetime.now()}")

  
  

# TAREAS EN PARALELO

  

async def execute_async():

    await asyncio.gather(

    # Primero ejectua estas cuatro tareas en paralelo

    task("A", 1),

    task("B", 7),

    task("C", 2),

    task("D", 3)

    )

    # Luego ejecuta esta última tarea asincrona

    await task("ULTIMO",1)

asyncio.run(execute_async())
```