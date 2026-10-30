# Step 1: Create the repository
Main working directory : cd /N/scratch/schapag/validate-ngs

HPC -A : r01340


Tool	
Nextflow:	26.04.6, installed in ~/.local/bin
Apptainer	1.3.6, from the system (/N/soft)
Java	21.0.8 (Nextflow needs 17 or newer,) - update
conda	available (system install 26.3.2)
nf-core 4.1.0
nf-test 0.9.5

#
Create envionment on mkdir -p /N/scratch/schapag/validate-ngs-data/conda/envs /N/scratch/schapag/validate-ngs-data/conda/pkgs  and install necessary packages
Downloaded the packages and modules required in nfcore with their versions
[Write only if needed impt packages and their versions ] 

Next we also created an environment.yml  to reproduce the exact environment
