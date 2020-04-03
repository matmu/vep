# Variant effect predictor (VEP)
This documentation describes the usage of Docker images at https://hub.docker.com/r/matmu/vep containing Ensembl Variant effect predictor (VEP) for annotating genetic variants. The image comes with

* Merged cache including RefSeq and Ensembl transcripts (VEP parameter --merged required)
* Reference genome and index
* Plugins (annotation data is not included)


## Building image using Singularity
```bash
singularity build vep.<version>.simg docker://matmu/vep:<version>
```

`<version>` is a tab representing the Ensembl version and the species + version of the reference genome. Examples for available versions are **99-GRCh38** (VEP v99 with cache for reference GRCh38) or **99-GRh37** (VEP v99 and cache for reference GRCh37). The version **latest** is always the most recent Ensembl version with cache for reference GRCh38. 

Visit https://hub.docker.com/r/matmu/vep/tags to get a list of all available versions.


## Run VEP from Singularity image
To run VEP execute
```bash
singularity exec vep.<version>.simg vep [options]
```
whereby `<version>` is replaced by a respective version (see above), e.g. `99-CRCh38`. Please **always** use the VEP option `--merged` because only the cache for "merged" is included in the image. 


### Options
For further option explanations on VEP visit http://uswest.ensembl.org/info/docs/tools/vep/script/vep_options.html. The options for base cache/plugin directories, species and assembly are set to the right values by default.

### Examples

#### Test
```bash
singularity exec vep.<version>.simg vep --merged --cache --id rs699        
```

#### Minimum with compressed tab as output format
```bash
singularity exec vep.<version>.simg vep \
        --merged \
        --cache \
        --input_file <filename>.vcf[.gz] \
        --output_file <filename>.txt.gz \
        --tab \
        --compress_output bgzip
```


#### Minimum with compressed VCF as output format
```bash
singularity exec vep.<version>.simg vep \
        --merged \
        --cache \
        --input_file <filename>.vcf[.gz] \
        --output_file <filename>.vcf.gz \
        --compress_output bgzip
```

#### Full
```bash
singularity exec vep.<version>.simg vep \
        --input_file <input_vcf> \
        --output_file <output_vcf> \
        --check_ref \
        --tab \
        --merged \
        --cache \
        --offline \
        --verbose \
        --force_overwrite \
        --sift b \
        --polyphen b \
        --ccds \
        --uniprot \
        --hgvs \
        --symbol \
        --numbers \
        --domains \
        --regulatory \
        --canonical \
        --protein \
        --biotype \
        --uniprot \
        --tsl \
        --appris \
        --gene_phenotype \
        --af \
        --af_1kg \
        --af_esp \
        --af_gnomad \
        --max_af \
        --pubmed \
        --variant_class \
        --total_length \
        --check_existing \
        --total_length \
        --nearest symbol
```


## Filtering by VEP annotations
The image also includes a VEP filtering script which can be executed by
```bash
singularity exec vep.<version>.simg filter_vep [options]
```

### Options

### Examples
```bash
singularity exec vep.<version>.simg filter_vep
```
