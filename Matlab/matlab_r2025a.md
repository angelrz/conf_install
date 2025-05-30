# Instalación MATLAB R2025A en Linux Debian y derivados

## Descargar el instalador de MATLAB

Ingresar a [MATLAB](https://la.mathworks.com/downloads/), seleccionar la versión y dar clic en descargar.

> [!NOTE]
> La instalación es para MATLAB R2025A, ojo.

## Descomprimir el .zip instalador

Puede ser desde el **explorador de archivos** dando doble clic o **terminal** con el comando

```bash
unzip matlab_R2025a_Linux.zip
```

## Ejecutar el instalador

Después de descomprimir, abrir el directorio que apareció en la terminal y ejecutar el siguiente comando

```bash
sudo chmod +x install
```

El comando anterior da permisos de ejecución al instalador. Ahora, ejecutar el instalador con

```bash
sudo ./install
```

## Seleccionar ruta de instalación e instalación

Sugerencia, mantener el directorio por defecto de MATLAB:
> [!IMPORTANT]
> Ruta por defecto: **/usr/local/MATLAB/R2025a**
> Recuerda esta ruta porque será para la [variable de entorno](#variables-de-entorno) y el [ejecutable](#crear-ejecutable).

## Ejecutar MATLAB

> [!CAUTION]
> Al tratar de ejecutar **matlab** en terminal, te aparecerá algo como

```txt
matlab: no se encontró la orden
```

## Variables de entorno

Configura tú varible de entorno. Para ello, abrir con nano el archivo **.bashrc** en terminal

```bash
sudo nano ~/.bashrc
```

Y escribir el comando de la variable

```bash
export PATH=/usr/local/MATLAB/R2025a/bin:${PATH}
```

## Crear ejecutable

Ahora, crea el ejecutable de matlab para que aparezca en el menú de apps. En terminal ejecuta

```bash
sudo nano /usr/share/applications/matlab.desktop
```

Y pega lo siguiente:

```bash
[Desktop Entry]
Name=Matlab
Comment=R2025a
Version=1.0
Type=Application
Exec=/usr/local/MATLAB/R2025a/bin/matlab -desktop
Icon=/usr/local/MATLAB/R2025a/resources/coreui/matlab/splash.png
Terminal=false
```

Material de apoyo:
> [!TIP]
> Puedes apoyarte con el siguiente [Video de Youtube](https://www.youtube.com/watch?v=KCDG_SCDcaY), lo explico con la versión R2024A.
> Adicional, puedes visitar este [Blog](https://linux.how2shout.com/how-to-install-matlab-in-ubuntu-22-04/) que también me fue de utilidad.
