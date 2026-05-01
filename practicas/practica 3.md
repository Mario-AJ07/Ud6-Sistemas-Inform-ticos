# PRÁCTICA 3

## 1. Configuración inicial del servidor

En el servidor:
1. Cambia el nombre del equipo a:
srv-ad01
2. Reinicia el sistema.
3. Comprueba el nombre del equipo ejecutando:
hostname
Incluye capturas y explica el papel que tendrá este servidor dentro de la red.

[!Screenshot Hostname windows](./Imagenes/hostname_windows.png)

Hemos cambiado el nombre del host a srv-ad01 y su función principal sera facilitar la
comunicación, permitiendo usar nombres legibles en lugar de direcciones IP numéricas complejas

Indica la documentación consultada.
https://www.ionos.es/digitalguide/hosting/cuestiones-tecnicas/hostname/

## 2. Instalación del rol Active Directory Domain Services

Abre Server Manager.
Selecciona:
Add Roles and Features
Instala el rol:
Active Directory Domain Services
Durante el proceso se instalarán también las herramientas de administración necesarias.

Incluye capturas del asistente de instalación y explica qué función cumple Active Directory
Domain Services.

[!Screenshot Administrador del servidor](./Imagenes/administrador_servidor.png)

Abrimos el administrador del servidor y seleccionamos en agregar roles

[!Screenshot Servidor](./Imagenes/servidor.png)

Seleccionamos el servidor en el que vamos a agregar los cambios y nos dirigimos a donde los roles

[!Screenshot Roles del servidor](./Imagenes/roles_servidor.png)

Vemos la lista de los roles y seleccionamos para instalar los servicios de dominio de Active
Directory.

[!Screenshot resultados](./Imagenes/resultados.png)

Una vez seleccionado lo aplicamos y se instalarán también las herramientas necesarias para
administrar.

Indica la documentación consultada.
https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-

## 3. Promoción del servidor a controlador de dominio
Una vez instalado el rol, selecciona:
Promote this server to a domain controller
Selecciona la opción:
Add a new forest
Nombre del dominio:
empresa.local
Completa el asistente utilizando la configuración por defecto.
Define una contraseña para el modo de restauración (DSRM).
Finaliza el asistente y reinicia el servidor.

Incluye capturas del proceso y explica qué significa convertir un servidor en controlador de
dominio.

[!Screenshot Configuracion post-instalacion](./Imagenes/configuracion_posterior.png)

En la bandera encontramos una pestaña donde clickearemos donde pone “Agregar roles y
carecterísticas”

[!Screenshot Nuevo bosque](./Imagenes/nuevo_bosque.png)

Seleccionamos la opción de agregar un nuevo bosque

[!Screenshot Nuevo dominio](./Imagenes/nuevo_dominio.png)

Y en el nombre del dominio raíz escribimos que será empresa.local después continuaremos la
instalación sin tocar nada más

https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-

## 4. Verificación del dominio
Tras el reinicio, inicia sesión con la cuenta:
empresa\Administrator
Abre la herramienta:
Active Directory Users and Computers
Comprueba que aparece el dominio:
empresa.local

Incluye capturas y explica la estructura básica que aparece en el dominio.

[!Screenshot Inicio de sesion dominio empresa](./Imagenes/inicio_sesion.png)

Después de la instalación se reiniciara la máquina y al volverla a iniciar y vemos la nueva cuenta

[!Screenshot active directory user](./Imagenes/Active_directory_user.png)

Abrimos la herramienta Active Directory Users and Computers y comprobamos que en efecto
aparece el dominio: empresa.local

Indica la documentación consultada.
https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-

## 5. Creación de usuarios de dominio
En Active Directory Users and Computers crea dos usuarios:
usuario1
usuario2
Asigna una contraseña inicial a cada uno.

Incluye capturas del proceso y explica la diferencia entre:
• usuario local: Un usuario local es una cuenta que se crea y se almacena en un único equipo.
• usuario de dominio: Un usuario de dominio es una cuenta creada en el servidor mediante
Active Directory Domain Services.

[!Screenshot active directory user](./Imagenes/active_directory_user.png)

Miramos en el dominio empresa.local y buscamos la carpeta donde se almacenan los usuarios

[!Screenshot carpeta de usuarios](./Imagenes/carpeta_users.png)

Una vez hemos encontrado la carpeta la abrimos.

[!Screenshot Crear Usuarios 1 y 2](./Imagenes/nuevo_users.png)

Y con click derecho se nos desplegarán multiples opciones, pulsamos donde dice “nuevo” y acto
seguido pulsamos usuario, escribiremos el nombre del usuario y su contraseña y lo repetiremos
yuna vez más todo el proceso

[!Screenshot Usuarios 1 y 2 creados](./Imagenes/users_creados.png)

Ahora en usuarios se nos ha añadido tanto Usuario1 como Usuario2.

Indica la documentación consultada.

https://www.youtube.com/watch?v=nIbtIcFnioQ


## 6. Preparación de la carpeta de perfiles móviles
En el servidor crea la carpeta:
C:\perfiles
Comparte la carpeta con el nombre:
perfiles

