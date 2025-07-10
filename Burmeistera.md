# Análisis filogenético del gen rps16 dentro del género Burmeistera

Autora: Claudia Icaza


## Q1. ¿En qué organismo o grupo de organismos vas a trabajar?
Trabajaré con el género de plantas Burmeistera, familia Campanulaceae.

## Q2. Brevemente describe qué piensas hacer en tu proyecto
Filtrar secuencias, realizar alineamientos múltiples y generar árboles filogenéticos preliminares en secuencias que tengan el gen rps16 el cual es un gen que codifica una proteína ribosomal que forma parte de la subunidad 40S. Pertenece a la familia S9P de proteínas ribosomales.

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

## Q7 Cómo realizar el análisis
* Ingresar al programa GitBash
* Entrar a hoffman con el comando:
  $ ssh "correo institucional" y colocar la clave 
* Pedir un nodo computacional para pedir memoria y tiempo de uso del programa con el comando:
  $ qrsh -l h_data=7G,h_vmem=30G,h_rt=2:00:00 
* entrar a la carpeta de SCRATCH con:
  $ cd $SCRATCH/
* entrar a la carpeta de la materia con:
  $ cd Bioinformatica-PUCE/
* entrar a la carpeta de maestrías para sacar nuestras secuencias:
  $ cd MastBio/
* descargarnos las secuencias del gen rps16 para el género Burmeistera
  $  /u/scratch/d/dechavez/Bioinformatica-PUCE/MastBio/edirect/esearch -db nuccore -query "rps16 [GENE] AND Burmeistera[ORGN]" | efetch -format fasta > Gen_rps16_Burmeistera.zip
* copiar el archivo en nuestra carpeta del proyecto
  $ cp Gen_rps16_Burmeistera.zip ../RediseBio/ClaudiaIc/BurmeisteraProyecto/
* observar que nuestro archivo zip se haya copiado correctamente con el comando:
  $ ls 
*  descomprimir nuestro archivo con:
  $ unzip Gen_rps16_Burmeistera.zip
*  
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
