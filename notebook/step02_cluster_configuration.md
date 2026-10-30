Step 2: Cluster configuration

- Pipeline tools are not installed here. They come as containers, pulled through the nf-core modules added in Phase 3.
- This step sets up how Nextflow submits each process as a job to the SLURM workload manager on Quartz: which account runs it, which partition, and how many CPUs/GPUs, memory and time each job gets.
- These are standard starting values. They will be tuned in Phase 3 once the test run and first full run show real time and memory use (from the Nextflow trace and report, enabled in Phase 3).

Config files
- nextflow.config: the entry point. Holds the manifest and profiles, and loads the other config files.
- conf/base.config: resources per process label and the retry rule. Generic, works on any cluster.
- conf/slurm.config: Quartz-specific settings (executor, account, partitions, GPU routing). Plays the role of an nf-core institutional profile.
- Added later in Phase 3: conf/modules.config (tool arguments, output locations) and conf/test.config (small test dataset).
- Run with: -profile slurm,apptainer

Values set
- Account r01340, default partition general.
- Label resources (nf-core defaults): single 1 CPU/6 GB/4 h, low 2/12 GB/4 h, medium 6/36 GB/8 h, high 12/72 GB/16 h, long 20 h, high_memory 200 GB.
- Ceiling for any job: 128 CPUs, 500 GB, 96 h (one Quartz general node and the 4-day limit).
- Retry rule: only jobs killed for memory or time are retried (max 2), with memory and time doubled. Any other error stops the run. No process is ever skipped.
- DeepVariant's neural-network step (call_variants) runs on h100-single with 1 GPU, time capped at 47 h (partition limit is 2 days).
- Checked with nextflow config -profile slurm,apptainer: all files load correctly.
