#### Gamaliel López-Leal

###### Laboratorio de Biología Computacional y Virómica Integrativa

###### Centro de Investigación en Dinámica Celular-UAEM

[gamaliel.lopez@docentes.uaem.edu.mx](mailto:gamaliel.lopez@docentes.uaem.edu.mx)





## Ensambles *de Novo* de genomas virales

Para este paso usaremos un programa que se llama **metaviralsapdes**. Es de la colección de herramientas
para en ensambles de **spades**. Para mayor información pueden consultar en siguiente enlace: https://github.com/ablab/spades

Antes de ejecutar `metaviralspades.py`  debes de correr el siguiente comando:

```
PATH=/home/App/SPAdes-3.15.5:$PATH
```

Nota: Esta es una particularidad de nuestro servidor y no es necesario correr ese comando en
otros servidores o equipos de computo.

Como cualquier otra herramienta bioinformática podemos consultar el menú con los comandos: `--help`,
`-h`, `man`, por mencionar algunos.

```
metaviralspades.py --only-assembler  -k 21,33,55,77,99,127 -1 Reads-R1-v3_val_1.fq -2 Reads-R2-v3_val_2.fq -o MetaViral_results
```

Ahora en el subdirectorio `MetaViral_results` se encuentran los resultados del ensamble. Revisemos el archivo **contigs.fasta**, que es el contiene los genomas virales.



### Práctica

> Ahora hagan un ensamble (solo con spades) *de novo* usando las lecturas Reads-R1-v3\_val\_1.fq y Reads-R2-v3\_val\_2.fq. 

Pero esta vez utiliza el programa `spades.py` agrega las opciones de -k 21,33,55,77,99,127 `--careful` `--only-assembler`. 



## Estadísticas generales del ensamble

Existen varias herramientas para revisar la estadística general de los ensambles. Para esto, usaremos una herramienta llamada `quast`. Para mayor información consultar el siguiente enlace: [https://github.com/ablab/quast](https://github.com/ablab/quast)

```
quast.py MetaViral_contigs.fasta spades_contigs.fasta  -o quast_results
```

Para mayor información de los archivo de salida de Quast puedes visitar: [https://hoytpr.github.io/bioinformatics-semester/materials/genomics-assembly-reporting/](https://hoytpr.github.io/bioinformatics-semester/materials/genomics-assembly-reporting/)



## Verificación de los contigs virales

Un paso importante a evaluar cuando hacemos ensambles *de Novo* a partir de aproximaciones de metagenómica viral es la verificación o validación de contigs virales. Para esto existen varias herramientas. En este paso usaremos **VirSorter2** con la finalidad de validar o recuperar los contigs virales. 

```
cp .bashrc.mamba .bashrc #activa ambientes mamba
mamba activate VS2d
```

```
virsorter run --keep-original-seq -i contigs.fasta -w vs2-pass --include-groups dsDNAphage,ssDNA --min-length 50000 --min-score 0.5 -j 5 all
```

Podemos revisar el reporte de VirSorter2 en el archivo **final-viral-score.tsv**























































