# WHOLE GENOME SEQUENCING (WGS) of _Enterobacter cloacae_
WGS pipeline (Quality Check, Genome Mapping, Variant Calling, and Variant Annotation) of _Enterobacter cloacae_

---

## 🧬 Biological Question

> Are there variants in β-lactamase genes?

| | |
|---|---|
| **Dataset** | SRR29468201 —  _Enterobacter cloacae_ from wastewater sources in Pakistan|
| **Genome Reference** | GCF_905331265.2 |
| **Key finding** | blaCMH as the chromosomal β-lactamase is present |


---

## Results

### SNP Effect by Region Barplot
![Barplot](https://github.com/ashar200599/wgs_entb/blob/abc34dff6dd48c239ec640cb887e4fdba7d945db/wgs/plot/effect_regions.png)

### SNP Effect by Type Barplot
![Barplot](https://github.com/ashar200599/wgs_entb/blob/abc34dff6dd48c239ec640cb887e4fdba7d945db/wgs/plot/effect_types.png)

### Manhattan Plot
![Manhattan Plot](https://github.com/ashar200599/wgs_entb/blob/abc34dff6dd48c239ec640cb887e4fdba7d945db/wgs/plot/manhattan_plot.png)

### Pie Chart
![Pie Chart](https://github.com/ashar200599/wgs_entb/blob/abc34dff6dd48c239ec640cb887e4fdba7d945db/wgs/plot/pie_charts.png)

---

## 📁 Repository Structure

```
.
├── wgs
│   ├── freebayes
│   ├── ngi_visualizations
│   ├── plot
│   │   ├── effect_regions.png
│   │   ├── effect_types.png
│   │   ├── manhattan_plot.png
│   │   └── pie_charts.png
│   ├── reference_data
│   │   └── GCF_905331265.2_AI2999v1_cpp_genomic.fna.gz
│   ├── results
│   │   ├── bcftools
│   │   │   ├── variants_filtered.vcf
│   │   │   ├── variants_norm.vcf
│   │   │   └── variants_norm_renamed.vcf
│   │   ├── fastp
│   │   │   ├── fastp_report.html
│   │   │   ├── fastp_report.json
│   │   │   ├── sample_clean_1.fastq
│   │   │   └── sample_clean_2.fastq
│   │   ├── fastqc
│   │   │   ├── multiqc_clean_report_data
│   │   │   │   ├── fastqc-status-check-heatmap.txt
│   │   │   │   ├── fastqc_adapter_content_plot.txt
│   │   │   │   ├── fastqc_per_base_n_content_plot.txt
│   │   │   │   ├── fastqc_per_base_sequence_quality_plot.txt
│   │   │   │   ├── fastqc_per_sequence_gc_content_plot_Counts.txt
│   │   │   │   ├── fastqc_per_sequence_gc_content_plot_Percentages.txt
│   │   │   │   ├── fastqc_per_sequence_quality_scores_plot.txt
│   │   │   │   ├── fastqc_sequence_counts_plot.txt
│   │   │   │   ├── fastqc_sequence_duplication_levels_plot.txt
│   │   │   │   ├── fastqc_sequence_length_distribution_plot.txt
│   │   │   │   ├── llms-full.txt
│   │   │   │   ├── multiqc.log
│   │   │   │   ├── multiqc.parquet
│   │   │   │   ├── multiqc_citations.txt
│   │   │   │   ├── multiqc_data.json
│   │   │   │   ├── multiqc_fastqc.txt
│   │   │   │   ├── multiqc_general_stats.txt
│   │   │   │   ├── multiqc_software_versions.txt
│   │   │   │   └── multiqc_sources.txt
│   │   │   ├── multiqc_data
│   │   │   │   ├── fastqc-status-check-heatmap.txt
│   │   │   │   ├── fastqc_adapter_content_plot.txt
│   │   │   │   ├── fastqc_per_base_n_content_plot.txt
│   │   │   │   ├── fastqc_per_base_sequence_quality_plot.txt
│   │   │   │   ├── fastqc_per_sequence_gc_content_plot_Counts.txt
│   │   │   │   ├── fastqc_per_sequence_gc_content_plot_Percentages.txt
│   │   │   │   ├── fastqc_per_sequence_quality_scores_plot.txt
│   │   │   │   ├── fastqc_sequence_counts_plot.txt
│   │   │   │   ├── fastqc_sequence_duplication_levels_plot.txt
│   │   │   │   ├── fastqc_sequence_length_distribution_plot.txt
│   │   │   │   ├── llms-full.txt
│   │   │   │   ├── multiqc.log
│   │   │   │   ├── multiqc.parquet
│   │   │   │   ├── multiqc_citations.txt
│   │   │   │   ├── multiqc_data.json
│   │   │   │   ├── multiqc_fastqc.txt
│   │   │   │   ├── multiqc_general_stats.txt
│   │   │   │   ├── multiqc_software_versions.txt
│   │   │   │   └── multiqc_sources.txt
│   │   │   ├── SRR29468201_1_fastqc.html
│   │   │   ├── SRR29468201_1_fastqc.zip
│   │   │   ├── SRR29468201_2_fastqc.html
│   │   │   ├── SRR29468201_2_fastqc.zip
│   │   │   ├── multiqc_clean_report.html
│   │   │   ├── multiqc_report.html
│   │   │   ├── sample_clean_1_fastqc.html
│   │   │   ├── sample_clean_1_fastqc.zip
│   │   │   ├── sample_clean_2_fastqc.html
│   │   │   └── sample_clean_2_fastqc.zip
│   │   ├── freebayes
│   │   │   └── variants_raw.vcf
│   │   ├── samtools
│   │   │   ├── sorted.bam
│   │   │   └── sorted.bam.bai
│   │   └── snpEff
│   │       ├── snpEff_summary.csv
│   │       ├── snpEff_summary.genes.txt
│   │       ├── snpEff_summary.html
│   │       └── variants_annotated.vcf
│   ├── scripts
│   │   ├── .RData
│   │   ├── .RDataTmp
│   │   ├── .Rhistory
│   │   ├── script.md
│   │   └── vcfR_plot.Rmd
│   └── snpEff
│       ├── data
│       │   └── enterobacter_cloacae
│       │       ├── genes.gff
│       │       ├── sequence.NZ_OW968328.1.bin
│       │       ├── sequences.fa
│       │       └── snpEffectPredictor.bin
│       ├── examples
│       │   ├── 1kg.head_chr1.filtered.vcf.gz
│       │   ├── 1kg.head_chr1.vcf.gz
│       │   ├── cancer.ann.vcf
│       │   ├── cancer.eff.vcf
│       │   ├── cancer.vcf
│       │   ├── cancer_pedigree.ann.vcf
│       │   ├── cancer_pedigree.vcf
│       │   ├── example_motif.vcf
│       │   ├── examples.sh
│       │   ├── file.vcf
│       │   ├── intervals.bed
│       │   ├── my_annotations.bed
│       │   ├── samples_cancer.txt
│       │   ├── samples_cancer_one.txt
│       │   ├── test.1KG.ann_encode.vcf
│       │   ├── test.1KG.ann_reg.vcf
│       │   ├── test.1KG.vcf
│       │   ├── test.ann.vcf
│       │   ├── test.chr22.ann.filter_missense.vcf
│       │   ├── test.chr22.ann.filter_missense_any.vcf
│       │   ├── test.chr22.ann.filter_missense_any_TRMT2A.vcf
│       │   ├── test.chr22.ann.filter_missense_first.vcf
│       │   ├── test.chr22.ann.one_per_line.txt
│       │   ├── test.chr22.ann.txt
│       │   ├── test.chr22.ann.vcf
│       │   ├── test.chr22.vcf
│       │   ├── test.vcf
│       │   ├── variants_1.ann.vcf
│       │   ├── variants_1.vcf
│       │   ├── variants_2.ann.vcf
│       │   └── variants_2.vcf
│       ├── galaxy
│       │   ├── tool-data
│       │   │   ├── snpEff_genomes.loc
│       │   │   └── snpEff_genomes.loc.sample
│       │   ├── snpEff.xml
│       │   ├── snpEffWrapper.pl
│       │   ├── snpEff_download.xml
│       │   ├── snpSiftWrapper.pl
│       │   ├── snpSift_annotate.xml
│       │   ├── snpSift_caseControl.xml
│       │   ├── snpSift_filter.xml
│       │   ├── snpSift_int.xml
│       │   ├── tool_conf.xml
│       │   └── tool_dependencies.xml
│       ├── scripts
│       │   ├── gsa
│       │   │   ├── bayesFactor_correction_scoreCount.r
│       │   │   ├── bayesFactor_correction_scoreCount.sh
│       │   │   ├── bayesFactor_correction_scoreCount_max10.sh
│       │   │   ├── checkGeneNames.py
│       │   │   ├── create_sets.bds
│       │   │   ├── geneSetOverlap.py
│       │   │   ├── geneSetOverlap.sort.txt
│       │   │   ├── geneSetsGtex.py
│       │   │   ├── pvalue_correction_scoreCount.r
│       │   │   ├── pvalue_correction_scoreCount.sh
│       │   │   └── pvalue_correction_scoreCount_min10.sh
│       │   ├── 1kg.sh
│       │   ├── annotate_demo.sh
│       │   ├── annotate_demo_GATK.sh
│       │   ├── bedEffOnePerLine.pl
│       │   ├── buildDbNcbi.sh
│       │   ├── cgShore.pl
│       │   ├── cgShore.sh
│       │   ├── countColumns.py
│       │   ├── db.pl
│       │   ├── extractSequences.pl
│       │   ├── fasta2tab.pl
│       │   ├── fastaSample.pl
│       │   ├── fastaSplit.pl
│       │   ├── fastqSplit.pl
│       │   ├── filterBy.py
│       │   ├── gffRemovePhase.pl
│       │   ├── isutf8.py
│       │   ├── join.pl
│       │   ├── joinSnpEff.pl
│       │   ├── make_dbNSFP.sh
│       │   ├── nextProt_filter.pl
│       │   ├── ped2vcf.py
│       │   ├── plot.pl
│       │   ├── plotHistogram.pl
│       │   ├── plotLabel.pl
│       │   ├── plotMA.pl
│       │   ├── plotQQ.pl
│       │   ├── plotQQsubsample.pl
│       │   ├── plotSmoothScatter.pl
│       │   ├── plotXY.pl
│       │   ├── queue.pl
│       │   ├── sam2fastq.pl
│       │   ├── snpEff
│       │   ├── snpSift_filter_sample_to_number.pl
│       │   ├── sortLine.py
│       │   ├── splitChr.pl
│       │   ├── statsNum.pl
│       │   ├── swapCols.pl
│       │   ├── transpose.pl
│       │   ├── txt2fa.pl
│       │   ├── txt2vcf.py
│       │   ├── uniqCount.pl
│       │   ├── uniqCut.pl
│       │   ├── vcfAnnFirst.py
│       │   ├── vcfBareBones.pl
│       │   ├── vcfEffHighest.ORI.py
│       │   ├── vcfEffOnePerLine.pl
│       │   ├── vcfFilterSamples.pl
│       │   ├── vcfInfoOnePerLine.pl
│       │   ├── vcfOnlyAlts.pl
│       │   ├── vcfReduceGenotypes.pl
│       │   ├── vcfRefCorrect.py
│       │   └── wigSplit.pl
│       ├── SnpSift.jar
│       ├── snpEff.config
│       ├── snpEff.jar
│       └── variants_norm.vcf
├── .gitattributes
├── .gitignore
├── README.md
└── tree_output.txt

```





---
## Methods
| Step | Tool | Details |
|---|---|---|
|Data Download| SRA Toolkit | SRR29468201 |
|SRA to FASTQ conversion |fastq-dump | splitting files into SRR29468201_1.fastq SRR29468201_2.fastq |
|Quality Control| FastQC and MultiQC | check FASTQ quality
|Adapter Trimming | FastP | clean th adapters |
|Genome Mapping| bwa | mapping reads into GCF_905331265.2 genome
|Convert SAM to BAM | samtools | convert .sam output into .bam format
|Variant Calling | freebayes | check variants
|Variant Annotation | snpEff | annotate variant using snpEff custom database
|VCF Plot | ggplot | Barplot, Manhattan plot, Pie chart


---

## 📈 Key Results

| Findings | Details | Biological Meaning |
|---|---|---|
| Downstream & Upstream gene regions| ~200,000 and ~175,000 genes | Most genetic variation in this E. cloacae strain is in regulatory/flanking regions, which could affect gene expression rather than protein structure|
| Variant Quality | relatively uniform across the ~5 Mb chromosome |  indicating even sequencing coverage|
| Silent/Synonymous variants| 84.72% |  these mutations don't change amino acid sequence, suggesting strong purifying selection maintaining protein function|
| Missense variants | 15.22% | these alter amino acid identity and are candidates for functional impact
| Modifier impact | 91.16% | variants in non-coding or regulatory regions with indirect/unknown effects
| Variant rate | 	1 variant every 120 bases | Mtb sample is genetically close to the referenc

**Conclusion:** The variant landscape is consistent with a clinically adapted or environmentally stable strain.

---

## 👤 Author

**Ashar Kurnia** 



