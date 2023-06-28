# proks_et_al_2023

Complenetary analysis to [nf-core/marsseq](https://github.com/nf-core/marsseq).

Dataset available at [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8016374.svg)](https://doi.org/10.5281/zenodo.8016374)

## nf-core/marsseq

```bash
module load java/11.0.15 nextflow/22.10.6 singularity/3.8.0

sh nf-core_tower.sh mm9_ref nextflow run $PIPELINE_PATH/nf-core-marsseq \
  --input /home/fdb589/projects/people/fdb589/projects/proks_et_al_2022/pipeline/SB26/design.csv \
  --build_references \
  --genomes_base /scratch/Brickman/references \
  --genome mm10

sh nf-core_tower.sh SB26 nextflow run $PIPELINE_PATH/nf-core-marsseq \
  --input /home/fdb589/projects/people/fdb589/projects/proks_et_al_2022/pipeline/SB26/design.csv \
  --genomes_base /scratch/Brickman/references \
  --genome mm10

sh nf-core_tower.sh SB28 nextflow run $PIPELINE_PATHnf-core-marsseq \
  --input /home/fdb589/projects/people/fdb589/projects/proks_et_al_2022/pipeline/SB28/design.csv \
  --genomes_base /scratch/Brickman/references \
  --genome mm10
```

## MARS-seq2.0

```bash
module load miniconda/latest

source activate ngs
cookiecutter https://github.com/brickmanlab/mars-seq2-inhouse

source activate mars
python helpers/prepare.py --input $PIPELINE_PATH/pipeline/SB26/ --output test_data

# split cells per Batch
scripts/split_fastqs.sh test_data/raw_reads/SB26/orig_files/ test_data/raw_reads/SB26/ 4000000
scripts/split_fastqs.sh test_data/raw_reads/SB28/orig_files/ test_data/raw_reads/SB28/ 4000000

# run pipeline
scripts/run_pipeline_locally.sh test_data
```
