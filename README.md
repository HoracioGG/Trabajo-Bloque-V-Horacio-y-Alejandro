# Trabajo-Bloque-V-Horacio-y-Alejandro

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/b09273d7dd331b25a497fad692a097ce.gif)

<br>

<h1>Índice</h1>
<ul>
  <li>Ejercicio 1</li>
  <li>Ejercicio 2</li>
  <li>Ejercicio 3</li>
  <li>Ejercicio 4</li>
  <li>Ejercicio 5</li>
</ul>

<br>

<h1>Ejercicio 1</h1>

<h3>
  Realiza un script llamado comprobarApache.sh, que compruebe cada minuto si el
servicio apache2 está activo (running).
Si está parado, entonces: <br> <br>
1.- Introduce una línea: “Error-Apache: Fecha y hora actual” en /root/ApacheError.tmp,
donde FechaActual, representa día, mes, año, hora y minuto. <br><br>
2.- Reinicia el servicio apache2
Para comprobarlo, para el servicio. Ejecuta el script en segundo plano y observa si lo
reinicia y crea el archivo. <br><br>
3.- Además del script, crea una tarea programada, de forma que ese script se ejecute cada
6 horas, todos los días. Y si el ordenador está apagado, se debe ejecutar la próxima vez
que se inicie, transcurrido cinco minutos.
</h3>

<br>

![Tarea programada](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/TareaProgramada.png)

<br>
<br>
<br>

<h2>Script</h2>

![Script](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Script%20.png)

<br>
<br>
<br>

<h2>Reactivación del apache</h2>

![Reactivamos el apache](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Reactivacion%20de%20apache.png)

<br>
<br>
<br>

<h2>Archivo creado</h2>

![Creamos el archivo](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Archivo%20creado.png)

<br>
<br>
<br>

<h2>Activamos el apache</h2>

![Activamos el apache](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apache%20running.png)

<br>
<br>
<br>

<h2>Apache parado</h2>

![Paramos el apache](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apache%20parado.png)

<br>
<br>
<br>

<hr>

<br>
<br>
<br>

<h1>Ejercicio 2</h1>

<br>

<h3>
  Realiza un script llamado usuariosBloqueados.sh, que nos muestre un menú:<br>
1.- Usuarios Bloqueados.<br>
2.- Bloquear un usuario.<br>
3.- Desbloquear usuario.<br>
4.- Cerrar sesión usuario<br>
5.- Salir<br>
Cada opción del menú corresponde con una función.<br>
UsuariosBloqueados → nos muestra en pantalla los usuarios (uid>1000 y <2000) que
tengan la cuenta bloqueada.<br>
BloquearUsuario → Nos pregunta el nombre de un usuario y lo bloqueamos.<br>
DesbloquearUsuario → Nos pregunta el nombre de un usuario y lo desbloqueamos.<br>
CerrarSesion → Nos pregunta el nombre de un usuario, y si el usuario lleva más de 30
minutos (1800 seg) sin actividad, se le cierra la sesión.<br>
</h3>
































