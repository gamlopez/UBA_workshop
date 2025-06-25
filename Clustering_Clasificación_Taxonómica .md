#### Gamaliel López-Leal

###### Laboratorio de Biología Computacional y Virómica Integrativa

###### Centro de Investigación en Dinámica Celular-UAEM

[gamaliel.lopez@docentes.uaem.edu.mx](mailto:gamaliel.lopez@docentes.uaem.edu.mx)



## Clustering y Clasificación Taxonómica 



### Clustering usando el genoma (VIRIDIC)

La herramienta **VIRIDIC** no solo se puede cirrer usando la interfaz web (https://rhea.icbm.uni-oldenburg.de/viridic/), en caso de tener una gran cantidad de contigs/genomas es mejor correrlo usando un servidor de HPC (High-Performance Computing), https://github.com/CristinaMoraru/VIRIDIC?tab=readme-ov-file.

Ahora en su `home`cree un diretorio para la el modulo 4 clusterización y taxonomia

```
#Entrar al directorio de home, $HOME es una variable predefinida que contiene el path hacia su home. 
cd $HOME 
#crear directorio para modulo de clustering y taxonomia
mkdir clustering_taxonomia
#copiar los contigs en el nuevo directorio
cp /path/final_viral_sequences.fasta $HOME/clustering_taxonomia
```

Para correr VIRIDIC en el servidor, se necesita como entrada las secuencias fasta en un solo archivo (igual que en el servidor web).

```
#Atención: este comando no deja autocompletar así que deben estar muy seguros de como estan escritos los directorios. 
#projdir = nombre del directorio donde quieren guardar la salida de VIRIDIC
#in = archivo con las secuencias fasta.
/App/viridic_v1.0_r3.6/viridic.bash projdir=/home/gama/UBA_workshop/clustering_taxonomia/final_contigs_VIRIDIC.out in=/home/gama/UBA_workshop/clustering_taxonomia/final_viral_sequences.fasta
```

Ahora tiene un directorio llamado `final_contigs_VIRIDIC.out/`donde se encuentran todos los archivos de salida de VIRIDIC. Dentro de este directorio el resultado final se encuentra en `04_VIRIDIC_out`.

```
#Para ver la matriz de similitud 
more clustering_taxonomia/VIRIDIC.out/04_VIRIDIC_out/sim_MA_genCol.csv
#Para ver los clusters generados
more clustering_taxonomia/VIRIDIC.out/04_VIRIDIC_out/clusters.csv
```

¿Cuántos clusters se generaron? ¿Coincide con la matriz de similitud?

### Generación de un dendrograma/árbol filogénetico a partir de la matriz de similitud.

Para completar este paso vamos a usar las librerias de R, ape y phagorn. Para abir R:

```
cd clustering_taxonomia
mkdir trees
cd trees
R 
```

En R debe leer el archivo de matriz de similitud

```
#Importar la matriz de similitud y volverla una matriz numerica 
mat_similitud=read.table("sim_MA_genCol.csv",sep="\t",h=T)

rownames(mat_similitud)=mat_similitud$genome

mat_similitud=mat_similitud[,-1]

#Pasarla a distancias de 0 a 1
mat_distancias=1-(mat_similitud/100)

#Tansformarla a un objeto de distancias en R
distancias <- as.dist(mat_distancias)

#Cargue las librerias
library(ape)
library(phangorn)

#Crear un arbol con Neighbour-Joining (ape)
tree_nj <- nj(distancias)

#Crear un arbol con UPGMA (phangorn)
tree_upgma <- upgma(distancias)

#Guardar los arboles en un archivo de texto. 
write.nexus(tree_nj, file='NJ_tree.nex')
write.nexus(tree_upgma, file='UPGMA_tree.nex')

#Cerrar sesion
q() #presionar Y seguido de Enter. 
```

Ahora, puede descargar los archivos para visualizarlos en iTOL (para que el taller sea mas rápido descarguelos del github Modulo4/Ejercicios). Para visualizar dirijase al sitio web iTOL (interactive Tree Of Life [https://itol.embl.de/](https://itol.embl.de/) ), cree un usuario o inicie sesión.

Ingrese a "MyTrees > Tree upload", seleccione los archivos .nex. Luego Ingrese al link con el nombre del archivo que aparece en iTOL y puede ver el árbol.



### Clasificación Taxonómica (taxmyPHAGE)

taxmyPHAGE comparar el genoma(s)  con los genomas de referencia del ICTV. Ejecutar un análisis tipo VIRIDIC. Interpreta el resultado del análisis tipo VIRIDIC para determinar si el fago pertenece a un género o especie actual. No ejecuta VIRIDIC, pero utiliza la misma fórmula para la comparación de genomas.

```
cp .bashrc.mamba .bashrc #activa ambientes mamba
conda activate tax
```

Ahora usa tu archivo fasta con tus secuencias virales (fagos o profagos) y ejecuta taxmyPHAGE:

```
taxmyphage run -i final_contigs.fasta -o tax.out
```

Importante: revisar los resultados en los archivos  **Summary_taxonomy.tsv**

Vizualiza el árbol (Ej. NJ) que generaste y colorea los fagos que lograste clasificar.

También puedes usar otras formas de clusterizar y clasificar usando taxmyPHAGE (https://github.com/amillard/tax_myPHAGE) ó usando la versión web (https://ptax.ku.dk/)



































































