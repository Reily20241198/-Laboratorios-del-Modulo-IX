# -Laboratorios-del-Modulo-IX
Practica 1 Instalacion de Webmin (1Pts )
# Práctica 1 - Instalación y Uso de Webmin en CentOS

Esta práctica te guía paso a paso para instalar Webmin en CentOS y realizar tareas de administración desde su panel web.

-----------------------------------------------------
1. INSTALACIÓN DE WEBMIN
-----------------------------------------------------

1.1 Actualizar el sistema:
Este comando actualiza todos los paquetes del sistema a su última versión.

    sudo dnf update -y

1.2 Instalar Perl (Webmin lo necesita):
    
    sudo dnf install perl -y

1.3 Crear archivo de repositorio de Webmin:
Esto le dice a DNF dónde buscar los paquetes de Webmin.

    sudo tee /etc/yum.repos.d/webmin.repo <<EOF
    [Webmin]
    name=Webmin Distribution Neutral
    baseurl=https://download.webmin.com/download/yum
    enabled=1
    gpgcheck=0
    EOF

> NOTA: Se desactivó `gpgcheck=1` porque la clave GPG dio error.

1.4 Instalar Webmin directamente sin validación GPG:

    sudo dnf install webmin -y

1.5 Verificar si Webmin se está ejecutando:

    sudo systemctl status webmin

1.6 Abrir el puerto del firewall si es necesario (10000):

    sudo firewall-cmd --permanent --add-port=10000/tcp
    sudo firewall-cmd --reload

-----------------------------------------------------
2. ACCESO A WEBMIN
-----------------------------------------------------

Abrir el navegador e ingresar a:

    https://<IP_DE_TU_SERVIDOR>:10000

Usuario: root  
Contraseña: (la que uses para root)

-----------------------------------------------------
3. TAREAS DESDE LA INTERFAZ DE WEBMIN
-----------------------------------------------------

3.1 Crear y eliminar usuarios:
Ruta: System > Users and Groups
- Crear: "Create a new user"
- Eliminar: Seleccionar un usuario y clic en "Delete"

3.2 Administrar servicios (ejemplo: SSH):
Ruta: System > Bootup and Shutdown
- Buscar "sshd" → Start, Stop, Restart

3.3 Configurar IP estática:
Ruta: Networking > Network Configuration > Network Interfaces
- Seleccionar la interfaz activa (ej. ens33)
- Cambiar a Static
- Especificar:
    IP Address: 192.168.1.100
    Netmask: 255.255.255.0
    Gateway: 192.168.1.1
- Guardar y aplicar

3.4 Instalar, eliminar y actualizar software:
Ruta: System > Software Packages
- Instalar: escribir el nombre del paquete (ej. htop) y dar clic en Install
- Eliminar: buscar y clic en Remove
- Actualizar todo: System > Software Package Updates > Update All

3.5 Exploración, edición y eliminación de archivos:
Ruta: Others > File Manager
- Explorar carpetas
- Clic derecho → Edit o Delete
Ejemplo: editar /etc/hosts

3.6 Monitorizar sistema:
Ruta: Others > System and Server Status
- CPU, RAM, disco, carga promedio

-----------------------------------------------------
4. RESULTADOS ESPERADOS
-----------------------------------------------------

✔ Webmin instalado correctamente
✔ Usuario creado y eliminado
✔ Servicio ssh reiniciado
✔ IP estática asignada
✔ Paquete htop instalado o eliminado
✔ Archivo editado en el File Manager
✔ Monitoreo del sistema visualizado

-----------------------------------------------------
Fin de la práctica klk
