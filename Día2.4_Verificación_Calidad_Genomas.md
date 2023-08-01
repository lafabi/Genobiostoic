![image](https://github.com/lafabi/Genobiostoic/assets/60276632/40d76290-f711-48df-ba71-7dceae833532)![image](https://github.com/lafabi/Genobiostoic/assets/60276632/71673b42-c0b2-4dfb-aead-96ad8654be52)# Verificación de calidad de reads en el servidor NLHPC

Para verificar la calidad de los genomas, primero hay que recibirlos de la plataforma de secuenciación y luego subirlos a los servidores de alta capacidad. Existen varias formas de transferir los archivos al servidor, que se mencionarán a continuación. Supongamos que tenemos los siguientes genomas de zorros, m2267sub2_R1.fastq.gz, m2267sub2_R2.fastq.gz, m2293sub2_R1.fastq.gz y m2293sub2_R2.fastq.gz contenidos el directorio "genomes" de nuestra máquina local, y los queremos subir al servidor remoto del NLHPC con destino al directorio /home/courses/sutdentXX/genomes. Para realizar esta tarea, ocuparemos el comando ```rsync``` junto con otros operadores de la siguiente forma:

```
rsync -azvrP -e /home/User/genomes ssh studentXX@leftraru.nlhpc.cl:/home/courses/studentXX/ 

```

>**Nota**: El comando, bajo el formato en el que está descrito, debe ejecutarse desde el directorio /home/User/, contenida en la máquina local. A grandes rasgos, el comando está indicando que se transifera el directorio "genomes" hacia el directorio studentXX/, presente en el servidor remoto.

Al trabajar con datos genómicos, muchas veces grandes en peso y también numerosos, conviene estar atentos a que las transferencias se hagan de forma correcta, es decir que los archivos no estén *truncados*. Para ello, el comando ```rsync``` no solamente nos permite transferir archivos, sino que además nos verifica la imagen de integridad de la transferencia. De esta forma, si se llegara a interrumpir la conexión de transferencia, se recupera la información ya transferida al ejecutar el mismo comando otra vez, continuando la transferencia de datos desde el punto donde se interrumpió.

Ya una vez transferidos los genomas de Zorros al servidor (esto ya lo hemos hecho para ahorar tiempo), pasaremos al primer "análsis", que es comprobar la calidad de los genomas. Para ello vamos a ejecutar el comando de FastQC de diferentes formas, luego MultiQC, y por último transferiremos los resultados a nuestra máquina local para verlos en el navegador.

Los genomas estarán depositados en el siguiente directorio ```/home/courses/studentXX/genomes/``. Crearemos un directorio dentro del directorio genomes/, quedando así  /home/courses/studentXX/genomes/QC_estudianteX/. Con esto, ya estamos listos para construir nuestros scripts y ejecutarlos

```
mkdir ~/genomes/QC_estudianteX

```

Para la elaboración de los scripts, se considera los siguientes comandos para FastQC y MultiQC
Comando general de FastQC:
```
fastqc –o ~/genomes/QC_estudianteX –t 1 –f fastq ~/genomes/m2267sub2_R2.fastq.gz
```

Comando general de MultiQC:
```
multiqc .
```
NOTA: este último se debe ejecutar desde el directorio donde se encuentran los outputs del fastqc (~/genomes/QC_estudianteX).

Tranferencia de los resultados a maquina local. Para realizar esto, se debe ejecutar el siguiente comando desde la terminal de la COMPUTADORA LOCAL. De esta forma, indicaremos que conecte con el cluster, y descargue todo el directorio *QC_estudianteX* en el WD.
```
rsync -azvrP -e ssh student88@leftraru.nlhpc.cl:/home/courses/student88/genomes/QC_estudianteX .
```


Una vez descargado este archivo procederemos a abrirlo a través de su enlace a una pagina web. Aquí veremos un resumen de la calidad de los reads entregados por la empresa de secuenciación:

 + ¿Cuántos millones de reads tenemos entre los R1 y R2?
 + ¿Cuántas secuencias duplicadas tenemos?
 + ¿Cuál es el tamaño promedio de los reads
 + ¿Poseen restos de adaptadores?
 + ¿Qué significan los colores verdes, amarillos y rojos en cada análisis?
 + ¿Cuál es la profundidad de secuenciación potencial que obtuve?
