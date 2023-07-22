# Genoma de referencia para la reconstrucción de genomas a partir de lecturas cortas: Dia 2

Existen dos principales formas de reconstruir genomas: 1) A patir de genomas de Referencias y 2) A partir de un ensamblaje *de novo*.

En este tutorial nos enfocaremos en realizar el ejercicio de reconstrucción de genomas a partir de  **genomas de referencia** en lecturas cortas (short reads).
 
## Dónde encuentro los genomas de Referencia: Repositorios de Genomas.

El Centro Nacional de Información Biotecnológica [NCBI](https://www.ncbi.nlm.nih.gov/) es una parte de la Biblioteca Nacional de Medicina de los Estados Unidos, la cual forma parte del Instituto Nacional de la Salud (NIH). El NCBI es un recurso integral de información en biología molecular y  desempeña un papel vital en el avance de la investigación en diversos campos de la biología, entre ellos la Genómica.
El NCBI brinda acceso a diversas bases de datos y herramientas que son ampliamente utilizadas por científicos, investigadores y profesionales de la salud. Algunos de los recursos más conocidos ofrecidos por el NCBI incluyen:

[NCBI Assembly](https://www.ncbi.nlm.nih.gov/assembly):  Este repositorio recopila, almacena y organiza **secuencias genómicas en genomas completos** o parciales dentro de las bases de datos de la plataforma del NCBI. Podemos encontrar secuenciaciones genómicas en bruto a nivel de contigs, scaffolds y cromosomas. Esta herramienta es la que utizaremos a continuación para descargar y analizar y escoger los genomas de referencias.

Mencionamos además estas herramientas que ofrece el NCBI de relevante importancia:

[GenBank](https://www.ncbi.nlm.nih.gov/genbank/): Una base de datos de secuencias genéticas que recopila y almacena secuencias de ADN y ARN de diversos organismos. GenBank sirve como un repositorio central para los datos de secuencias generados por investigadores de todo el mundo.

[NCBI Gene](https://www.ncbi.nlm.nih.gov/gene/): Una base de datos que proporciona información sobre genes y sus anotaciones funcionales, incluyendo secuencias de genes, ubicaciones genómicas y datos relacionados. Ayuda a los investigadores a estudiar el papel de los genes en diversos procesos biológicos y enfermedades.

[PubMed](https://pubmed.ncbi.nlm.nih.gov/): Una base de datos de literatura biomédica que contiene millones de citas y resúmenes de revistas científicas. Es una herramienta valiosa para realizar búsquedas bibliográficas y mantenerse al día con las últimas investigaciones.

Si trabajas con conservación biológica, también te puede interesar los siguientes repositorios de genomas: 

> + https://www.dnazoo.org/
> + https://vertebrategenomesproject.org/


### Consideraciones para escoger Genoma de referencia

Dependiendo de la pregunta de tu proyecto existirán ciertos atributos de los genoma de referencia disponibles que deberás revisar y escoger, Entre ellos:  

> + Nivel de ensamblaje: Scaffolds vs Cromosomas
> + Cariotipaje según tu modelo de estudio: Número de Cromosomas parecido al modelo?
> + Calidad de Cobertura: Cobertura de Secuenciación
> + Relación Filogenética con tu modelo de estudio: Qué tan emparentados estan con nuestro modelo de estudio
> + Representación del formato del Genoma en el Repositorio: Formato GenBank vs RefSeq
> + Consideraciones sobre la Tecnología de secuenciación: Ilumina, PacBio, etc.


## Busquemos Genomas de referencias de las siguientes especies en el [NCBI Assembly](https://www.ncbi.nlm.nih.gov/assembly)

```
Pudu puda
```
```
Spheniscus humboldti
```
```
Rhinoderma darwinii
```
```
Zorrito de Darwin
```

Con base en estas consideraciones,hagamos un ejercicio práctico para buscar genomas de Referencia 


Construye una tabla comparativa entre los atributos de cada uno de los posibles genomas de referencia encontrados en el NCBI. En caso que no existan genoma de referencias de los modelos propuestos, cuáles otros pudieras escoger y por qué?. A continuación mostraremos un diagrama con base en la toma de decisiones que debiéramos tomar en consideración a la hora de escoger el genoma de referencia. Ten en consideración que la escogencia dependerá de tu pregunta de investigación.


![Pregunta-proyecto](https://github.com/lafabi/Genobiostoic/blob/main/Pregunta-proyecto.png)

