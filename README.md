# Apuntes

## 3.1 Lamp

* Instalamos el servidor lamp para poder ***desplegar las aplicacionses***.
* Instalamos ***ftp para pasar archivos al servidor con el cliente filezilla***.
* El protrocolo ***FTP -> Puerto 21***
* Moviamos los archivos a ***/var/www/html para poder acceder a las aplicaciones*** a traves del default.conf
* ***Permisos chmod 755*** -> Permite a todos solo leer y ejecutar. Y ademas escribir al propietario
* ***Permisos chmod -R 644*** -> Permite a todos solo leer. Y ademas ejecutar y escribir al propietario
  * El ***-R era para no mostrar todos los archivos*** sobre los que ha hecho cambios.
* Instalamos el servidor ***ssh es para tener un control remoto*** del servidor.
  * Con el cliente ***putty (SSH) -> Puerto 22.***
  * El ***fingerprint*** envia un certificado para saber si es ese servidor.
* Cambiar los archivos para la base de datos del servidor.

## 3.2 Servidor de Paginas web

* Accedemos al phpmyadmin para la base de datos y pasabamos los archivos

## 4.1 Protocolo LDAP

* Sirve para acceder a una ***base de datos que almacenas en el servidor y poder gestionarlo***
  * Tambien llamado ***gestor de direcctorios***.
    * Dentro estaran los usuarios, grupos, etc;
    * Gestiona la informacion
  * Permite ***crear usuarios y grupos y organizarlos***.
  * Aprovechar el ***protocolo*** para hacer la ***autentificacion***
* 2.4 comando ***LDAP DIT*** muestra una estructura en forma de arbol.
* 2.2 archivo ***.ldif*** apra gestionar LDAP
* el ***dn*** define el nombre Distinguished Name
<!-- * ou -> organizacional  unit -> se utiliza para separar las diferentes organiaciones
* dc -> el dominio  no entra-->
* ***add_entradas*** -> permite agregar varios usuarios a la vez.
* ***modify_entradas.ldif*** ->  Modifica y añade varias entradas a la vez, por ejemplo añadimos el movil.
* ***delete_entradas.ldif*** -> listado de las entridades que queremos eliminar
* `ldapadd -x -D cn=admin,dc=dawXX,dc=net -W -f add_entradas.ldif` -> Crea todas las entidades que habia en el archivo .ldif
* `ldapmodify -x -D cn=admin,dc=dawXX,dc=net -W -f modify_entradas.ldif` -> Modifica las entradas con los cambios del archivo .ldif
* `ldapsearch -x -b dc=dawXX,dc=net “objectClass=inetOrgPerson”` -> Nos muestra el DIT de lo que indiquemos -> Para filtrar en este caso nos dara las entidades con el dc dawXX.net
* `ldapdelete -x -D cn=admin,dc=daw25,dc=net -W -f delete_entradas.ldif` -> elimina las entidades listadas en el archivo .ldif

* Clientes LSAP.
  * phpLDAPadmin para gestionar(exportar/importar/borrar/añadir) entidades.
  * Creamos un archivo LDAP, despliegue.ldif, como si nos lo hubiéramos exportado, y utilizamos la función de importar del servicio LSAP admin


* ***Autentificacion*** -> 5.4, 5.5 restricciones para que no puedan entrar a profesor los que pertenecan a griegos y a departameto los que pertenccan a romanos.
  * Otro ejemplo, con cronos puedes entrar a un departamento y minerva no
  * La autenticación es la mayor potencia

<br>
<br>
<br>
<br>


## Comandos

* ***netstat -ltn*** -> comprueba los puertos que estan escuchando
> * Lo siguiente esta mas atras mejor explicado
> * ldapsearch -> nos muestra el DIT de lo que indiquemos, parecido a como es en una BBDD
> * ldapadd -> Nos añade las entidades que hayamos definido en el fichero .ldif y las añade al DIT
> * ldapmodfy -> Modifica y añade varias entidades definidas en el fichero .ldif
> * ladapdelete -> Nos elimina todas las entradas definidas en el fichero .ldif


## Ficheros interesantes

* /etc/ldap/slapd-d -> Contiene el DIT de configuración del servidor.

>
> ### Ficheros menos interesantes
>
> * /etc/vsftpd.conf -> Fichero de configuración de vsftpd
> * /etc/ldap -> Contiene todos los ficheros y directorios ldap
> * /etc/ldap/slapd-d -> Contiene el DIT de configuración del servidor.
> * /etc/ldap/schema -> Contiene los schemas del servidor en formato .ldif
>
>

## Conceptos

* ***LAMP server*** -> Para poder ***desplegar las aplicacionses*** -> ***Es como Xampp*** pero para linux.
* ***vsftpd*** -> Para ***pasar*** archivos al servidor ***con el cliente filezilla*** -> ***Es como un servidor FTP*** para linux.
* En el fichero vsftpd.conf, activar estas tres directivas ->
  * -> anonymus_enable
  * -> local_enable
  * -> write_enable
* ***Filezilla*** -> se usara para ***pasar los archivos al servidor de Linux***.
* Open ***SSH*** server -> Servidor de Linux que ***permitira que otros equipos se conecten de forma remota***.
* ***PUTTY*** -> Cliente que ***permitira conectarnos remotamente a Linux*** a traves del SSH.

## Pasos para deplegar la aplicacion web en servidor

1. ***Acedemos al phpmyadmin*** de Linux en nuestro ordenador local, introduciendo la IPDeLinux/phpmyadmin, e iniciamos la sesion con root
2. ***Cambiamos los parametros de los php*** que queremos subir para que se ajusten a la base de datos del sevidor Linux
3. ***Con el Filezilla***, desde el equipo local, ***movemos los archivos de nuestra pagina a /var/www/html***
4. ***Cambiamos los permisos del directorio /var/www/html/alumnos*** que es la carpeta de dentro de /var/www/html donde esta nuestra pagina ->
    * ***Sudo chmod 775 /var/www/html/alumnos*** -> Permite a todos solo leer y ejecutar. Y ademas escribir al propietario
    * ***Sudo chmod 644 -R /var/www/html/alumnos/* *** -> Permite a todos solo leer. Y ademas ejecutar y escribir al propietario -> El -R era para no mostrar todos los archivos sobre los que ha hecho cambios.
5. Se añade una ***nueva directiva de alumnos en 000-default.conf*** -->
    * ***OpenLDAP*** -> Servicio de directorios de codigo abierto que proporciona inforcion sobre usuarios, grupos y servidores
    * Supongamos que tenemos un archivo .ldif lo siguiente
        * ***dn: ou=usuarios,dc=daw22,dc=net*** -> el ***dn*** signifiga ***Distinguished Name*** -> especifica la unida organizativa usuarios y el dominio de entrada daw22.net
    * ***phpLDAPadmin*** -> clientes LSAP, te da una ***interfaz grafica*** para, gestionar(exportar/importar/borrar/añadir) entidades.

## Puertos

* ***Puerto servidor MySQL -> 3306***
* ***Puerto sevidor FTP -> 21***
* ***Puerto sevidor SSH -> 22***
