# Tema 20: Anotación de genomas

## Estructura de la práctica:

1. Instalación de programas
2. Anotación global de un genoma
3. Identificación de genes de virulencia
4. Identificación de genes de resistencia
5. Identificación de integrones
6. Anotación de rutas metabolicas
7. Anotaci
8. Identificación de SNPs

## Metodología:

## 1. Instalación de programas

### Instalar los siguientes programas en un ambiente de conda

```bash
conda create -n annotation_01 -c bioconda prokka abricate integron_finder mgcplotter

conda create -n annotation_02 -c bioconda rgi

```
> **Comentario:** 
> - `conda create`: Este es el comando base para crear un nuevo entorno Conda.
> - `-n assembly`: Esta opción especifica el nombre del nuevo entorno como "assembly". Los entornos virtuales son como carpetas aisladas donde puedes instalar diferentes versiones de software sin que interfieran con otras instalaciones.
> - `-c bioconda`: Esta opción indica que se debe buscar los paquetes en el canal "bioconda".
> - `unicycler`: Un ensamblador de genomas híbrido que combina lecturas de corta y larga longitud.
> - `flye`: Un ensamblador de genomas para lecturas de larga longitud.
> - `quast`: Una herramienta para evaluar la calidad de los ensamblajes de genomas.
> - `checkm-genome`: Una herramienta para evaluar la integridad y contaminación de los ensamblajes de genomas.
> - `racon`: Una herramien
