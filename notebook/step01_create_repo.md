Phase 1: Project setup

Locations
- Repo (code, tracked in git): /N/scratch/schapag/validate-ngs
- Big files (not in git): /N/scratch/schapag/validate-ngs-data, linked inside the repo as data/
- Conda environment: /N/scratch/schapag/validate-ngs-data/conda/envs/validate-ngs
- Container cache: /N/scratch/schapag/validate-ngs-data/apptainer_cache
- Nextflow home: /N/scratch/schapag/validate-ngs-data/nxf_home
- Slurm account is r01340. Partitions: general (4 days), interactive (8 h), debug (1 h); GPU partitions v100 and h100 will be used for DeepVariant.

Start of every session
```
srun -p interactive -A r01340 --cpus-per-task=4 --mem=16G --time=04:00:00 --pty bash
cd /N/scratch/schapag/validate-ngs
git pull
source scripts/env.sh
```

Step 1: Repository
- Created the GitHub repo validate-ngs. It was first made in the home directory and then moved to scratch.

Step 2: Environment
- Created a new conda environment on scratch from conda-forge and bioconda, using the latest releases.
- scripts/env.sh activates the environment and points all Nextflow and Apptainer caches to scratch. It overrides older settings in ~/.bashrc.
- envs/validate-ngs.yml can recreate the environment with: conda env create -p <path> -f envs/validate-ngs.yml
- Tool versions: Nextflow 26.10.4, nf-core tools 4.2.1, nf-test 0.9.5, samtools 1.25, bcftools 1.25, bedtools 2.31.1, sra-tools 3.4.1 (all from the conda env); Apptainer 1.3.6 and Java 21.0.8 (from the HPC system).
- Pipeline tools such as BWA-MEM2, GATK, DeepVariant and fgbio are not installed with conda. They come as containers through the nf-core modules in Phase 3.
- Tested on a compute node: nextflow run nextflow-io/hello worked, and Apptainer pulled an Ubuntu image.

Next: Step 3, cluster configuration.
