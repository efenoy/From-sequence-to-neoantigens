# NetMHCpan 

Esta herramienta predice union de peptidos a moleculas de MHC utilizando redes neuronales artificiales (ANN). El metodo esta entrenado con una combinacion de mas de 180,000 datos de union obtenidos a partir de espectrometria de masas que cubre 55 diferentes MHC de humanos y ratones. El set de datos de entrenamiento cuenta tambien con peptidos con mediciones de afinidad de union, los cuales cubren 172 moleculas de MHC de humano (*HLA-A, B, C, E*), raton (*H-2*), bovinos (*BoLA*), primates (*Patr, Mamu, Gogo*) y porcinos (*SLA*).

Una particularidad que caracteriza a netMHCpan es la integracion de las secuencias del peptido y del MHC durante el entrenamiento, lo que permite realizar asociaciones entre elementos de ambas moleculas. La ventaja principal de esto es que, asi como la herramienta aprende a predecir secuencias peptidicas con aminoacidos que nunca ha visto, tambien lo puede hacer en la secuencia del MHC, lo que le permite realizar predicciones acertadas para nuevas moleculas.

Tambien, gracias a la implementacion del algoritmo *nnaling* que se encarga de subsamplear y alinear las secuencias peptidicas, la herramienta no esta limitada en el largo de entrada que puede recibir.

La herramienta esta disponible desde su servidor web: [netMHCpan](http://www.cbs.dtu.dk/services/NetMHCpan/) o puede ser descargada de forma gratuita para usuarios academicos: [Descarga](http://www.cbs.dtu.dk/cgi-bin/nph-sw_request?netMHCpan).

Si quieren investigar mas detalladamente pueden bajarse el paper de la herramienta [aca](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5679736).

En la maquina virtual tenemos instalado ya el programa, se puede utilizar desde la consola de comandos tipeando **netMHCpan-4.0**. Si no le pasamos ningun argumento nos va a mostrar todas las opciones que contempla con una breve descripcion de cada una.

Por defecto admite un archivo fasta con una o mas secuencias proteicas. Todas estas son ventaneadas para obtener peptidos del/los largos deseados sobre los cuales hacer predicciones. Uno tambien puede utilizar el argumento **-p** para indicar que el archivo de entrada es una lista de peptidos, en ese caso solo se haran predicciones sobre estos.

Mediante la opcion **-a** debemos especificar una o mas moleculas de MHC para predecir la union. En caso de ser varias se deben separar por coma, sin espacios (ej. HLA-A01:01,HLA-B27:02 ).

Con esto podemos correr nuestra primera prediccion con netMHCpan

```Bash
netMHCpan-4.0 -a HLA-A01:01 secuencias.fasta
```

La salida del programa es por consola pero podemos redireccionarla a un archivo con el simbolo mayor (**>**). A continuacion tenemos un ajemplo de salida:

```
# NetMHCpan version 4.0

# Tmpdir made /usr/opt/www/webface/tmp/server/netmhcpan/59DBCCFF00005A84DAFF1311/netMHCpanVszuD8
# Input is in FSA format

# Peptide length 8,9,10,11,12

# Make Eluted ligand likelihood predictions

HLA-A03:01 : Distance to training data  0.000 (using nearest neighbor HLA-A03:01)

# Rank Threshold for Strong binding peptides   0.500
# Rank Threshold for Weak binding peptides   2.000
-----------------------------------------------------------------------------------
  Pos          HLA         Peptide       Core Of Gp Gl Ip Il        Icore        Identity     Score   %Rank  BindLevel
-----------------------------------------------------------------------------------
   15  HLA-A*03:01       HQAAMQMLK  HQAAMQMLK  0  0  0  0  0    HQAAMQMLK     Gag_180_209 0.5697290  0.2857 <= SB
   14  HLA-A*03:01      GHQAAMQMLK  GQAAMQMLK  0  1  1  0  0   GHQAAMQMLK     Gag_180_209 0.2137130  1.1582 <= WB
    7  HLA-A*03:01       TMLNTVGGH  TMLNTVGGH  0  0  0  0  0    TMLNTVGGH     Gag_180_209 0.0487720  3.0466
    8  HLA-A*03:01       MLNTVGGHQ  MLNTVGGHQ  0  0  0  0  0    MLNTVGGHQ     Gag_180_209 0.0319510  3.7842
   13  HLA-A*03:01     GGHQAAMQMLK  GQAAMQMLK  0  1  2  0  0  GGHQAAMQMLK     Gag_180_209 0.0313010  3.8215
   12  HLA-A*03:01    VGGHQAAMQMLK  VQAAMQMLK  0  1  3  0  0 VGGHQAAMQMLK     Gag_180_209 0.0166440  5.2079
   15  HLA-A*03:01      HQAAMQMLKE  HQAAMQMLK  0  0  0  0  0    HQAAMQMLK     Gag_180_209 0.0124970  5.9719
   16  HLA-A*03:01        QAAMQMLK  QAA-MQMLK  0  0  0  3  1     QAAMQMLK     Gag_180_209 0.0086270  7.1279
   21  HLA-A*03:01       MLKETINEE  MLKETINEE  0  0  0  0  0    MLKETINEE     Gag_180_209 0.0079270  7.4157
..
..
-----------------------------------------------------------------------------------

Protein Gag_180_209. Allele HLA-A*03:01. Number of high binders 1. Number of weak binders 1. Number of peptides 105

Link to Allele Frequencies in Worldwide Populations HLA-A03:01
-----------------------------------------------------------------------------------
```

Ademas de la informacion sobre los parametros que se utilizaron para correr el programa tenemos la prediccion que muestra los siguientes campos:  
**Pos:** La posicion del peptido en la secuencia si se corrio sobre un *fasta*.  
**HLA:** El alelo al que se estra prediciendo la union.  
**Peptide:** El peptido sobre el que se llevo a cabo la prediccion.  
**Core:** La correccion de NNAlign para fijar el largo del peptido al core usual de los MHC clase I que es de 9 aminoacidos.  
**Of, Gp, Gl, Ip, Il,:** informacion sobre las inserciones, deleciones y offset incluidos para adecuar el peptido al core.  
**Icore:** Core de interaccion. Contine el core con sus posibles inserciones o deleciones.  
**Identity:** El ID de la proteina de la cual proviene el peptido.  
**Score:** Puntaje provisto por el metodo, va de 0 a 1. Mientras mas cercano a 1 mayor afinidad predicha.  
**%Rank:** Correccion por alelo. Dado que diferentes alelos se unen con diferente afinidad a sus ligandos se calcula un score segun la posicion esperada del peptido predicho en un ranking que contenga 100.000 peptidos aleatorios predichos para ese alelo. Asi, peptidos con %Rank<2 son considerados *strong binders* aun si su score no es tan alto.  
**BindLevel:** Indica peptidos con alta afinidad (SB) y afinidad debil (WB).  

Por ultimo tenemos un resumen de los resultados obtenidos.

