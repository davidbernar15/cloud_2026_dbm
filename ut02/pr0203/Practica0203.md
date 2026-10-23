

Los precios corresponden a la región US East (N. Virginia), us-east-1, en dólares estadounidenses por GB al mes.

| Clase de almacenamiento       | Coste aprox. ($/GB/mes) | Tiempo mínimo de facturación | Tamaño mínimo facturable                  | Tiempo de recuperación (Retrieval)                                              |
| ----------------------------- | ----------------------- | ---------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------- |
| S3 Standard                   | 0,023 $                 | Ninguno                      | Ninguno                                   | Inmediato (milisegundos)                                                        |
| S3 Standard-IA                | 0,0125 $                | 30 días                      | 128 KB                                    | Inmediato (milisegundos)                                                        |
| S3 Glacier Flexible Retrieval | 0,0036 $                | 90 días                      | 40 KB de metadatos adicionales por objeto | De minutos a horas (3-5 horas en recuperación estándar)                         |
| S3 Glacier Deep Archive       | 0,00099 $               | 180 días                     | 40 KB de metadatos adicionales por objeto | Hasta 12 horas en recuperación estándar y hasta 48 horas en recuperación masiva |



### 1. Riesgo de microficheros en clases IA/Glacier

1. Si una aplicación sube 500.000 ficheros de log de 2 KB cada uno a S3 Standard-IA, la factura puede aumentar porque esta clase tiene un tamaño mínimo facturable de 128 KB por objeto, aunque el fichero real sea mucho más pequeño.

Cálculo del tamaño real:

500.000 × 2 KB = 1.000.000 KB, aproximadamente 1 GB decimal.

Cálculo del tamaño facturable:

500.000 × 128 KB = 64.000.000 KB, aproximadamente 61 GB utilizando unidades binarias.

Coste mensual aproximado:

61,04 GB × 0,0125 $ = 0,76 $ al mes.

En cambio, en S3 Standard, el almacenamiento de esos ficheros costaría aproximadamente 0,02 $ al mes.

Conclusión: aunque S3 Standard-IA tiene un precio por GB inferior, el tamaño mínimo facturable hace que almacenar muchos ficheros pequeños pueda resultar más caro. Además, pueden aplicarse cargos por solicitudes y recuperación de datos.

### 2. Borrado prematuro

2. S3 Glacier Flexible Retrieval tiene un periodo mínimo de almacenamiento de 90 días. Si un script elimina un fichero de 10 GB después de solo 15 días, AWS cobra el almacenamiento restante hasta completar el periodo mínimo.

Cálculo:

90 - 15 = 75 días adicionales.

Respuesta: AWS cobrará 75 días adicionales de almacenamiento como penalización por borrado anticipado, calculada según la cantidad de datos eliminados y la tarifa aplicable.

### 3. Cálculo de ahorro

3. Una empresa almacena 20 TB de copias de seguridad estáticas que casi nunca se consultan. Para comparar los costes, suponemos que 1 TB equivale a 1.024 GB y utilizamos un mes de 30 días.

Capacidad total:

20 × 1.024 = 20.480 GB.

Coste mensual en S3 Standard:

20.480 GB × 0,023 $ = 471,04 $ al mes.

Coste mensual en S3 Glacier Flexible Retrieval:

20.480 GB × 0,0036 $ = 73,73 $ al mes.

Ahorro mensual:

471,04 $ - 73,73 $ = 397,31 $.

Porcentaje de ahorro:

(397,31 / 471,04) × 100 = 84,34 % aproximadamente.

Conclusión: almacenar las copias de seguridad en S3 Glacier Flexible Retrieval permitiría ahorrar aproximadamente 397,31 $ al mes, es decir, un 84,34 % respecto a S3 Standard, utilizando estos precios de referencia. 

[Volver al inicio](../index.md)
