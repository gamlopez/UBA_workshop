#### Gamaliel López-Leal

###### Laboratorio de Biología Computacional y Virómica Integrativa

###### Centro de Investigación en Dinámica Celular-UAEM

[gamaliel.lopez@docentes.uaem.edu.mx](mailto:gamaliel.lopez@docentes.uaem.edu.mx)



## Identificación de Secuencias de Bacteriófagos (Metagenomica Viral y Profagos) 

### Identificación de profagos

La identificación de profagos es un proceso mas exaustivo. Para esto usaremos de nuevo **VirSorter2**. En el subdirectorio `Genomes` encontrarán un genoma de *Pseudomonas aeruginosa* que usaremos para hacer la predicción de los profagos.

```
virsorter run --keep-original-seq -i P_aeruginosa_M37351.fna -w vs2-pass-M37351 --include-groups dsDNAphage,ssDNA --min-length 30000 --min-score 0.9 -j 5 all
```

Ahora podemos revisar los resultados en el archivo **final-viral-score.tsv** ubicado dentro del subdirectorio `vs2-pass-M37351` . Dato importante: Se modificaron los flags `--min-length` y `--min-score` 



### Validación de los contigs virales

El uso de **VirSorter2** para validar los contigs virales puede ser una buena estrategia. Sin embargo, existen algunas herramientas que nos permiten verificar la integridad y calidad de los contigs virales. Aquí usaremos la herramienta **CheckV**, para mayor información consultar el siguiente enlace: https://bitbucket.org/berkeleylab/checkv/src/master/

Como **CheckV** se encuentra en el ambiente de conda, por lo que debemos ir a nuestro `home` ejecutar el  comando `cp .bashrc.conda .bashrc` , salir de la sesión y volver a ingresar:

```
cd
cp .bashrc.conda .bashrc
exit
#iniciar sesión
source activate checkv3
```

```
checkv end_to_end final-viral-combined.fa checkv_results -t 5
```

Los resultados los encontraremos en la el subdirectorio `checkv_results`. Es importante revisar la información que viene el archivo **quality_summary.tsv**

Podemos usar el script `contig_length_fasta.pl` para mirar el tamaño de los contigs virales después de pasarlos por **CheckV**     

```
perl ../../../Script/contig_length_fasta.pl  proviruses.fna
```



#### Ejercicio: 

Para comprender más lo que hace **CheckV**, podemos volver a correr **CheckV** y **VirSorter2** usando el archivo **proviruses.fna** como entrada

```
checkv end_to_end proviruses.fna checkv_results2 -t 5
```

Importante: revisar los resultados en los archivos ***.fna** y **quality_summary.tsv**

También podemos ejecutar **CheckV** con los contigs virales, resultado del ensamble *de Novo*.

```
checkv end_to_end contigs_virales.fasta checkv_results_contigs -t 5
```

Finalmente copiaremos los contigs virales validados a un nuevo directorio, para crear un nuevo directorio usa el comando `mkdir` 

```
mkdir Final_Viral_Contigs
```











































