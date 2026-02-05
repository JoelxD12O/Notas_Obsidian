cat /etc/passwd :
cat /etc/passwd :
Entidad creada en Linux para otorgar permisos que permitan al usuario realizar tareas específicas. Se crean usuarios para personas que requieren acceso al computador, también para servicios/aplicaciones que requieren acceso ciertos archivos y otros recursos del sistema operativo. 

usuario se puede clasificar en :
![[Pasted_image_20250821204018.jpg]]
que usuario soy:
whoami
id:
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),119(netdev),120(lxd),999(docker)

si no especifico el grupo linux te coloca a un grupo por lo tanto crea un grupo con el mismo nombre de usuario

sudo: super user do
cualquier usuario que pertenezca a ese grupo ejecutara comandos como si fuera root 

---
NO HACER(comando publico):
Por defecto se crea un grupo con el mismo nombre de usuario y se le asigna como grupo primario
useradd-m jperez:  solo el usuario root lo puede ejecutar
![[Pasted_image_20250821204418.jpg]]
![[Pasted_image_20250821204444.jpg]]


---
crear grupo estudiantes :
$ groupadd estudiantes

para mirar los grupos:
$ cat /etc/group

---
como crear un usuario

sudo useradd -m  jcayllahua -g  estudiantes  -G  tesistas,sudo

sudo useradd -m  usuariorimac -g  estudiantes  



-g:grupo primario
-G: grupos adicionales

creamos contraseña:
sudopasswd utec

---
cambiar de usuario
su jcayllahua

---
para que esto se logre tienes que salir y volver a entrar 
agregamos el grupo investigadores

sudo usermod jcayllahua -a -G investigadores,sudo

exit

su jcayllahua
id


---

chmode 664 holamundo.cpp

---
df -h

lo que usamos la instancia en el disco duro 