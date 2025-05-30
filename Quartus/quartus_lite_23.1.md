# Instalar QUARTUS Lite en Linux Debian y derivados

## Descargar instalador

Desde [Intel](https://www.intel.com/content/www/us/en/software-kit/795187/intel-quartus-prime-lite-edition-design-software-version-23-1-for-linux.html) seleccionar la versión de Quartus

> [!NOTE]
> Para este caso será la versión 23.1

## Ejecutar el instalador

Abrir la carpeta de Descargas (Downloads) en terminal, dar permiso de ejecución al .run con

```bash
sudo chmod +x *.run
```

Ejecutar el instalador

```bash
sudo ./*.run
```

> [!TIP]
> Seleccionar descargar e instalar, sugiero la siguiente por defecto: **/home/USUARIO/intelFPGA_lite/23.1std**  

**Saltar** creación del ejecutable y el primer lanzamiento.

## Crear variables de entorno

Abrir el archivo **.bashrc** con nano

```bash
nano ~/.bashrc  
```

Escribir al final del archivo las var

```bash
export PATH=/home/angel/intelFPGA_lite/23.1std/quartus/bin:${PATH}

QUARTUS_ROOTDIR_OVERRIDE=/home/angel/intelFPGA_lite/23.1std/quartus
export QUARTUS_ROOTDIR_OVERRIDE

QUARTUS_64BIT=1
export QUARTUS_64BIT
```
  
> [!NOTE]
> Salir para reinciar terminal y escribir **quartus** para verificar que aparezca

```text
quartus: error while loading shared libraries: libprotobuf.so.14: cannot open shared object file: No such file or direct  
```

Si aparece, ejecutar

```bash
sudo chmod -R go=u-w intelFPGA_lite/
```

## Descargar JTAG

Seguir el siguiente [PDF sobre Quartus](https://mil.ufl.edu/3701/docs/quartus/Quartus19.1_install_on_Linux.pdf) para **descargar JTAG**

> [!NOTE]
> Descargar directamente [Libreria JTAG](https://marsohod.org/downloads/category/16?download=178)

Descomprimir y ejecutar copiar el directorio:

```bash
cp libjtag_hw_mbftdi-blaster.so ~/intelFPGA_lite/23.1std/quartus/linux64  
```

## Driver USB Blaster
  
Crear o abrir archivo **51-usbblaster.rules**

```bash
sudo nano /etc/udev/rules.d/51-usbblaster.rules
```

Desde [Cable II Driver on Linux Systems](https://www.intel.com/content/www/us/en/docs/programmable/683719/current/installing-the-driver-on-linux-systems.html)

Puede o NO aparecer lo siguiente

```text
SUBSYSTEM=="usb",ENV{DEVTYPE}=="usb_device",ATTR{idVendor}=="0403",ATTR{idProdu>
10",MODE="0666",RUN+="/usr/sbin/rmmod ftdi_sio"
```
  
Modificar por la [Sugerencia en Intel Community](https://community.intel.com/t5/Intel-Quartus-Prime-Software/Quartus-II-JTAG-Server-Error-Code-89/td-p/162221) o bien:

```text
# USB-Blaster
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="09fb", ATTRS{idProduct}=="6001", MODE="0666", SYMLINK+="usbblaster/%k"  
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="09fb", ATTRS{idProduct}=="6002", MODE="0666", SYMLINK+="usbblaster/%k"  
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="09fb", ATTRS{idProduct}=="6003", MODE="0666", SYMLINK+="usbblaster/%k"  
  
# USB-Blaster II
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="09fb", ATTRS{idProduct}=="6010", MODE="0666", SYMLINK+="usbblaster2/%k"  
SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="09fb", ATTRS{idProduct}=="6810", MODE="0666", SYMLINK+="usbblaster2/%k"
```
  
> [!TIP]
> O bien, ocupar el archivo de este [repositorio de GitHub](https://github.com/GoComputing/QuartusInstallerUbuntu/tree/master/files).

## Crear ejecutable (icono)

Crear el archivo **quartus.desktop**

```bash
sudo nano /usr/share/applications/quartus.desktop
```

Agregar las siguientes propiedades

```text
[Desktop Entry]
Name=Quartus Prime
Comment=Lite Edition (23.1)
Version=1.0
Type=Application
Exec=/home/angel/intelFPGA_lite/23.1std/quartus/bin/quartus -desktop
Icon=/home/angel/intelFPGA_lite/23.1std/quartus/adm/quartusii.png
Terminal=false
```

>[!NOTE]
> Reiniciar PC sí no aparece el ejecutable
