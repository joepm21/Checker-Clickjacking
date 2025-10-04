Ejecutable escrito en Python para comprobar si una página es vulnerable a clickjacking. Al ejecutarlo, validará si la página es vulnerable y se puede enmarcar en un HTML. Si es así, creará un archivo .html adjuntando la página vulnerable.

Lo descargamos y le damos permisos como ejecutable

    git clone https://github.com/joepm21/Checker-Clickjacking.git    
    cd Checker-Clickjacking 
    chmod +x checker_clickjacking
    
![image](https://github.com/user-attachments/assets/f2200a79-e289-4cf1-a459-413d1e21ce49)

Ejecutamos 
  
    ./checker_clickjacking {URL}
    
![image](https://github.com/user-attachments/assets/3f262d4b-7017-484b-8305-990ad8dae475)

![image](https://github.com/user-attachments/assets/24e68df4-4deb-4847-94e3-fe1807fe6cd5)
