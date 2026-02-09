# variant_validate
Protocols for assessing short variants (SNP/InDel) and structural variants (SV)

# 1 Short variants (SNP/InDel) validate
This is a set of programs based on htslib to benchmark variant calls against gold standard truth datasets.

## 1.1 Preparing the environment
```bash
conda create -n hap -c bioconda python=2.7.15 hap.py
```

## 1.2 Usage
To compare a VCF against a gold standard dataset, use the following commmand line to perform genotype-level haplotype comparison.
```bash
output_prefix=${out_dir}/${prefix}
cpus=30

export HGREF=${Ref_file}
conda run -n hap hap.py \
    truth.vcf \
    query.vcf \
    -f confident.bed \
    -o output_prefix \
    --engine=vcfeval \
    --threads=${cpus} \
    --pass-only
```

# 2 Structural variants (SV) validate
Truvari is a toolkit for benchmarking, merging, and annotating Structural Variants

## 2.1 Preparing the environment
```bash
conda create -n turvari_env -c bioconda python=3.9 truvari
```

## 2.2 Usage
Each sub-command contains help documentation. Start with truvari -h to see available commands.

The current most common Truvari use case is for structural variation benchmarking:
```bash
conda run -n turvari_env truvari bench \
    -b base.vcf.gz \
    -c comp.vcf.gz \
    --passonly \
    -o output_dir/ \
    -f reference.fa \
    --includebed include.bed \
    --typeignore  -r 1000 -p 0
```