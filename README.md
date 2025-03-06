# Tema 20: Anotación de genomas

## Estructura de la práctica:

1. Instalación de programas
2. Obtención de datos
3. Anotación de un genoma
4. Identificación de genes de virulencia
5. Identificación de genes de resistencia
6. Identificación de integrones
7. Identificación de rutas metabolicas
8. Identificación de grupos de genes biosintéticos de metabolitos secundarios
9. Visualización del genoma

## Metodología:

## 1. Instalación de programas

### Instalar los siguientes programas en un ambiente de conda

```bash
conda create -n annotation_01 -c bioconda prokka abricate integron_finder mgcplotter

conda create -n annotation_02 -c bioconda rgi
```

> **Comentario:** 
> - `prokka`: Anotación rápida de genomas procariotas.
> - `abricate`: Detección masiva de contigs para genes de resistencia antimicrobiana y virulencia.
> - `integron_finder`: Detecta integrones en genomas procariotas.
> - `mgcplotter`: Visualiza el contexto genético de un genoma.
> - `rgi`: Identificador de genes de resistencia a antibióticos.

> **Otras herramientas bioinformáticas en línea:**

> - `AntiSMASH`: https://antismash.secondarymetabolites.org/#!/start 
> - `KAAS`: https://www.genome.jp/kegg/kaas/ 
> - `Proksee`: https://proksee.ca/ 

## 2. Obtención de los datos 

```bash
cd ~/genomics/assembly/nanopore

gdown https://drive.google.com/uc?id=1cIZYfPZVUQLKW_ixWvhjiJrSqmxeY78A
```

## 3. Anotación de un genoma

```bash
cd ~/genomics

mkdir annotation

cd annotation

conda activate annotation_01

prokka --outdir prokka --cpus 2 --addgenes --genus Shigella --species sonnei --strain INS2025 --prefix m01 /home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta
```

> **Comentario:** 
> - `--addgenes`: Esta opción le indica a Prokka que añada los genes como características en el archivo GFF resultante. Es muy util para visualizaciones posteriores.
> - `--prefix m01`: Establece el prefijo para los nombres de los genes y otras características anotadas. En este caso, todas las características anotadas comenzarán con "m01_". Esto es útil para mantener la organización de los resultados, especialmente cuando se anotan múltiples genomas.
> - `--genus Shigella`: Especifica que el genoma pertenece al género Shigella. Esto ayuda a Prokka a seleccionar las bases de datos y modelos de predicción de genes más apropiados para este género.
> - `--species sonnei`: Especifica que el genoma pertenece a la especie Shigella sonnei. Esto refina aún más la selección de bases de datos y modelos.
> - `--strain INS2025`: Especifica la cepa del organismo como INS2025. Esto es útil para mantener la trazabilidad y la organización de los resultados, especialmente si estás anotando múltiples cepas.
> - `/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta`: Especifica la ruta al archivo de secuencia de entrada en formato FASTA. Este es el genoma ensamblado que se va a anotar. En este caso, se trata de un ensamblaje generado con Flye y pulido con Racon, obtenido de datos de secuenciación Nanopore.

```bash
ls -lh prokka

-rw-rw-r-- 1 ins_user ins_user 483K Uya   6 12:39 m01.err
-rw-rw-r-- 1 ins_user ins_user 1,7M Uya   6 12:39 m01.faa
-rw-rw-r-- 1 ins_user ins_user 4,5M Uya   6 12:39 m01.ffn
-rw-rw-r-- 1 ins_user ins_user 4,8M Uya   6 12:35 m01.fna
-rw-rw-r-- 1 ins_user ins_user 4,8M Uya   6 12:39 m01.fsa
-rw-rw-r-- 1 ins_user ins_user  11M Uya   6 12:39 m01.gbk
-rw-rw-r-- 1 ins_user ins_user 6,7M Uya   6 12:39 m01.gff
-rw-rw-r-- 1 ins_user ins_user  80K Uya   6 12:39 m01.log
-rw-rw-r-- 1 ins_user ins_user  19M Uya   6 12:39 m01.sqn
-rw-rw-r-- 1 ins_user ins_user 1,4M Uya   6 12:39 m01.tbl
-rw-rw-r-- 1 ins_user ins_user 501K Uya   6 12:39 m01.tsv
-rw-rw-r-- 1 ins_user ins_user  106 Uya   6 12:39 m01.txt
```

