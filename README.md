# Trabajo Bloque V Horacio y Alejandro

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/script-en-diferentes-lenguajes.jpg)
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

<h1 align="center">Ejercicio 1</h1>

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

<br>

<summary>Script</summary>

<br>

````
!/bin/bash
 Author: Horacio Gomez y Alejandro bayo
 Version: 1.0
 Fecha: 15-05-2024
 Descripcion: Este script realiza -
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
comprobar_apache &

````


</details>

<br>

> [!CAUTION]
> Aquí ponemos los problemas.

<br>

<h2 align="right">Tarea Programada</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/TareaProgramada.png)

<br>
<br>
<br> 

<h2 color="red" align="rigth">Reactivación del apache</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Reactivacion%20de%20apache.png)

<br>
<br>
<br>

<h2 color="red" align="rigth">Archivo creado</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Archivo%20creado.png)

<br>
<br>
<br>

<h2 color="red" align="rigth">Activamos el apache</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apache%20running.png)

<br>
<br>
<br>

<h2 color="red" align="rigth">Apache pausado</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apache%20parado.png)

<br>
<br>
<br>

<hr>

<h1 align="center">Ejercicio 2</h1>

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

<summary>Script</summary>

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
> Aquí ponemos los problemas.
<br>

<h2>Apartado 1 sin bloqueados</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%201%20sin%20bloqueados.png)


<h2 color="red" align="rigth">Apartado 2 pregunta</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%202%20pregunta.png)

<h2 color="red" align="rigth">Apartado 2 ya bloqueado</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%202%20ya%20bloqueado.png)

<h2 color="red" align="rigth">Apartado 3 pregunta</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%203%20pregunta.png)

<h2 color="red" align="rigth">Apartado 3 ya desbloqueado</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%203%20ya%20desbloqueado.png)

<h2 color="red" align="rigth">Apartado 4 pregunta</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%204%20usuario%20no%20conectado.png)

<h2 color="red" align="rigth">Apartado 4 usuarios no conectados</h2>

![](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Apartado%204%20pregunta.png)

<hr>

<br>

<h2 align="center">Ejercicio 3</h2>

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

<summary>Script</summary>

<br>

<p>Escribir aquí la explicacion del script</p>

</details>

<br>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

<hr>

<br>

<h2 align="center">Ejercicio 4</h2>

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

<summary>Script</summary>

<br>

```
!/bin/bash
 Author: Horacio Gomez y Alejandro Bayo
 Version: 1.0
 Fecha: 18-05-2024
 Descripcion: Este script realiza -
Parametros/Variables
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
	 sudo useradd -m -p $(echo -n "$password" | openssl passwd -1 -stdin) "$nombre_usuario"
    sudo chage -d 0 "$nombre_usuario"

    echo "$nombre_usuario:$password" >> usuariosCreados-$fecha.tmp
    done
cat "usuariosCreados-$fecha.tmp"
````

</details>

<br>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

<h2>Usuarios creados comando passwd</h2>

<br>

![Usuarios creados](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Usuarios%20creados%20comando%20passwd.png)

<br>

<h2 color="red" align="rigth">Muestreo del archivo temporal</h2>

<br>

![Muestra del archivo temporal](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Muestreo%20del%20archivo%20temporal.png)


<h2 color="red" align="rigth">Introducción de comandos y variables</h2>

<br>

![Introducción del comando y variables](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Introduccion%20del%20comando%20y%20variables.png)


<h2 color="red" align="rigth">Cambio de contraseñas</h2>

<br>

![Cambio de contraseñas](https://github.com/HoracioGG/Trabajo-Bloque-V-Horacio-y-Alejandro/blob/main/Cambio%20de%20la%20contraseña.png)

<hr>

<br>

<h2 align="center">Ejercicio 5</h2>

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

<summary>Script</summary>

<br>

<p>Escribir aquí la explicacion del script</p>

</details>

<br>

> [!CAUTION]
> Aquí ponemos los problemas.
<br>

















