# Containerized Variant Effect Predictor (VEP) + Cache GRCh37/38

&nbsp;+ [Introduction](#Introduction) \
&nbsp;+ [Building image with Singularity](#Building-image-with-Singularity) \
&nbsp;+ [Run VEP](#Run-VEP) \
&nbsp;&nbsp;&nbsp;&nbsp;|-- [More options](#More-options) \
&nbsp;&nbsp;&nbsp;&nbsp;|-- [Examples](#Examples) \
&nbsp;+ [Filtering by VEP annotations](#Filtering-by-VEP-annotations) \
&nbsp;&nbsp;&nbsp;&nbsp;|-- [Options](#Options) \
&nbsp;&nbsp;&nbsp;&nbsp;|-- [Filtering examples](#Filtering-examples) \
&nbsp;+ [VEP plugins](#VEP-plugins) \
&nbsp;+ [Build & run VEP with Docker](#Build-&-run-VEP-with-Docker)



## Introduction
This documentation describes the usage of the Docker image at https://hub.docker.com/r/matmu/vep which contains the bioinformatics tool **Ensembl Variant effect predictor (VEP)** for annotating genetic variants. The image comes with

* Merged cache including RefSeq and Ensembl transcripts (VEP parameter --merged required)
* Reference genome and index
* Plugins (annotation data is not included)


## Building image with Singularity
```bash
singularity build vep.<version>.simg docker://matmu/vep:<version>
```

`<version>` is a tag representing the Ensembl version and the species + version of the reference genome. Examples for available versions are **99-GRCh38** (VEP v99 with cache for reference GRCh38) or **99-GRh37** (VEP v99 and cache for reference GRCh37). The version **latest** is always the most recent Ensembl version with cache for reference GRCh38. 

Visit https://hub.docker.com/r/matmu/vep/tags to get a list of all available versions.


## Run VEP
To run VEP execute
```bash
singularity exec vep.<version>.simg vep --merged [options]
```
whereby `<version>` is replaced by a respective version (see above), e.g. `99-CRCh38`. Please **always** use the VEP option `--merged` because only the merged cache including both RefSeq and Ensembl transcripts is installed in the image. 

### More options
The options for base cache/plugin directories, species and assembly are set to the right values by default and do not need to be set by the user.

Visit http://uswest.ensembl.org/info/docs/tools/vep/script/vep_options.html for detailed information about all VEP options. Detailed information about **input/output formats** can be found at https://www.ensembl.org/info/docs/tools/vep/vep_formats.html#defaultout. 

### Examples

#### Test
```bash
singularity exec vep.<version>.simg vep --merged --cache --id rs699        
```

#### Minimum (output format: compress tab)
```bash
singularity exec vep.<version>.simg vep \
        --merged \
        --cache \
        --input_file <filename>.vcf[.gz] \
        --output_file <filename>.txt.gz \
        --tab \
        --compress_output bgzip
```


#### Minimum (output format: compressed vcf)
```bash
singularity exec vep.<version>.simg vep --merged --cache --input_file <filename>.vcf[.gz] --output_file <filename>.vcf.gz --compress_output bgzip
```

#### Full annotation
```bash
singularity exec vep.<version>.simg vep --merged --cache --input_file <filename>.vcf[.gz] --output_file <filename>.vcf.gz --compress_output bgzip --everything --nearest symbol        
```


## Filtering by VEP annotations
The image also includes a VEP filtering script which can be executed by
```bash
singularity exec vep.<version>.simg filter_vep [options]
```

### Options
Visit https://www.ensembl.org/info/docs/tools/vep/script/vep_filter.html for detailed info about available options.


### Filtering examples
#### Filter for rare variants
```bash
singularity exec vep.<version>.simg filter_vep --input_file <filename>.vcf --output_file <filename>.filtered.vcf --only_matched --filter "(IMPACT is HIGH or IMPACT is MODERATE or IMPACT is LOW) and (BIOTYPE is protein_coding) and ((PolyPhen > 0.446) or (SIFT < 0.05)) and (EUR_AF < 0.001 or gnomAD_NFE_AF < 0.001 or (not EUR_AF and not gnomAD_NFE_AF))" 
```


## VEP plugins
TODO


## Build & run VEP with Docker
TODO