> **Comentario:** 
> - `m01.err`: Este archivo contiene los mensajes de error generados durante la ejecución de Prokka. Si está vacío o contiene pocos mensajes, significa que Prokka se ejecutó sin problemas importantes.
> - `m01.faa`: Contiene las secuencias de aminoácidos (proteínas) predichas por Prokka en formato FASTA.
> - `m01.ffn`: Contiene las secuencias de nucleótidos de los genes codificantes de proteínas predichos por Prokka en formato FASTA.
> - `m01.fna`: Contiene la secuencia del genoma de entrada original en formato FASTA.
> - `m01.fsa`: Este archivo, en este caso, es identico al m01.fna, y contiene la secuencia del genoma de entrada original en formato FASTA con informaciones extras en el encabezado.
> - `m01.gbk`: Contiene la anotación completa del genoma en formato GenBank. Este es uno de los archivos de salida más importantes, ya que contiene información detallada sobre los genes, sus funciones y otras características anotadas.
> - `m01.gff`: Contiene la anotación del genoma en formato GFF (General Feature Format). Este formato es ampliamente utilizado para visualizar y manipular anotaciones genómicas.
> - `m01.log`: Contiene un registro detallado de la ejecución de Prokka, incluyendo los comandos ejecutados y los resultados intermedios.
> - `m01.sqn`: Contiene la anotación del genoma en formato Sequin. Este formato se utiliza principalmente para enviar anotaciones a GenBank.
> - `m01.tbl`: Contiene una tabla de características anotadas en un formato que se puede utilizar para crear archivos de envío a GenBank.
> - `m01.tsv`: Contiene la anotación del genoma en formato TSV (Tab Separated Values). Este formato es muy útil para trabajar con la información de la anotación en hojas de cálculo o con programas de análisis de datos.
> - `m01.txt`: Contiene un resumen muy breve de la ejecución de Prokka.

```bash
cat prokka/m01.txt

organism: Shigella sonnei INS2025 
contigs: 4
bases: 4945468
CDS: 5194
gene: 5312
rRNA: 22
tRNA: 95
tmRNA: 1
```

```bash
head prokka/m01.faa

>COIJMHOG_00007 HTH-type transcriptional regulator HdfR
MDTELLKTFLEVSRTRHFGRAAESLYLTQSAVSFRIRQLENQLGVNLFTRHRNNIRLTAA
GEKLLPYAETLMSTWQAARKEVAHTSRHNEFSIGASASLWECMLNQWLGRLYQNQDAHTG
LQFEARIAQRQSLVKQLHERQLDLLITTEAPKMDEFSSQLLGYFTLALYTSAPSKLKGDL
NYLRLEWGPDFQQHEAGLIGADEVPILTTSSAELAQQQIAMLNGCTWLPVSWARKKGGLH
TVVDSTTLSRPLYAIWLQNSDKNALIRDLLKINVLDEVY
>COIJMHOG_00008 hypothetical protein
MAESFTTTNRYFDNKHYPRGFSRHGDFTIKEAQLLERHGYAFNELDLGKREPVTEEEKLF
VAVCRGEREPVTEAERVWSKYMTRIKRPKRFHTLSGGKPQVEGAEDYTDSDD
>COIJMHOG_00009 Competence protein ComM
```

## 4. Identificación de genes de virulencia

