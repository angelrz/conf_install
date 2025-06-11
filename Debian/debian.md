# Configuración Debian 12

> [!note]
> Recordar, estamos iniciando el sistema, por ende todo se realiza con *su*

## Superusuario

```bash
su
```

## GRUB

- Evitar problemas horarios entre sistemas operativos

```bash
sudo timedatectl set-local-rtc 1
```

- DualBooT: Seleccionar el último sistema

```bash
nano /etc/default/grub
```

- Agregar/actualizar las siguientes líneas

```bash
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

**Salir y actualizar** el grub

```bash
sudo update-grub
```

---

## Uso de terminal

### Ejecución sudo con mi usuario

Entrar con *su* al modo [superusuario](#superusuario)

```bash
root@debian: 
```

Modificar le archivo /etc/sudoers

```bash
nano /etc/sudoers
```

Agregar MI_USER. Ver * cuando ingreso mi contraseña

```bash
Defaults    env_reset,pwfeedback
...

# User privilege specification
root    ALL=(ALL:ALL) ALL
MI_USER    ALL=(ALL:ALL) ALL
```

### Autocompletado en terminal

Instalar bash-completion

```bash
sudo apt update
sudo apt install bash-completion
```

Entrar al archivo ~/.bashrc

```bash
sudo nano ~/.bashrc
```

Verificar líneas en el archivo ~/.bashrc del root

```bash
# Activar bash-completion
if [ -f /etc/bash_completion ]; then
        . /etc/bash_completion
fi
```

Si modifico/agrego, asegurar cambios

```bash
source ~/.bashrc
```

---

## Comandos, ventanas, experiencia

- Activar el clic del touchpad
Ratón y panel táctil/Panel Táctil/Tocar para pulsar'

- Terminal con teclado
 Teclado/'Ver y personalizar Atajos'/Atajo personalizado
 Comando: gnome-terminal

### Navegación y ventanas

- Alt+Tab y navegación
 Teclado/'Ver y personalizar Atajos'/Navegación
  Cambiar entre ventanas: alt+tab
  Ocultar todas las ventanas normales: super+d

- Cerrar ventana con super+q
 Teclado/'Ver y personalizar Atajos'/Ventanas
  Cerrar ventana: ctrl+q

- Lanzadores estilo windows
 Teclado/'Ver y personalizar Atajos'/Lanzadores
  Carpeta personal: super+e
  Configuracion: super+i

### Cierre inesperado de la calculadora

```bash
dconf write /org/gnome/calculator/refresh-interval 0
```

---

## Eliminar app/juegos en Debian 12 GNOME

```bash
sudo apt purge gnome-2048 gnome-contacts gnome-weather gnome-maps gnome-calendar gnome-clocks gnome-chess five-or-more simple-scan four-in-a-row cheese gnome-sound-recorder hitori gnome-klotski lightsoff gnome-mines gnome-nibbles gnome-mahjongg quadrapassel rhythmbox gnome-robots iagno gnome-music gnome-sudoku gnome-taquin gnome-tetravex thunderbird transmission-common transmission-gtk aisleriot swell-foop tali libreoffice* evolution debian-reference-common yelp && sudo apt autoremove 
```

## LMDE6

```bash
sudo apt purge gnote gedit libreoffice* hexchat hypnotix redshift onboard celluloid transmission gnome-calendar  gnome-2048 gnome-chess gnome-games gnome-klotski gnome-mahjongg gnome-mines gnome-nibbles gnome-robots gnome-sound-recorder gnome-sudoku gnome-taquin gnome-tetravex gnome-video-effects thunderbird pidgin remmina shotwell sound-juicer transmission-common transmission-gtk rhythmbox xterm drawing pix sticky thingy warpinator && sudo apt autoremove
```

## Eliminar Ubuntu desde Windows (Persiste el GRUB)

- Abrir CMD como administrador y ejecutar *diskpart*

```bash
C:\WINDOWS\system32>diskpart 
Microsoft DiskPart version 10.0.19041.3636
Copyright (C) Microsoft Corporation.
On computer: TuPC

DISKPART>     
```

- Seleccionar el disco de Windows y la partición de arranque

```cmd
sel disk #
```

```cmd
sel part #

```

> [!note]
> *Reemplazar # por el número de disco donde está Windows y la partición de arranque*

- Una vez que estamos en la partición, ejecutar

```cmd

assign letter X

```

- Abrir un **nuevo CMD** como administrador, dentro abrir la unidad X

```cmd
X:
```

- Cambiar de directorio a EFI

```cmd
cd EFI
```

- Eliminar la carpeta Linux, por ejemplo, si es ubuntu

``` cmd
rd /s ubuntu
```

- Cerrar ese CMD y volver al CMD donde asignamos la letra X, para ahora removerla

```cmd
remove letter X
```

- Salir del *diskpart* con

```cmd
exit
```

- Ver la lista de arranque

```cmd
bcdedit /enum firmware

```

- Encontrar la que diga Linux y copiar el Identificador, copiarlo con *Ctrl + C* y eliminar la entrada con

```cmd
bcdedit /delete {identificador}  
```

Reiniciar para verificar que ya no existe el GRUB.
