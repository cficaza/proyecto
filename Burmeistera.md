# Análisis filogenético del gen rbcL dentro del género Burmeistera

Autora: Claudia Icaza


## Q1. ¿En qué organismo o grupo de organismos vas a trabajar?
Trabajaré con el género de plantas Burmeistera, familia Campanulaceae.

## Q2. Brevemente describe qué piensas hacer en tu proyecto
Filtrar secuencias, realizar alineamientos múltiples y generar árboles filogenéticos preliminares en secuencias que tengan el gen rbcL el cual tiene como función principal codificar la proteína RuBisCO

## Q3. ¿Qué programas voy a usar en mi proyecto y cómo descargarlos?
* git bash = Entrar al link https://carpentries.github.io/workshop-template/install_instructions/#shell y escoger la opción para tu computadora en la sección "Git"
* muscle = https://www.ebi.ac.uk/jdispatcher/msa/muscle?stype=protein
* fig tree = Entrar al siguiente link https://github.com/rambaut/figtree/releases y descargar el zip "FigTree.v1.4.4.zip"
* iqtree = https://iqtree.github.io/ descargar la versión 3.0.1

  ## ¿Cómo instalarlos?
  * git bash
  * muscle = usar dentro del mismo link 
  * fig tree = descomprimir el archivo zip y abrir el programa FigTree.v1.4.4
  * iqtree = descomprimir el archivo zip, entrar a la carpeta bin y abrir el archivo iqtree3, si 

## Q4. Sube una foto que represente tu organismo o grupo de organismos
![Alt text](https://inaturalist-open-data.s3.amazonaws.com/photos/12875007/large.jpg)

## Q5 Propósito del programa de tu proyecto
Estudiar la diversidad genética y relaciones evolutivas dentro del género.

## Q6 Requisitos para ejecutar el programa
* Descargar los programas básicos necesarios para el análisis filogenético como muscle, iqtree y figtree
* Descargar las filogenias que se vayan a utilizar, en este caso serán las filogenias de las cuales se tengan los datos necesarios para observar una presencia del gen dentro de las especies de Burmeistera

## Q7 Cómo usar el programa
* Ingresar al programa GitBash y moverse hacia el escritorio de la computadora con el comando:
  $ cd Desktop/ 
* Una vez se encuentre dentro del escritorio crear una carpeta que sea únicamente utilizada para el proyecto y así evitar confusiones de los datos, para esto se usará el siguiente comando:
  $ mkdir BurmeisteraProyecto
* Para este trabajo es necesario conseguir las secuencias de las especies por lo que será necesario entrar a NCBI, escoger la opción de nucleótidos y a lado en la barra de búsqueda colocar el género o la especie de la cual se está buscando la secuencia nucleotídica y seguida de la misma el gen que se quiere buscar. Descargar al escritorio en formato FASTA
* Copiar el programa de muscle dentro de la carpeta del proyecto la cual se encuentra en nuestro escritorio con el siguiente comando 
  $ cp ../../muscle3.8.31_i86linux64 ./
* Alinear las secuencias con el comando:
  $ for rbcL in *.fasta
  do
  ./muscle3.8.31_i86linux64 -in $rbcL -out muscle_$rbcL -maxiters 1 -diags
  done
* Correr el comando "ls" y observar que se haya alineado nuestra secuencia, esta debería terminar en .fasta 
* Cargar el programa de iqtree con el siguiente comando:
  $ module load iqtree/2.2.2.6
* Correr el programa iqtree con el archivo fasta alineado:
  $ iqtree -s muscle_sequence.fasta
* Correr el comando "ls" y observar que se haya creado nuestra filogenia, la cual debería terminar en .treefile
* Descargar nuestra filogenia con el siguiente comando: scp dechavez@hoffman2.idre.ucla.edu:/u/scratch/d/dechavez/Bioinformatica-PUCE/RediseBio/ClaudiaIc/BurmeisteraProyecto/muscle_sequence.fasta.treefile .
* Una vez descargada nuestra filogenia subirla a figtree 
* Finalmente dentro de figtree ir a "file" luego "open" y abrir nuestro archivo "muscle_sequence.fasta.treefile"
