# The Variant Call Format (VCF)

Guardar variables con archivos de referencia

```Bash 
HREFF="/home/seminario/Escritorio/references/Homo_sapiens_assembly38_chr22.fasta"
IREFF="/home/seminario/Escritorio/references/mills_gold.b38.chr22.vcf"
SREFF="/home/seminario/Escritorio/references/1000G.snps.b38.chr22.vcf"
```

Explorar opciones de gatk y de Mutect2

ir a carpeta:  
/home/seminario/Escritorio/data/DNA/

```Bash
gatk Mutect2 --reference ${HREFF} --I TCRBOA2-T-WEX-chr22.recal.bam -tumor TUMOR -I TCRBOA2-N-WEX-chr22.recal.bam -normal NORMAL -O TCRBOA2-T-WEX-chr22.vcf.gz
```

2. Filtrar Variantes
 
```Bash
gatk FilterMutectCalls -V TCRBOA2-T-WEX-chr22.vcf.gz -O TCRBOA2-T-WEX-chr22.filtered.vcf.gz
```

3. Visualizar en igv
   1. encontrar SNP
   2. encontrar SNV
   3. encontrar deleción
   4. encontrar inserción
   5. Comprarar una variante filtrada y una variante PASS
