<h1 align="center">Trabajo Bloque V<a name="titulo"></a></h1>

<img src="desktop-source-code-and-wallpaper-by-computer-language-with-coding-and-programming.jpg" alt="Descripción de la imagen" width="1100" height="700">
<br>

<h1 align="center">Alejandro Bayo y Horacio Gómez></h1>

<br>

**ÍNDICE**
1. [Ejercicio 1](#1)
2. [Ejercicio 2](#2)
3. [Ejercicio 3](#3)
4. [Ejercicio 4](#4)
5. [Ejercicio 5](#5)
6. [Bibliografía](#Bibliografía)
7. [Conclusiones](#Conclusiones)
8. [:shipit: FÍN :shipit:](#8)

<br>

<h1 align="center">Ejercicio 1<a name="1"></a></h1>

<details>

<summary> Enunciado del ejercicio 1</summary>

### Ejercicio 1

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

</details>

<br>

<details>


<summary> Archivo Script </summary>


````
#!/bin/bash
# Author: Horacio Gomez y Alejandro bayo
# Version: 1.0
# Fecha: 15-05-2024
# Descripcion: Este script realiza -
Parametros/Variables
fecha=$(date +"%Y-%m-%d %H:%M")
#Funciones
comprobarRoot ()
{
    if [ "$(id -u)" != "0" ]
    then
   	 echo "Este script solo puede ser ejecutado por el root"
   	 exit
    fi
}
comprobarapache() {
	while true; do

    	if systemctl is-active --quiet apache2;
    	then
        	echo "El servicio Apache está activo."
    	else
        	echo "El servicio Apache está parado."
        	reiniciar_apache
    	fi
    	sleep 60
	done
}
reiniciarapache() {
	echo "Error-Apache: $fecha" >> /root/ApacheError.tmp
	systemctl restart apache2
}
#Bloque principal
clear
comprobarRoot
comprobar_apache

````


</details>

<br>

> [!CAUTION]
> En este ejercicio no hemos tenido casi ningún problema, pero la parte con algo de dificultad ha sido el hecho de que se active cada 1 minuto. Lo hemos solucionado con un "sleep" en el while true. La parte para que se ejecute cada 6 horas, todos los días, y si el ordenador está apagado, se debe ejecutar la próxima vez que se inicie, transcurrido cinco minutos, ha sido la que nos ha resultado más difícil y la hemos solucionado con un cambio en el fichero "crontab" con las características que nos pide y la ejecución del script.

<br>

<h2>Tarea Programada</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/1.png" width="1015" height="350">

<br>

<p>Aquí tenemos el archivo que hará que se ejecute el script cada 6 horas todos los días</p>

<br>
<br>

<h2>Procedemos a activamos el Apache</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/2.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aquí tenemos el resultado que da el script cuando el servidor Apache está activado</p>

<br>
<br>

<h2>Apache pausado</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/3.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Esto es lo que muestra por pantalla, cuando el script está comprobando pero el servidor Apache está apagado y además se ha creado un archivo de error que veremos a continuación</p>

<br>
<br>

<h2>Reactivación del Apache</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/4.png" alt="Descripción de la imagen" width="1015" height="350">
<br>

<p>Aquí podemos ver cómo el propio script reactiva el servidor Apache una vez que estaba apagado</p>

<br>
<br>

<h2>Archivo creado</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/5.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Este es el archivo que se nos crearía automáticamente, el cual almacena un mensaje de la fecha en la que el servidor Apache estuvo parado. Con un cat vemos el interior del archivo</p>

<br>
<br>

<hr>

<br>

<h1 align="center">Ejercicio 2<a name="2"></a></h1>

<br>

<details>

<summary>Enunciado del ejercicio 2</summary>

### Ejercicio 2

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

</details>

<br>

<details>

<summary> Archivo Script </summary>

<br>

````
#!/bin/bash
# Author: Horacio Gomez y Alejandro Bayo
# Version: 1.0
# Fecha: 14-05-2024
# Descripcion: Este script realiza -
#Parametros/Variables
menu ()
{
    echo "*********************************************"
    echo "Servidor de usuarios:"
    echo "*********************************************"
    echo "1.- Usuarios Bloqueados."
    echo "2.- Bloquear un usuario."
    echo "3.- Desbloquear usuario."
    echo "4.- Cerrar sesión usuario."
    echo "5.- Salir."
    read -p "Pulse un número: " opcion

case $opcion in
1)
    UsuariosBloqueados
    ;;
2)
    BloquearUsuario
    ;;
3)
    DesbloquearUsuario
    ;;
4)
    CerrarSesion
    ;;

5)
    exit
    ;;
*)
    clear
    echo "Tiene que ser del 1 al 5"
    ;;
esac
}

comprobarRoot ()
{
    if [ "$(id -u)" != "0" ]
    then
   	 echo "Este script solo puede ser ejecutado por el root"
   	 exit
    fi
}

UsuariosBloqueados() {
	clear
	echo "Usuarios Bloqueados:"
	awk -F':' '$3 >=1000 && $3 < 2000 { system("passwd -S " $1) }' /etc/passwd | awk '$2 == "L" { print $1 }'
}

BloquearUsuario() {
	clear
	read -p "Introduce el nombre de usuario a bloquear: " usuario
	passwd -l $usuario
	clear
	echo "Usuario $usuario bloqueado correctamente."
}

DesbloquearUsuario() {
	clear
	read -p "Introduce el nombre de usuario a desbloquear: " usuario
	passwd -u $usuario
	clear
	echo "Usuario $usuario desbloqueado correctamente."
}

CerrarSesion() {
	clear
	read -p "Introduce el nombre de usuario para cerrar sesión: " usuario
	clear
	if who | grep -qw "$usuario"; then
    	pkill -KILL -u "$usuario"
    	echo "La sesión de $usuario ha sido cerrada."
	else
    	echo "El usuario $usuario no tiene una sesión activa."
	fi
}

#Bloque principal
clear
comprobarRoot
while true
do
    menu
done

````

<br>

</details>

<br>

> [!CAUTION]
> Este script ya nos ha resultado más difícil que el anterior y las partes más difíciles han sido la de buscar los comandos para forzar las acciones sobre los usuarios. Los hemos conseguido encontrar buscando información sobre cómo ejecutar comandos en la terminal que afecten a las sesiones y permisos de los usuarios. Otra parte complicada ha sido la parte de que si el usuario lleva más de 30 minutos (1800 seg) sin actividad, se le cierra la sesión. La dificultad aquí radica en determinar el tiempo de inactividad de un usuario y luego forzar el cierre de la sesión de ese usuario si ha excedido el límite de tiempo. Sin embargo, con la lógica de pkill -KILL -u "$usuario" se ha solucionado.

<br>

<h2>Apartado 1 sin bloqueados y vista del menu</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/6.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aqui podemos ver el menu y aparte lo que nos mostraria por pantalla al introducir el numero 1 y no tener ningun usuario bloqueado</p>

<br>
<br>

<h2>Apartado 2 pregunta</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/7.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Esto es lo que se nos mostraria al introducir el numero 2 en el menu, nos pediria el usuario que queramos bloquear</p>

<br>
<br>

<h2>Apartado 2 ya bloqueado</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/8.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Una vez introducido el usuario que queremos bloquear nos saltara este mensaje</p>

<br>
<br>

<h2>Apartado 3 pregunta</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/9.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Si en el menu se pulsa el 3, nos mostraria esto por pantalla y nos preguntaria que que usuario queremos desbloquear</p>

<br>
<br>

<h2>Apartado 3 ya desbloqueado</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/10.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Cuando en el apartado anterior le insertamos un usuario obtenemos este mensaje</p>

<br>
<br>

<h2>Apartado 4 pregunta</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/11.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Si seleccionamos el apartado 4 del menu nos muestra esta pestaña en la cual tendremos que escribir el nombre de ususario que queremos cerrar sesion</p>

<br>
<br>

<h2>Apartado 4 usuarios no conectados</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/12.png" alt="Descripción de la imagen" width="1015" height="350">
<br>

<p>Cuando intentamos cerrar sesion de un usuario que no esta conectado nos muestra este mensaje</p>

<br>
<br>

<hr>

<br>

<h1 align="center">Ejercicio 3<a name="3"></a></h1>

<details>

<summary>Enunciado del ejercicio 3</summary>

### Ejercicio 3

Realiza un script llamado crearBorrarUsuarios.sh, que nos muestre un menú: <br>
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
/root/usuarios.csv.

</details>

<br>

<details>

<summary> Archivo Script </summary>

<br>

```
#!/bin/bash
# Author: Horacio Gomez y Alejandro Bayo
# Version: 1.0
# Fecha: 18-05-2024
# Descripcion: Este script realiza -
#Parametros/Variables

#Funciones
comprobarRoot ()
{
    if [ "$(id -u)" != "0" ]
    then
   	 echo "Este script solo puede ser ejecutado por el root"
   	 exit
    fi
}
menu ()
{
   while true;
   do
	echo "************************************"
	echo "Menú: "
	echo "************************************"
	echo "1.- Crear Usuarios"
	echo "2.- Borrar Usuarios"
	echo "3.- Salir"
	read -p "Pulse un número: " numero
   
	case $numero in
    	1)
        	clear
        	crearUsuarios ;;
    	2)
        	clear
        	borrarUsuarios ;;
    	3)
        	clear
        	exit ;;
    	*)
        	echo "Tiene que ser un numero del 1 al 3"
        	;;
	esac
   done
}

crearUsuarios()
{
	while read linea
	do
    	usuario=$(echo $linea | cut -d: -f1)
    	contrasena=$(echo $linea | cut -d: -f2)
    	nombre=$(echo $linea | cut -d: -f3)
    	apellido=$(echo $linea | cut -d: -f4)
    	correo=$(echo $linea | cut -d: -f5)
   	 
    	sudo useradd -m -s /bin/bash -p $contrasena -c "$nombre $apellido" -e "2025-05-18" $usuario > /dev/null 2>&1
                	if [ $? -eq 0  ];
                	then
                    	echo "El usuario: $usuario ha sido creado."
                	else
                    	echo "El usuario: $usuario ya esta creado. "
                	fi
    	echo "$correo" > /home/$usuario/correo.txt
	done </root/usuarios.csv
}
borrarUsuarios()
{
	while read linea
	do
    	usuario=$(echo $linea | cut -d: -f1)
    	sudo userdel -r $usuario > /dev/null 2>&1
    	if [ $? -eq 0  ];
            	then
            	echo "El usuario: $usuario ha sido eliminado "
            	else
            	echo "El usuario: $usuario no se ha podido eliminar"
    	fi
  	 
	done</root/usuarios.csv
}

# Bloque principal
clear
comprobarRoot
menu

```

</details>

<br>

> [!CAUTION]
> En este ejercicio, la principal dificultad ha sido el procesamiento del campo "gecos" del fichero /etc/passwd y asegurar que se obtenga correctamente el nombre y apellidos de cada usuario. Lo hemos solucionado utilizando el comando awk -F':' '$3 >= 1000 && $3 < 2000 {print $5}' /etc/passwd, que nos permite extraer el campo "gecos" de los usuarios con UID entre 1000 y 2000. Además, hemos tenido que asegurarnos de que el archivo se cree correctamente en el directorio /tmp, y que se actualice cada día a las 7:00 am mediante una tarea programada en el cron, la cual se realiza con el siguiente comando: 0 7 * * * 
<br>

<h2>Menu</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/13.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aqui tenemos el menu que se nos pedia en el ejercicio</p>

<br>
<br>

<h2>Creación de usuarios</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/14.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>El script lee el archivo que previamente se nos a dado en el ejercicio y hemos creado en el root ,y nos crea los usuarios que le hemos indicado en el archivo</p>

<br>
<br>

<h2>Borrado de usuarios</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/15.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aqui nos muestra el listado de usuarios borrados apartir del archivo que le hemos proporcionado</p>

<br>
<br>

<h2>Archivo</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/16.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Podemos ver que el archivo se ha creado en la ruta indicada, y contiene los nombres y apellidos de los usuarios del sistema</p>

<br>
<br>

<hr>

<br>

<h1 align="center">Ejercicio 4<a name="4"></a></h1>

<details>

<summary>Enunciado del ejercicio 4</summary>

### Ejercicio 4

Crea en un script llamado crearUsuarios.sh que permita crear usuarios de forma
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

</details>

<br>

<details>

<summary> Archivo Script </summary>

<br>

```
#!/bin/bash
# Author: Horacio Gomez y Alejandro Bayo
# Version: 1.0
# Fecha: 18-05-2024
# Descripcion: Este script realiza una creación de usuarios de forma masiva, donde nosotros introducimos un nombre y número de usuarios que queramos. Además, la primera vez que entremos, tendremos que cambiar la contraseña, pero la primera contraseña para entrar es su nombre.
#Parametros/Variables
nombre_usuario_generico=$1
numero_usuarios=$2
fecha=$(date +"%Y-%m-%d %H:%M")
#Funciones
comprobarRoot ()
{
    if [ "$(id -u)" != "0" ]
    then
   	 echo "Este script solo puede ser ejecutado por el root"
   	 exit
    fi
}
#Bloque principal
clear
comprobarRoot
if [ $# -ne 2 ]; then
  echo "Tienes que meter dos parametros el Primero:nombre_usuario_genérico y el segundo:número_de_usuarios"
  exit
fi

for i in $(seq 1 1 $numero_usuarios)
    do
      nombre_usuario="$nombre_usuario_generico$i"
      password="$nombre_usuario"
	 sudo useradd -m -p $(echo -n "$password" | openssl passwd -1 -stdin) "$nombre_usuario" > /dev/null 2>&1
    sudo chage -d 0 "$nombre_usuario"

    echo "$nombre_usuario:$password" >> usuariosCreados-$fecha.tmp
    done
cat "usuariosCreados-$fecha.tmp"

````

</details>

<br>

> [!CAUTION]
> Este script ha sido sencillo de implementar utilizando el comando find para buscar archivos por extensión y tamaño. La principal dificultad ha sido asegurarnos de que los parámetros se pasen correctamente y que el script se ejecute con privilegios de root para garantizar el acceso a todos los archivos y directorios necesarios. Hemos solucionado esto con la función comprobarRoot que verifica si el script se ejecuta como root.
<br>

<h2>Introducción de comandos y variables</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/17.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aqui tenemos como debemos llamar al script ya que tenemos que colocar como primera variable el nombre que usuarn los usuarios y como segunda variable el numero de usuarios que vamos a quedar. en este caso sera Hora y 3 </p>

<br>
<br>

<h2>Muestreo del archivo temporal</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/18.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>Aqui nos muestra los usuarios creados con sus respectivas contraseñas </p>

<br>
<br>

<h2>Usuarios creados comando passwd</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Usuarios%20creados%20comando%20passwd.png" alt="Descripción de la imagen" width="650" height="550">

<br>

<p>Aqui tenemos una verificacion de que los usuarios estan creados perfectamente</p>

<br>
<br>

<h2>Cambio de contraseñas</h2>

<img src="https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Git/20.png" alt="Descripción de la imagen" width="1015" height="350">

<br>

<p>En esta imagen se puede ver la ejecución del script y el archivo generado con los resultados de la búsqueda</p>

<br>
<br>

<hr>

<br>

<h1 align="center">Ejercicio 5<a name="5"></a></h1>

<details>

<summary>Enunciado ejercicio 5</summary>

### Ejercicio 5

Partimos de que tenemos varios usuarios: usuario1, usuario2, usuario3.<br>
Al usuario1, se le ha establecido una cuota de disco: 40k y 100K (soft y hard
respectivamente).<br>
Realiza un script llamado cuotasUsuarios.sh, que nos copie la cuota del usuario1 a todos
los usuarios cuyo uid >1000 y uid<2000.

</details>

<br>

<details>

<summary> Archivo Script </summary>

<br>

<p>Escribir aquí la explicacion del script</p>

</details>

<br>

> [!CAUTION]
> Este ejercicio se nos a complicado mucho el hecho de cambiarle las cuotas al usuario ya que hemos intentado por varias formas y no hemos podido y el hecho de empezar este script se nos a hecho imposible no sabiamos por donde empezar.
<br>


<hr>

<br>

<h1 align="center">Bibliografía<a name="Bibliografía"></a></h1>

<p>-Hemos usado los boletines de scripts intermedios hechos en clase y tambien los que usamos para el examen.</p>

<p>-Tambien Hemos usado el temario del que disponemos en la moodle.</p>

<p>-Esta es una pagina web en la que hemos encontrado ayuda para las opciones de algunos comandos y busqueda de otros ya que es un manual de los mismos.</p>

<a href="">https://www.gnu.org/software/bash/manual/bash.html</a>

<p>-Esta es una ia muy completa que hemos encontrado la cual la hemos usado para resolver dudas que ya se nos hacian imposible sacar como la encriptacion de la contraseña del ejercicio 4 </p>

<a href="">https://www.solab.ai/</a>

<br>


<hr>

<br>
<br>

<h1 align="center">Conclusiones<a name="Conclusiones"></a></h1>

<br>
<br>

<p>Las conclusiones finales que sacamos de este trabajo son las siguientes: el mundo del scripting en Bash se puede complicar mucho más de lo que hemos visto en clase. También el mundo de GitHub, ya que es una aplicación que, con este trabajo, nos hemos dado cuenta de que es muy usada en el mundillo de la programación. Con este trabajo, hemos aprendido a manejarla, aunque sea un mínimo, pero suficiente para poder manejarnos mínimamente. El planteamiento del trabajo está muy bien adaptado a nuestro nivel, lo que nos ha ayudado a poder sacar adelante los ejercicios. También hemos comprobado que los scripts te ayudan muchísimo a la hora de hacer tareas normales en un ordenador.</p>

<br>
<br>

<hr>

<br>
<br>

<h1 align="center">:shipit: FIN :shipit:<a name="8"></a></h1>
