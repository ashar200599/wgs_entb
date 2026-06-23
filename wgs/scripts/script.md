# Chapter 1 : Make a directory

**1. Make root folder**

```bash
mkdir wgs
cd wgs
```

**2. Make sub-folder**

```bash
mkdir raw_data reference_data scripts results
mkdir -p results/fastqc
mkdir -p results/fastp
mkdir -p results/bwa
mkdir -p results/samtools
mkdir -p results/freebayes
mkdir -p results/bcftools
```

# Chapter 2: Conda Setup (Windows)

## A.Installing Conda

**1. Download Conda installer**

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

**2. Run the installer**

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

**3. Waking Up Conda**

```bash
source ~/.bashrc
conda --version
```

**4. Create a conda environment**

```bash
conda create -n wgs python=3.9 -y
conda activate wgs
```

## B. Setting up Bioconda

```bash
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

## C. WGS Tools installation

```bash
conda install -y sra-tools fastqc multiqc fastp bwa samtools freebayes snpeff bcftools

prefetch --version
fastq-dump --version
fastqc --version
multiqc --version
fastp --version
bwa --version
samtools --version
freebayes --version
snpeff --version
bcftools --version
```

**Notes:**

If installing freebayes error try this

```bash
sudo apt update
sudo apt update && sudo apt install -y pkg-config liblzma-dev cmake
```

```bash
git clone --recursive https://github.com/freebayes/freebayes.git
cd freebayes
meson setup build
cd build
meson compile
freebayes --version
```

If installing snpeff error try this

1. Check Java version

```bash
java --version
```

2.If jave version less than ver.21, update java

```bash
sudo apt update
sudo apt install openjdk-21-jdk
```

3. Download and install snpeff

```bash
wget https://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip
unzip snpEff_latest_core.zip
cd snpEff
java -jar snpEff.jar --version
```

# Chapter 3: Data download

**1. Download SRA data**

```bash
cd raw_data
prefetch SRR29468201
```

**2. SRA to FASTQ conversion**

```bash
fastq-dump --split-files SRR29468201.sra

```

# Chapter 4: Quality control

**1. FastQC**

```bash
fastqc SRR29468201_1.fastq SRR29468201_2.fastq -o ../results/fastqc/
```

**2. Check fastqc result**

```bash
cd ../results/fastqc
multiqc .
explorer.exe multiqc_report.html

```

**3. Adapter trimming**

```bash
fastp -i SRR29468201_1.fastq -I SRR29468201_2.fastq -o ../results/fastp/sample_clean_1.fastq -O ../results/fastp/sample_clean_2.fastq --detect_adapter_for_pe --html ../results/fastp/fastp_report.html --json ../results/fastp/fastp_report.json

```

**4.Check fastp result**

```bash
cd ../results/fastp
explorer.exe fastp_report.html
```

**5. Check the quality after trimming**

```bash
fastqc sample_clean_1.fastq sample_clean_2.fastq -o ../fastqc/
multiqc ../fastqc/ -o ../fastqc/ -n multiqc_clean_report
explorer.exe multiqc_clean_report.html

```

# Chapter 5 : Genome Mapping

**1. Reference genome download**

```bash
cd ../../reference_data
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/905/331/265/GCF_905331265.2_AI2999v1_cpp/GCF_905331265.2_AI2999v1_cpp_genomic.fna.gz
```

**2.Unzip reference genome**

```bash
 gunzip GCF_905331265.2_AI2999v1_cpp_genomic.fna.gz

```

**3.Rename reference genome**

```bash
mv GCF_905331265.2_AI2999v1_cpp_genomic.fna ent_reference.fna

```

**4. Index reference genome**

```bash
bwa index ent_reference.fna

```

**5.Mapping Reads into reference genome**

```bash
cp ../results/fastp/sample_clean_1.fastq .
cp ../results/fastp/sample_clean_2.fastq .
bwa mem ent_reference.fna sample_clean_1.fastq sample_clean_2.fastq -o ../results/bwa/alignment.sam

```

# Chapter 6 : Convert and Short Data

**1. Convert SAM to BAM**

```bash
cd ../results/bwa
samtools view -bS alignment.sam -o ../samtools/alignment.bam
cd ../samtools
samtools sort alignment.bam -o ../samtools/sorted.bam
samtools index sorted.bam
```

**2. Using samtools for advanced analysis**

```bash
samtools flagstat sorted.bam        # see basic statistic
samtools coverage sorted.bam                    # see coverage
samtools depth sorted.bam  |  head -n 10         # see depth

