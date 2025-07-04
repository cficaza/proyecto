# Análisis bioinformático del gen rbcL dentro del género Burmeistera

Claudia Icaza


## Q1. ¿En qué organismo o grupo de organismos vas a trabajar?
Trabajaré con el género de plantas Burmeistera, familia Campanulaceae.

## Q2. Brevemente describe qué piensas hacer en tu proyecto
Filtrar secuencias, realizar alineamientos múltiples y generar árboles filogenéticos preliminares en secuencias que tengan el gen rbcL el cual tiene como función principal codificar la proteína RuBisCO

## Q3. ¿Qué programas voy a usar en mi proyecto?
* git bash 
* muscle 
* fig tree
* iqtree

## Q4. Sube una foto que represente tu organismo o grupo de organismos
![Alt text](https://inaturalist-open-data.s3.amazonaws.com/photos/12875007/large.jpg)

## Q5 Propósito del programa de tu proyecto
Estudiar la diversidad genética y relaciones evolutivas dentro del género.

## Q6 Requisitos para ejecutar el programa
Descargar los programas básicos necesarios para el análisis como muscle, iqtree y figtree
Descargar las filogenias que se vayan a utilizar, en este caso serán las filogenias de las cuales se tengan los datos necesarios para observar una presencia del gen dentro de las especies de Burmeistera

## Q7 Cómo usar el programa
Ingresar al programa GitBash y moverse hacia el escritorio de la computadora con el comando:
  $ cd Desktop/ 
Una vez se encuentre dentro del escritorio crear una carpeta única para el proyecto y así evitar confusiones de los datos, para esto se usará el siguiente comando:
  $ mkdir BurmeisteraProyecto
Para este trabajo es necesario conseguir las secuencias de las especies por lo que será necesario entrar a NCBI, escoger la opción de nucleótidos y a lado en la barra de búsqueda colocar el género o la especie de la cual se está buscando la secuencia nucleotídica y seguida de la misma el gen que se quiere buscar. Descargar al escritorio
Cambiar el formato de Phylip a Fasta con:
  $ cp ../../Phylip2Fasta.pl ./
Copiar el programa de muscle dentro de la carpeta del proyecto con el siguiente comando 
  $ cp ../../muscle3.8.31_i86linux64 ./
Alinear las secuencias con el comando:
  $
Cargar el programa de iqtree con el siguiente comando:
  $ module load iqtree/2.2.2.6
