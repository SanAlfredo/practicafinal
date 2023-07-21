#practicafinal
Tomar en cuenta que las indicaciones son para Sistema Operativo Windows
1. Una vez descargado el proyecto abrir una terminal en la carpeta "/Frontend/final", que esta dentro de la carpeta Practicafinal.
2. Configurar el archivo ".env.example", convertirlo en ".env", el nombre de la Aplicacion es RegistroApp
3. Dentro de la terminal abierta previamente escribir "npm install", para instalar las dependencias.
4. Despues de instalar las dependencias ver la terminal si dice "found 0 vulnerabilities" es que ya terminó.
5. Despues de instalar si pide correr "npm audit", en la terminal, hacerlo, finalmente, si no logra solucionar, es posible que requiera desinstalar materialize-css y instalarlo nuevamente, para ello correr en la terminal:
    * npm uninstall materialize-css
    * npm install materialize-css@next --save
6. Finalmente correr "npm run serve", en la misma terminal ubicada en la carpeta "/Frontend/final"

NOTA: Tomar en cuenta que el backend debe estar funcionando para poder acceder a estas vistas