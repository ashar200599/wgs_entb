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