```

**3.Check bam file**

```bash
samtools quickcheck sorted.bam && echo "OK"
```

**4.Delete alignment.sam and alignment.bam for save storage**

```bash
rm alignment.bam
cd ../bwa
rm alignment.sam
```

# Chapter 7: Variant calling

**1. Copy sorted.bam and reference.fna to the freebayes directory**

```bash
cp ../results/samtools/sorted.bam .
cp ../reference_data/ent_reference.fna .

```

**2. Run freebayes**

```bash
cd ../../freebayes
freebayes -f ent_reference.fna --min-mapping-quality 20 --min-base-quality 20 --min-coverage 10 sorted.bam > ../results/freebayes/variants_raw.vcf

```

**3. Check variant count**

```bash
cd ../results/freebayes
bcftools view -H variants_raw.vcf | wc -l

```

**4. Filter VCF file with BCF tools**

```bash
bcftools filter -e 'QUAL<30 || INFO/DP<10 || AF < 0.1' variants_raw.vcf -o ../bcftools/variants_filtered.vcf
```

**5.Check variant count**

```bash
cd ../bcftools
bcftools view -H variants_filtered.vcf | wc -l
```

**6. VCF Normalization**

```bash
cp ../../reference_data/ent_reference.fna .
bcftools norm -f ent_reference.fna -m- variants_filtered.vcf -o variants_norm.vcf
```

**7. Check variant count**

```bash

bcftools view -H variants_norm.vcf | wc -l
```

# Chapter 8: Variant Annotation

## Build annoation database

**1. Make snpEff directory**

```bash
cd ../snpEff
echo "# Enterobacter_cloacae custom database" >> snpEff.config  # Add new reference
echo "ent_sequences.fa.genome : Enterobacter_cloacae" >> snpEff.config
mkdir -p data/enterobacter_cloacae
```

**2.Add reference genome**

```bash
cp ../../reference_data/ent_reference.fna .
mv ent_reference.fna ent_sequences.fa
```

```bash
snpEff build -c snpEff.config -gff3 -v -noCheckCds -noCheckProtein enterobacter_cloacae

```

## Variant Annotation

**1. Variant Annotation**

```bash
grep -v "^#" variants_norm.vcf | cut -f1 | sort -u          #check CHROM
# sed 's/ID/Chromosome/g' variants_norm.vcf > variants_norm_renamed.vcf   #rename CHROM (optinal)

```

**2. Run snpEff**

```bash
cd ../../snpEff
cp ../results/bcftools/variants_norm.vcf .
snpEff -c snpEff.config -v  -stats ../results/snpEff/snpEff_summary.html -csvStats ../results/snpEff/snpEff_summary.csv Enterobacter_cloacae variants_norm.vcf > ../results/snpEff/variants_annotated.vcf
```

**3. Check results**

```bash
cd ../snpEff
explorer.exe snpeff_summary.html
```

**4. Data exploration**

```bash
grep -v "^#" variants_annotated.vcf | wc -l     #Count variants
grep -v "^#" variants_annotated.vcf | awk '{print $1}' | sort | uniq -c | sort -rn #Count variants per CHROM/contig
```

```bash
grep -v "^#" variants_annotated.vcf | cut -f10 | cut -d: -f1 | sort | uniq -c  #Check homozygote or heterzogote variants
```

5. Visualization

```bash
git clone https://github.com/ewels/ngi_visualizations.git
```

```bash
conda install -y setuptools matplotlib numpy #install dependencies
cd ngi_visualizations
python setup.py install

```

If error

```bash
pip install 2to3
2to3 -w ngi_visualizations/
pip install .
```

```bash
python ngi_visualizations/snpEff/snpEff_plots.py ../results/snpEff/snpEff_summary.csv #MAke plot

```

If error

```bash
sed -i 's/\.itervalues()/.values()/g; s/\.iteritems()/.items()/g; s/\.iterkeys()/.keys()/g' \
  /mnt/e/wgs_entb/wgs/ngi_visualizations/ngi_visualizations/snpEff/snpEff_plots.py
```

=
