1) Llamar a la herramienta Mutect2 para buscar variantes

guardar variables: 
HREFF="/home/seminario/Escritorio/references/Homo_sapiens_assembly38_chr22.fasta"
IREFF="/home/seminario/Escritorio/references/mills_gold.b38.chr22.vcf"
SREFF="/home/seminario/Escritorio/references/1000G.snps.b38.chr22.vcf"

ir a carpeta:
/home/seminario/Escritorio/data/DNA/

gatk Mutect2 --reference ${HREFF} --I TCRBOA2-T-WEX-chr22.recal.bam -tumor TUMOR -I TCRBOA2-N-WEX-chr22.recal.bam -normal NORMAL -O TCRBOA2-T-WEX-chr22.vcf.gz

2) Observar en igv
	a) encontrar SNP
	b) encontrar SNV
	c) encontrar deleción
	d) encontrar inserción

3) Filtrar Variantes
 
gatk FilterMutectCalls -V TCRBOA2-T-WEX-chr22.vcf.gz --contamination-table TCRBOA2-T-WEX-chr22_calculatecontamination.table -O TCRBOA2-T-WEX-chr22.filtered.vcf.gz

4) Volver a visualizar en IGV. Comprarar archivos bam. Identificar variantes

