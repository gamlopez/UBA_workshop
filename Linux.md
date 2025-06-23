Escrito por:

##### Gamaliel López-Leal

gamaliel.lopez@docentes.uaem.edu.mx





## Acceso al servidor: Uso de la Terminal

Para iniciar sesión en el servidor, es necesario utilizar una **terminal** o **línea de comandos**. La terminal permite establecer una conexión remota segura mediante el protocolo SSH (**Secure Shell** ), que es esencial para acceder a los recursos del servidor y ejecutar tareas de forma eficiente. Este acceso no se realiza a través de interfaces gráficas tradicionales, sino escribiendo comandos directamente.

Debes de contar con:

**Nombre del Usuario:**
**Dirección IP:**
**Contraseña:**

```
ssh -X user@xxx.xxx.xxx
```

Para subir o descargar archivos debes de usar el sftp (Secure File Transfer Protocol)

```
sftp user@xxx.xxx.xxx
```

🔐 **Seguro**: Toda la transferencia está cifrada.

📁 **Acceso a archivos remotos**: Permite listar, subir, bajar, mover y borrar archivos en el servidor.

🔧 **Soporta comandos básicos**: Como `get`, `put`, `ls`, `cd`, `rm`, etc.



## Ejecutando comandos

Cada vez que se arranca una terminal se presenta un prompt en pantalla, es el indicador que el shell esta esperando para recibir comandos a ser ejecutados.

```
gama@conacyt:~$
```



## Directorio de trabajo

La parte del sistema operativo responsable de gestionar archivos y directorios se llama **sistema de archivos** (filesystem). Este organiza nuestros datos en **archivos**, que contienen información, y en **directorios** (también llamados **carpetas**), que contienen archivos u otros directorios.

Primero, vamos a averiguar en qué lugar nos encontramos ejecutando un comando llamado `pwd` (que significa "**print working directory**" o “imprimir directorio de trabajo”).

```
pwd
```

Para cambiar de directorio de trabajo debes de hacerlo con el comando `cd`

```
cd /path/             #accede a un directorio especifico.
cd ..                 #te dirige a un directorio superior.
cd                    # te lleva al home
```



### `ls` - Listar archivos y directorios

Muestra el contenido del directorio actual.

**Ejemplos:**

```
ls
ls -l   # Lista en formato detallado
ls -a   # Muestra archivos ocultos
ls -lh  # Tamaño de archivos en formato legible
ls -lt  # Ordena por fecha de modificación
```



## Crear y editar archivos con `pico`

`pico` es un **editor de texto simple en la terminal**. Se usa comúnmente en sistemas Linux y Unix. 

```
pico nombre_del_archivo.txt
```

- Si el archivo existe, lo abrirá.
- Si no existe, lo creará.



## Gestión de Archivos y Directorios

### `mkdir` - Crear directorios

Crea un nuevo directorio.

**Ejemplos:**

```
mkdir nuevo_directorio
mkdir -p carpeta1/carpeta2  #Crea múltiples carpetas anidadas
mkdir Taller  			    #Crea la carpeta 'Taller'
```



## `rmdir` - Eliminar directorios vacíos 

Elimina un directorio solo si está vacío.

## `rm` - Eliminar archivos y directorios

Elimina archivos o directorios (con `-r`).

```
rmdir carpeta_vacia
rmdir -p a/b/c  # Borra c, luego b si está vacía, luego a si está vacía

rmkdir -p carpeta1/carpeta2
```

```
rm archivo.txt  # Borra un archivo
rm -r carpeta  # Borra una carpeta y su contenido
rm -i archivo.txt  # Pregunta antes de borrar
rm -rf /directorio  # Borra forzadamente sin confirmación
```



## `cp` - Copiar archivos y directorios

Copia archivos de un lugar a otro.

**Ejemplos:**

```
cp archivo1.txt copia.txt      # Copia archivo1.txt a copia.txt
cp archivo.txt /path/  		   # Copia a otra carpeta
cp /path/archivo.txt . 		   # Copia archivo en directorio de trabajo
```



### `mv` - Mover o renombrar archivos y directorios

Mueve archivos o los renombra.

**Ejemplos:**

```
mv archivo.txt nuevo_nombre.txt  # Renombra el archivo
mv archivo.txt /otra_carpeta/    # Mueve el archivo a otra carpeta
mv * /home/usuario/todos/        # Mueve todos los archivos a otro directorio
```

















































































































