#Convert the bam to bed
/export/apps/bedtools2_old/bin/bedtools bamtobed -i sample_markduplicates.bam | gzip > sample_markdup_coverge.bed.gz;
#Extract no. of reads from bed files
bedtools coverage -a /mnt/NGS/Human_Exome_hg19/nexterarapidcapture_exome_targetedregions_v1.2.bed -b sample_markdup_coverge.bed.gz -d | gzip > coverage_target_regions.tsv.gz;
bedtools coverage -a /mnt/NGS/Human_Exome_hg19/AgilentSureSelect_hg19.bed -b sample_markdup_coverge.bed.gz -d | gzip > coverage_target_regions.tsv.gz;
bedtools coverage -a /mnt/NGS/Human_Exome_hg19/truseq-exome-targeted-regions-manifest-v1-2.bed -b sample_markdup_coverge.bed.gz -d | gzip > coverage_target_regions.tsv.gz; 
bedtools coverage -a /mnt/NGS/Human_Exome_hg19/CReV2_Covered.bed -b sample_markdup_coverge.bed.gz -d | gzip > coverage_target_regions.tsv.gz;
#Total no. of reads 
gunzip -c sample_markdup_coverge.bed.gz | wc -l;
#No. of reads in target regions(no. of rows)
gunzip -c coverage_target_regions.tsv.gz | wc -l;
#Sum of no. reads in target regions
gunzip -c coverage_target_regions.tsv.gz | awk '{sum+=$5} END{print sum}' | tail;
#No. of reads above 20x coverage
gunzip -c coverage_target_regions.tsv.gz | awk '$5>20 {print}' | wc -l;

#Determining read length in raw fastq files
gunzip -c filename.gz | awk 'NR%4==2{print length($0)}' | gzip > outfile.gz
#No of reads with read length 150
gunzip -c ayoob-R1.gz | awk '$1>150 {print}' | wc -l;
#Read counts in fastq files
gunzip -c filename | awk 'END{print NR/4}'
# Read counts in unmapped bam
samtools view -c /mnt/Data/ikrormi/data/bedtools-related/Sandor/sample_fastq2sam.bam

#Extract the mapped reads
samtools view -b -F 4 shsu_mapped_dedup_realigned_recal.bam > mapped.bam
#Total no. of reads in mapped bam
samtools view -c mapped.bam
#Extract the unmapped reads
samtools view -f 16 shsu_mapped_dedup_realigned_recal.bam | cut -f 1 | sort | uniq | wc -l;
#NGSrich
java NGSrich evaluate -r /data/results/arh_mapped_dedup_realigned_recal.bam -u hg19 -t /export/apps/NGSrich_0.7.8/Target_regions/nexterarapidcapture_exome_targetedregions_v1.2_modified.bed -a /data/results/HumanExome/humandb_hg19/hg19_refGene.txt -o /data/results/arh_NGSrich_evaluation -p 20 -s arh --no-details

