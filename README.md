# Variant effect predictor (VEP)
Containerized version of VEP. The Docker images are available on Dockerhub at https://hub.docker.com/r/matmu/vep.

## Installation using Singularity

```
singularity build vep.<version>.simg docker://matmu/vep:<version>
```

`<version>` has to be replaced by tag a representing the Ensembl version and the species + version of the reference. The latest available versions are **99-GRCh38** (VEP v99 with cache for reference GRCh38) and **99-GRh37** (VEP v99 and cache for reference GRCh37).

## Run it

To run vep in the container use

```
singularity exec <image_name> vep [options]
```
`<image_name>` has to be replaced with the corresponding Singularity container name. If you followed the installation instructions the name will be something like `vep.99-CRCh38.simg` Please **always** use the vep option `--merged` because only the cache for "merged" is included in the image. For further parameter explanation on vep and other information see http://uswest.ensembl.org/info/docs/tools/vep/script/vep_options.html.

Available apps are `vep`, `vep_vcf`, `vep_tab` and `filter_vep`. Examples for running these apps are given below.

```singularity run --app vep_vcf <input.vcf[.gz]> <outout.vcf> <image_name>```

```singularity run --app vep_tab <input.vcf[.gz]> <outout.txt> <image_name>```

```singularity run --app filter_vep <image_name>```

The parameter `<input.vcf[.gz]>` is the input file and `<outout.vcf>` is the name of the output file that will be created.