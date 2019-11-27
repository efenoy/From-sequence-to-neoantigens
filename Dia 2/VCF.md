# The Variant Call Format (VCF)

Guardar variables con archivos de referencia

```Bash 
HREFF="/home/seminario/Escritorio/references/Homo_sapiens_assembly38_chr22.fasta"
SREFF="/home/seminario/Escritorio/references/1000G.snps.b38.chr22.vcf"
```

Explorar opciones de gatk y de Mutect2

ir a carpeta:  
/home/seminario/Escritorio/data/DNA/

```Bash
gatk Mutect2 --reference ${HREFF} --I TCRBOA2-T-WEX-chr22.recal.bam -tumor TUMOR -I TCRBOA2-N-WEX-chr22.recal.bam -normal NORMAL -O TCRBOA2-T-WEX-chr22.vcf.gz --bam-output TCRBOA2-N-WEX-chr22.assembly.bam --dbsnp $SREFF --cosmic CosmicCodingMuts_chr22.vcf
```

2. Filtrar Variantes
 
```Bash
gatk FilterMutectCalls -V TCRBOA2-T-WEX-chr22.vcf.gz -O TCRBOA2-T-WEX-chr22.filtered.vcf.gz
```

3. Visualizar en igv los archivos bam y vcf obtenidos durante la ejecución del pipeline
   1. encontrar SNP
   2. encontrar SNV
   3. encontrar deleción
   4. encontrar inserción
   5. Comparar una variante filtrada y una variante PASS
   6. Comparar los archivos bam 
   
