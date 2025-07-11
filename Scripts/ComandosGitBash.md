* Ingresar al programa GitBash


* Entrar a hoffman con el comando:
  $ ssh "correo institucional" y colocar la clave 

* Pedir un nodo computacional para pedir memoria y tiempo de uso del programa con el comando:
  $ qrsh -l h_data=7G,h_vmem=30G,h_rt=2:00:00 

* Entrar a la carpeta de SCRATCH con:
  $ cd $SCRATCH/

* Entrar a la carpeta de la materia con:
  $ cd Bioinformatica-PUCE/

* Entrar a la carpeta de maestrías para sacar nuestras secuencias:
  $ cd MastBio/

* Descargarnos las secuencias del gen rps16 para el género Burmeistera
  $  /u/scratch/d/dechavez/Bioinformatica-PUCE/MastBio/edirect/esearch -db nuccore -query "rps16 [GENE] AND Burmeistera[ORGN]" | efetch -format fasta > Gen_rps16_Burmeistera.zip

* Copiar el archivo en nuestra carpeta del proyecto
  $ cp Gen_rps16_Burmeistera.zip ../RediseBio/ClaudiaIc/BurmeisteraProyecto/

* Observar que nuestro archivo zip se haya copiado correctamente con el comando:
  $ ls 

* Descomprimir nuestro archivo con:
  $ unzip Gen_rps16_Burmeistera.zip

* NOTA! Si el archivo no se descomprime porque no es un archivo zip hacer head a ver lo que tiene el archivo con el comando:
  $ head Gen_rps16_Burmeistera.zip

* Renombrar el archivo como fasta con el comando:
  $ mv Gen_rps16_Burmeistera.zip Gen_rps16_Burmeistera.fasta

* Copiar el programa de muscle dentro de la carpeta del proyecto la cual se encuentra en nuestro escritorio con el siguiente comando 
  $ cp ../../muscle3.8.31_i86linux64 ./

* Alinear las secuencias con el comando:
  $ for rps16 in *.fasta
  do
  ./muscle3.8.31_i86linux64 -in $rps16 -out muscle_$rps16 -maxiters 1 -diags
  done

* Si la secuencia no corre es porque puede ser algo pesada, para eso deberemos usar los comandos de Header por lo que deberemos cancaelar el primer alineamiento con ctrl + C, luego entrar a la carpeta de Scripts la cual está dentro de la carpeta de Rediseño y copiar a nuestra carpeta del proyecto el nano de Header:
  $ cp Header.sh ../ClaudiaIc/BurmeisteraProyecto/

* Modificar Header con:
  $ #!/bin/bash

#$ -l highp,h_rt=30:00:00,h_data=30G
#$ -pe shared 1
#$ -N CFIRGeneCalculator
#$ -cwd
#$ -m bea
#$ -o /u/scratch/d/dechavez/Bioinformatica-PUCE/RediseBio/ClaudiaIc/BurmeisteraProyecto/GeneCalculator.out
#$ -e /u/scratch/d/dechavez/Bioinformatica-PUCE/RediseBio/ClaudiaIc/BurmeisteraProyecto/GeneCalculator.err
#$ -M dechavezv

source /u/local/Modules/default/init/modules.sh
module load iqtree/2.2.2.6

* alineamiento:

for rps16 in *.fasta
  do
  ./muscle3.8.31_i86linux64 -in $rps16 -out muscle_$rps16 -maxiters 1 -diags
  done 

* Para correr nuestro alineamiento usar el comando:
  $ qsub Header.sh 

* Verificar que se esté corriendo nuestro alineamiento con:
  $ myjobs

* Verificar que salga r en state, eso significa que está corriendo 