```bash
cd ~/genomics/annotation

mkdir abricate

cd abricate

abricate --list

DATABASE	SEQUENCES	DBTYPE	DATE
argannot	2223	nucl	2025-Jan-14
ecoh	597	nucl	2025-Jan-14
ncbi	5386	nucl	2025-Jan-14
megares	6635	nucl	2025-Jan-14
resfinder	3077	nucl	2025-Jan-14
card	2631	nucl	2025-Jan-14
plasmidfinder	460	nucl	2025-Jan-14
vfdb	2597	nucl	2025-Jan-14
ecoli_vf	2701	nucl	2025-Jan-14
```

> **Comentario:** 
> - `argannot`: A database of antibiotic resistance genes.
> - `ecoh`: A database of E. coli outer membrane proteins.
> - `ncbi`: A database of antimicrobial resistance genes from NCBI (National Center for Biotechnology Information).
> - `megares`: A database of antimicrobial resistance genes and their associated phenotypes.
> - `resfinder`: A database of acquired antimicrobial resistance genes.
> - `card`: The Comprehensive Antibiotic Resistance Database, a curated collection of antibiotic resistance genes and associated information.
> - `plasmidfinder`: A database of plasmid replicons, which are often associated with the spread of resistance genes.
> - `vfdb`: The Virulence Factors Database, a database of bacterial virulence factors.
> - `ecoli_vf`: A database of E. coli virulence factors.

```bash
abricate --db vfdb /home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta > m01_vfdb.tab

head m01_vfdb.tab

#FILE	SEQUENCE	START	END	STRAND	GENE	COVERAGE	COVERAGE_MAP	GAPS	%COVERAGE	%IDENTITY	DATABASE	ACCESSION	PRODUCT	RESISTANCE
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	354682	355973	+	espX5	1-1293/1293	========/======	1/1	99.92	95.51	vfdb	NP_290699	(espX5) Type III secretion system effector EspX5 [LEE encoded T3SS (SS020)] [Escherichia coli O157:H7 str. EDL933]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	705737	707157	-	espX1	1-1422/1422	========/======	1/1	99.93	94.52	vfdb	NP_285716	(espX1) Type III secretion system effector EspX1 [LEE encoded T3SS (SS020)] [Escherichia coli O157:H7 str. EDL933]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1247629	1248399	-	entD	1-771/771	===============	0/0	100.00	93.52	vfdb	NP_752599	(entD) phosphopantetheinyl transferase component of enterobactin synthase multienzyme complex [Enterobactin (VF0228)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1248424	1250664	-	fepA	1-2241/2241	===============	0/0	100.00	96.34	vfdb	NP_752600	(fepA) ferrienterobactin outer membrane transporter [Enterobactin (VF0228)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1250907	1252109	+	fes	1-1203/1203	===============	0/0	100.00	96.43	vfdb	NP_752602	(fes) enterobactin/ferric enterobactin esterase [enterobactin (IA019)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1252327	1256156	+	entF	1-3830/3882	===============	0/0	98.66	95.82	vfdb	NP_752604	(entF) enterobactin synthase multienzyme complex component ATP-dependent [Enterobactin (VF0228)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1257554	1258369	-	fepC	1-816/816	===============	0/0	100.00	96.81	vfdb	NP_752606	(fepC) ferrienterobactin ABC transporter ATPase [Enterobactin (VF0228)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1258366	1259358	-	fepG	1-993/993	===============	0/0	100.00	94.76	vfdb	NP_752607	(fepG) iron-enterobactin ABC transporter permease [Enterobactin (VF0228)] [Escherichia coli CFT073]	
/home/ins_user/genomics/assembly/nanopore/m01_flye.racon.fasta	contig_1	1259355	1260371	-	fepD	1-1017/1017	===============	0/0	100.00	96.17	vfdb	NP_752608	(fepD) ferrienterobactin ABC transporter permease [Enterobactin (VF0228)] [Escherichia coli CFT073]	
```

