## Download pipeline
```
export NXF_SINGULARITY_CACHEDIR=/cluster/tufts/biocontainers/nf-core/singularity-images
nf-core download scrnaseq -r 2.5.1 --outdir 2.5.1 -d  -s singularity -u amend -x none 
```


## Notes
### container-cache-utilisation
In nf-core, `container-cache-utilisation` refers to how the pipeline interacts with the container image cache used by Nextflow, particularly with Singularity containers. It dictates how downloads and access to container images are handled, aiming to optimize efficiency and avoid redundant downloads. Here's a breakdown of the different options:

 1. default: This is the most common setting, where nf-core automatically manages the cache. It downloads Singularity images to the designated cache directory (`$NXF_SINGULARITY_CACHEDIR`) and copies them to the workflow archive/directory upon downloading a pipeline. This ensures the necessary containers are available when running the workflow on the same system.

 2. amend: This option is primarily used when downloading a pipeline on a system with internet access, but the actual workflow execution will occur on a different system without internet access. With `--container-cache-utilisation amend`, **nf-core only downloads the container images to the cache directory but skips copying them to the workflow archive**. This saves space in the archive and allows direct utilization of the cache on the target system.

 3. remote: This option leverages an existing container image cache on a remote system to avoid unnecessary downloads. You specify the location of the remote cache directory with --container-cache-index pointing to a text file listing the available images. When downloading a pipeline, nf-core checks the remote cache before attempting any downloads. This is ideal for shared infrastructure where container images are already downloaded on a central server.

 Remember, choosing the appropriate container-cache-utilisation depends on your specific workflow and system setup. The default option works well for most cases, while amend and remote cater to scenarios with limited internet access or shared cache environments.
