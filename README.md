# Tema 20: Anotación de genomas

## Estructura de la práctica:

1. Instalación de programas
2. Anotación global de un genoma
3. Identificación de genes de virulencia
4. Identificación de genes de resistencia
5. Identificación de integrones
6. Identificación de rutas metabolicas
7. Identificación de grupos de genes biosintéticos de metabolitos secundarios
8. Visualización del genoma

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

> - `AntiSMASH		https://antismash.secondarymetabolites.org/#!/start 
> - `KAAS			https://www.genome.jp/kegg/kaas/ 
> - `Proksee		https://proksee.ca/ 



