#!/bin/bash
echo "Bienvenido "
echo "Este es un script para realizar la instalación de algunos servicios"
echo "Por favor seleccione una opción:" 

echo "
1.  Instalar nginx
2.  Instalar http
3.  Instalar mariadb
4.  Instalar ssh
5.  Ver dirección IP
6.  Ver puertos de servicios (nginx, http, mariedb, ssh)
7.  Obtener nombre de servidor
8.  Consultar usuarios
9.  Iniciar servicio nginx
10. Iniciar servicio http
11. Iniciar Mariadb
12. Iniciar ssh
13. Ver el estado del servicio
14. Salir"

read option

installNginx() {
echo "Instalando el servicio Nginx"
yum install epel-release -y
yum install nginx -y
echo "Verificando la instalación"
sleep 2
rpm -qa | grep nginx
}

installHttp() {
echo "Instalando el servicio Http"
sleep 2
yum install epel-release -y
yum install httpd -y
echo "Verificando la instalación"
sleep 2
rpm -qa | grep httpd
}

installMariadb(){
echo "Instalando el servicio mariadb"
sleep 2
yum install epel-release -y
yum install mariadb-server -y
echo "Verificando la instalación"
sleep 2
rpm -qa | grep mariadb-server
}

installSsh(){
echo "Instalando el servicio ssh"
sleep 2
yum install openssh-server -y
echo "Verificando la instalación"
sleep 2
rpm -qa | grep openssh-server
}

viewStatus(){
systemctl status nginx
systemctl status httpd
systemctl status mariadb
systemctl status sshd
}

viewIp(){
echo "La ip es la siguiente: "
ip a s
}

viewPorts(){
echo "El puerto es: "
netstat -punta | grep nginx
netstat -punta | grep httpd
netstat -punta | grep mariadb
netstat -punta | grep sshd
}

viewHostName() {
echo "El nombre del servidor es: "
hostname
}

viewUsers() {
echo "Listado de usuarios: "   
cat /etc/passwd
}

stopServices(){
systemctl stop nginx
systemctl stop httpd
}

startNginx() {
echo "Servicio http detenido"
echo "Iniciando el servicio Nginx"
systemctl start nginx 
}

startHttp(){
echo "Servicio Nginx detenido"
echo "Iniciando el servicio Http"
systemctl start httpd
}

startMariadb(){
echo "Iniciando el servicio "
systemctl enable mariadb
systemctl start mariadb
}

startSsh(){
echo "Iniciando el servicio Ssh"
systemctl enable sshd
systemctl start sshd
}

case $option in
     1)
	     installNginx
     ;;	
     2)
	     installHttp
     ;;
     3)
	     installMariadb
     ;;
     4)
	     installSsh
     ;;
     5)
	     viewIp
     ;;
     6)
	     viewPorts
     ;;
     7)
	     viewHostName
     ;;
     8)
	     viewUsers
     ;;
     9)
	     stopServices
	     startNginx
     ;;
     10)
	     stopServices
	     startHttp
     ;;
     11)
	     startMariadb
     ;;
     12)
	     startSsh
     ;;
     13)
	     viewStatus
     ;;
     14)
	     exit 0
     ;;

esac