Incluye capturas del recurso compartido y explica qué función tendrá esta carpeta dentro del
dominio.
• La función de esta carpeta ses que se utilizará para almacenar los perfiles móviles de los
usuarios del dominio en Active Directory Domain Services.

[!Screenshot Carpeta perfiles](./Imagenes/carpeta_perfiles.png)

Nos dirigimos a equipo después a la carpeta c: desde el explorador de archivos y con click derecho
crearemos una nueva carpeta con el nombre de perfiles

[!Screenshot uso compartido avanzado](./Imagenes/compartido_avanzado.png)

Pulsaremos la opción uso compartido avanzado

Indica la documentación consultada.
https://learn.microsoft.com/es-es/windows-server/storage/folder-redirection/deploy-roaming-user-profiles


## 7. Configuración de perfiles móviles
En Active Directory Users and Computers:
Edita las propiedades de cada usuario.
En la pestaña Profile, configura la ruta del perfil:
\\srv-ad01\perfiles\%username%

Incluye capturas y explica qué es un perfil móvil y qué ventajas ofrece en un entorno de dominio.

• Un perfil móvil es una configuración que almacena los datos personales del usuario
(escritorio, documentos, favoritos, configuraciones de aplicaciones) en un servidor
centralizado en lugar de localmente en el equipo

[!Screenshot Ruta del perfil usuario1](./Imagenes/ruta_perfil.png)

Volvemos a la carpeta users y esta vez haremos click derecho en ususario1 nos dirijimos a donde
pone perfil y en donde pone ruta de acceso al perfil ponemos el host y la propia carpeta de perfiles

[!Screenshot Ruta del perfil usuario2](./Imagenes/ruta_perfil2.png)

Hacemos exactamente lo mismo con el usuario2

Indica la documentación consultada:

https://learn.microsoft.com/es-es/windows-server/storage/folder-redirection/deploy-roaming-user-profiles

## 8. Unión del equipo Windows 11 al dominio
En el equipo cliente cli01:
1. Abre la configuración del sistema.
2. Cambia el tipo de red para unir el equipo al dominio:
Dominio:
empresa.local
Cuando se solicite, introduce las credenciales de administrador del dominio.
Reinicia el equipo.

Incluye capturas del proceso y explica qué significa unir un equipo a un dominio.

[!Screenshot Unir el equipo al dominio de empresa.local](./Imagenes/unir_equipo.png)

Indica la documentación consultada.

## 10. Modificación de la política de contraseñas
En el servidor abre la herramienta:
Group Policy Management
Localiza la política:
Default Domain Policy
Edita la política y modifica alguno de los parámetros de contraseña, por ejemplo:
• longitud mínima de contraseña
• complejidad de contraseña
Aplica los cambios.

Incluye capturas y explica qué son las Group Policy Objects (GPO) y qué función tienen en un
dominio.

• son contenedores virtuales utilizados en active directory (AD) para gestionar y configurar
centralizadamente el entorno de usuarios y equipos

[!Screenshot Localiza la política Default Domain Policy](./Imagenes/domain_policy.png)

Nos metemos en la herramienta administración de directivas de grupo y localizamos el bosque
empresa.local

[!Screenshot Localiza la política Default Domain Policy](./Imagenes/default_domain.png)

Vamos desplegando de a poco la jerarquia de carpetas hasta encontrar la carpeta default domain.

[!Screenshot Directivas de las contraseñas](./Imagenes/directivas_contraseñas.png)

Seguimos desplegando carpetas hasta que encontramos las directivas de las contraseñas.

[!Screenshot Modificar las directivas de las contraseñas](./Imagenes/modificar_directivas.png)

Las editamos en mi caso aumentando la cantidad mínima de caracteres de 7 a 14 y disminuyendo el
tiempo de la vigencia de las contraseñas de 42 días a 30.

Indica la documentación consultada.



## 11. Verificación de la política aplicada
En el cliente ejecuta:
gpupdate /force
Después intenta cambiar la contraseña de uno de los usuarios para comprobar que se aplica la nueva
política.

Incluye capturas y explica cómo se aplican las políticas de dominio en los equipos cliente.
Indica la documentación consultada.

• Se aplican en los equipos cliente de Windows mediante un proceso automatizado del lado
del cliente que consulta al controlador de dominio (Active Directory) al inicio, logueo o
periódicamente

https://learn.microsoft.com/es-es/windows-server/administration/windows-commands/gpupdate


[!Screenshot gupdate para actualizar las directivas de las contraseñas](./Imagenes/gupdate.png)

Ejecutamos el comando gpupdate /force para implementar los cambios de las contraseñas y se
actualiza con éxito.

[!Screenshot cambio de usuario](./Imagenes/cambio_usuario.png)

Cambiamos de usuario para comprobar los cambios

[!Screenshot Error al escribir una contraseña que no sigue las nuevas directivas](./Imagenes/error.png)

Pone que la contraseña no se puede usar debidp a que es más pequeña que los 14 caracteres que he
puesto antes

## INDEX 
[Indice](../index.md)