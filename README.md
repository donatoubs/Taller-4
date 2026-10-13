# Taller Práctico 4: PICT + pytest (PagoYa)

**Integrantes:** Donato Oña y Guillermo Paredes

## Resumen del modelo
Modelamos la pasarela de pagos PagoYa utilizando 7 parámetros combinatorios (dispositivo, país, método, moneda, envío, cupón y monto). 
Aplicamos 6 restricciones avanzadas (R1 a R6) para asegurar la coherencia de monedas por país, restricciones geográficas de métodos como contraentrega, compatibilidad de billeteras y condiciones de cupones y montos mínimos.

## Resultados
| Medida | Valor |
|---|---|
| Combinaciones exhaustivas sin restricciones | 20,736 |
| Combinaciones válidas (/o:max) | 1,944 |
| Pruebas con t=2 | 48 |
| Pruebas con t=3 | 124 |
| Fallos antes de corregir (t=2 / t=3) | 31 |

## El error que encontramos
El error se disparaba al combinar el cupón de "Bienvenida" con el tipo de envío "Express", lo que provocaba que el sistema anulara indebidamente el descuento dejándolo en 0.00 y alterando el cálculo total. Lo descubrimos gracias a que la suite de pytest fallaba en esas combinaciones y lo corrigimos eliminando la línea condicional restrictiva dentro de la función `procesar_pago` en `pasarela.py`.

## Cómo ejecutar
    .\pict.exe checkout.pict /o:2 > checkout_t2.tsv
    .\pict.exe checkout.pict /o:3 > checkout_t3.tsv
    pytest