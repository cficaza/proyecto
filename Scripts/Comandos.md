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
* NOTA! Para crear una carpeta usar el comando:
  $ mkdir Proyecto
* Entrar a nuestra carpeta del proyecto y observar que nuestro archivo zip se haya copiado correctamente con el comando:
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
* Si la secuencia no corre rápido puede deberse a que es una secuencia muy pesada, para eso recortaremos las secuencias para que tengan una misma longitud final de 3000, esto se hará con el comando:
  $ awk '
  BEGIN {RS=">"; FS="\n"}
  NR > 1 {
    header = $1
    seq = ""
    for(i=2; i<=NF; i++) seq = seq $i
    print ">" header
    print substr(seq, 1, 3000)
  }
' Gen_rps16_Burmeistera.fasta > Gen_rps16_recortado3000.fasta
* Una vez realizado el corte correr la secuencia nuevamente 
* Realizar el comando ls y verificar que nuestro archivo muscle se haya generado correctamente con el comando:
  $ cat muscle_Gen_rps16_recortado3000.fasta
* Cargar el programa de iqtree con el siguiente comando:
  $ module load iqtree/2.2.2.6
* Correr el programa iqtree con el archivo fasta alineado:
  $ iqtree -s muscle_Gen_rps16_recortado3000.fasta
* Correr el comando "ls" y observar que se haya creado nuestra filogenia, la cual debería terminar en .treefile
* Una vez observado nuestra filogenia ir a una terminal nueva de git bash y entrar al escritorio con el comando:
  $ cd Desktop/
* OJO! El comando anterior puede variar
* Descargar nuestra filogenia con el siguiente comando: scp dechavez@hoffman2.idre.ucla.edu:/u/scratch/d/dechavez/Bioinformatica-PUCE/RediseBio/ClaudiaIc/BurmeisteraProyecto/muscle_Gen_rps16_recortado3000.fasta.treefile .
* Una vez descargada nuestra filogenia subirla a figtree 
* Finalmente dentro de figtree ir a "file" luego "open" y abrir nuestro archivo "muscle_Gen_rps16_recortado3000.fasta.treefile"
* Una vez realizado este último paso nuestra filogenia final aparece
