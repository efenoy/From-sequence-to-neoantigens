# MuPeXI

Dada una lista de mutaciones somáticas (archivo VCF) como entrada, MuPeXI devuelve una tabla que contiene todos los péptidos mutados (neopéptidos) de longitudes definidas por el usuario, junto con datos relevantes para priorizar posibles neoepítopes.

Ejecutaremos la herramienta desde el [servidor](http://www.cbs.dtu.dk/services/MuPeXI/). Para ejecutar por consola es posible descargar MuPeXI desde https://github.com/ambj/MuPeXI

Utilizar los archivos de ejemplo, los HLAs **HLA-A01:01,HLA-B08:01** y longitud de péptidos de **8-11**

Analizar los primeros 8 candidatos:

1. ¿De cuántas mutaciones distintas provienen los péptidos candidatos?
2. Filtrar por posición genómica y evaluar los candidatos que provienen de la misma mutación. ¿Cuál es el mejor candidato y por qué?
3. Evaluar promiscuidad de unión a alelos HLA buscando los valores reportados de afinidad de los péptidos para el resto de los alelos HLA
4. A partir de los [logos de afinidad a los alelos HLA](http://www.cbs.dtu.dk/services/NetMHCpan/logos_ps.php) explicar la diferencia en los valores de afinidad para los péptidos normal y mutado.
