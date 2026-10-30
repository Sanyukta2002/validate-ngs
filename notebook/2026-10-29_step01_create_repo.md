# Phase 1: Project setup 

## Locations
| What | Path |
|---|---|
| Repo (code, in git) | /N/scratch/schapag/validate-ngs |
| Big files (not in git) | /N/scratch/schapag/validate-ngs-data (linked as `data/` in repo) |
| Conda environment | /N/scratch/schapag/validate-ngs-data/conda/envs/validate-ngs |
| Container cache | /N/scratch/schapag/validate-ngs-data/apptainer_cache |
| Nextflow home | /N/scratch/schapag/validate-ngs-data/nxf_home |

Slurm account: `r01340`
Partitions: general (4 d), interactive (8 h), debug (1 h); GPU: v100, h100-* (for DeepVariant)

## Start of every session
```bash
srun -p interactive -A r01340 --cpus-per-task=4 --mem=16G --time=04:00:00 --pty bash
cd /N/scratch/schapag/validate-ngs
git pull
source scripts/env.sh
```

## Step 1: Repository
- Created repo validate-ngs; created in home, then moved to scratch

## Step 2: Environment
- New conda env on scratch, from conda-forge + bioconda (latest releases)
- `scripts/env.sh` activates the env and sends all Nextflow/Apptainer caches to scratch
  (overrides older settings in ~/.bashrc)
- `envs/validate-ngs.yml` rebuilds the env:
  `conda env create -p <path> -f envs/validate-ngs.yml`

| Tool | Version | Source |
|---|---|---|
| Nextflow | 26.10.4 | conda env |
| nf-core tools | 4.2.1 | conda env |
| nf-test | 0.9.5 | conda env |
| samtools / bcftools | 1.25 | conda env |
| bedtools | 2.31.1 | conda env |
| sra-tools | 3.4.1 | conda env |
| Apptainer | 1.3.6 | system |
| Java | 21.0.8 | system |

- Pipeline tools (BWA-MEM2, GATK, DeepVariant, fgbio, etc.) are not installed with conda;
  they come as containers per nf-core module (Phase 3)
- Tested on compute node: `nextflow run nextflow-io/hello` worked; Apptainer pulled an Ubuntu image

## Cluster Config

