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

> [!CAUTION]
> Aquí ponemos los problemas.
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

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%201%20sin%20bloqueados.png)


<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%202%20pregunta.png)

<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%202%20ya%20bloqueado.png)

<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%203%20pregunta.png)

<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%203%20ya%20desbloqueado.png)

<h2>a</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%204%20usuario%20no%20conectado.png)

<hr>

<h2>Ejercicio 3</h2>

<h3>Realiza un script llamado crearBorrarUsuarios.sh, que nos muestre un menú: <br>
1.- Crear Usuarios.<br>
2.- Borrar Usuarios.<br>
3.- Salir<br>
CrearUsuarios → Crea de forma masiva usuarios almacenados en el fichero
/root/usuarios.csv<br>
Los campos son los siguientes:<br>
- El campo 1 representa el nombre de usuario.<br>
- El campo 2 representa la contraseña.<br>
- El campo 3 representa el nombre.<br>
- El campo 4 representa su primer apellido.<br>
- El campo 5 representa su correo electrónico.<br>
Además, queremos que esas cuentas queden inactivas el 30 de junio de 2024.<br>
BorrarUsuarios → Borra de forma masiva usuarios almacenados en el fichero
/root/usuarios.csv.</h3><br>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

<hr>

<h2>Ejercicio 4</h2>

<h3>Crea en un script llamado crearUsuarios.sh que permita crear usuarios de forma
automática.<br> Indicaciones:<br>
1.- Al script se le pasa dos parámetros:<br>
a) El primer parámetro representa el nombre de un usuario genérico.<br>
b) El segundo parámetro representa el número de usuarios que quiere crearse.<br>
2.- A cada usuario se le asigna la contraseña que coincida con el nombre de usuario.<br>
3.- Al usuario se le obliga a cambiar de contraseña, cuando se loguee.<br>
4.- Se crea un archivo: usuariosCreados-FechaActual.tmp con el nombre de los usuarios
creados y la contraseña asignado, separados por “:”.<br>
5.- El archivo usuariosCreados-FechaActual.tmp tiene que ser mostrado en pantalla tras
la ejecución del scrip
</h3>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

<hr>

<h2>Ejercicio 5</h2>

<h3>
Partimos de que tenemos varios usuarios: usuario1, usuario2, usuario3.<br>
Al usuario1, se le ha establecido una cuota de disco: 40k y 100K (soft y hard
respectivamente).<br>
Realiza un script llamado cuotasUsuarios.sh, que nos copie la cuota del usuario1 a todos
los usuarios cuyo uid >1000 y uid<2000.
</h3>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

















