# Variant effect predictor (VEP)
This documentation describes the usage of Docker images containing tool Ensembl Variant effect predictor (VEP) for annotating genetic variants in conjunction with

* Merged cache including RefSeq and Ensembl transcripts (VEP parameter --merged required)
* Reference genome and index
* Plugins (annotation data is not included)

The images are available on Dockerhub at https://hub.docker.com/r/matmu/vep.


## Building imge using Singularity
```
singularity build vep.<version>.simg docker://matmu/vep:<version>
```

`<version>` is a tab representing the Ensembl version and the species + version of the reference genome. Examples for available versions are **99-GRCh38** (VEP v99 with cache for reference GRCh38) or **99-GRh37** (VEP v99 and cache for reference GRCh37). The version **latest** is always the most recent Ensembl version with cache for reference GRCh38. 

Visit https://hub.docker.com/r/matmu/vep/tags to get a list of all available versions.


## Run
To run VEP execute
```
singularity exec vep.<version>.simg vep [options]
```
whereby `<version>` is replaced by a respective version (see above), e.g. `99-CRCh38`. Please **always** use the VEP option `--merged` because only the cache for "merged" is included in the image. 


## VEP parameters
For further parameter explanation on vep and other information see http://uswest.ensembl.org/info/docs/tools/vep/script/vep_options.html.

Available apps are `vep`, `vep_vcf`, `vep_tab` and `filter_vep`. Examples for running these apps are given below.


## Filtering by VEP annotations
The image also includes a VEP filtering script which can be executed by
```
singularity exec vep.<version>.simg [options]
```


## Examples

### 



```singularity run --app vep_vcf <input.vcf[.gz]> <outout.vcf> <image_name>```

```singularity run --app vep_tab <input.vcf[.gz]> <outout.txt> <image_name>```

```singularity run --app filter_vep <image_name>```

The parameter `<input.vcf[.gz]>` is the input file and `<outout.vcf>` is the name of the output file that will be created.
