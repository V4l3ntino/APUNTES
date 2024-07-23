```python
import re

  

regex = r"\d+"

  

text = "Este es el ejercicio 16 publicado 15/04/2024."

  

def find_numbers(text: str) -> list:

    return re.findall(regex, text)

  

print(find_numbers(text=text))

  
  

def validate_email(email: str) -> bool:

    regex = r"\A[\w\.\S\+\-]+@[a-z]+\.[a-z]{3}\Z"

    return bool(re.match(regex, email))

  

print("GMAIL",validate_email("""MOURedev_-+898.asd@cola.net"""))

  

def validate_phone(phone: str) -> bool:

    regex = r"\A\+[\d]{2,3} [\d]{9}\Z"

    return bool(re.match(regex, phone))

  

print("TELEFONO", validate_phone("+34 632361737"))
```