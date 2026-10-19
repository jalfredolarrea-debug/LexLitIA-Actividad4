# LexLitIA | Actividad 4

## Descripcion

LexLitIA es un prototipo academico de clasificacion
de extractos sinteticos de demandas bancarias en Mexico.

Su objetivo es comparar tres modelos preentrenados
de Hugging Face mediante clasificacion zero-shot.

## Categorias

1. Tarjeta de Debito.
2. Tarjeta de Credito.
3. Cheques.
4. Canales Digitales.
5. Otros.

La clasificacion se determina por el producto
o servicio directamente controvertido.

Los pagos fisicos o contactless en TPV se asignan
a la categoria correspondiente a la tarjeta.

Las transferencias mediante banca movil o internet
se clasifican como Canales Digitales.

## Dataset

Se utilizaron 50 extractos juridicos sinteticos:

- 25 registros de desarrollo.
- 25 registros de evaluacion.
- Cinco categorias equilibradas.
- Cinco casos de evaluacion por categoria.

No se utilizaron expedientes reales ni informacion
confidencial de clientes bancarios.

## Modelos evaluados

- MoritzLaurer/mDeBERTa-v3-base-mnli-xnli
- joeddav/xlm-roberta-large-xnli
- facebook/bart-large-mnli

Los tres modelos fueron consultados en Hugging Face
y cuentan con licencia MIT.

## Metodologia

Se utilizo Google Colab con GPU Tesla T4.

La evaluacion zero-shot se realizo sin fine-tuning.

Los tres modelos procesaron los mismos 25 extractos
con las mismas cinco etiquetas descriptivas.

Se calcularon accuracy, precision macro, recall macro,
F1 macro y latencia de inferencia.

## Resultados

| Modelo | Accuracy | Precision macro | Recall macro | F1 macro | Latencia media (s) |
| --- | --- | --- | --- | --- | --- |
| mDeBERTa | 0.6400 | 0.7048 | 0.6400 | 0.6000 | 0.1295 |
| XLM-RoBERTa | 0.7200 | 0.6167 | 0.7200 | 0.6395 | 0.1284 |
| BART | 0.6800 | 0.7754 | 0.6800 | 0.6540 | 0.2113 |

## Matriz de decision

Los criterios y ponderaciones fueron:

- Accuracy: 30%.
- F1 macro: 30%.
- Recall de Otros: 20%.
- Latencia: 15%.
- Numero de parametros: 5%.

| Modelo | Puntaje sobre 100 |
| --- | --- |
| mDeBERTa | 61.07 |
| XLM-RoBERTa | 58.27 |
| BART | 56.56 |

El candidato experimental preferente fue
**mDeBERTa**, conforme a las ponderaciones
definidas para este ejercicio.

## Riesgos y limitaciones

Ningun modelo supero los umbrales exploratorios
de 80% de accuracy y 60% de recall en Otros.

La categoria Otros presento dificultades
significativas de clasificacion.

El conjunto de evaluacion contiene solamente
25 extractos sinteticos, por lo que los resultados
no acreditan desempeno sobre demandas reales.

No se recomienda el despliegue operativo sin
ampliar la evaluacion y establecer controles
de revision juridica humana.

## Reproduccion

1. Abrir el notebook en Google Colab.
2. Activar GPU T4.
3. Ejecutar las etapas en orden.
4. Instalar las dependencias indicadas.
5. Cargar lexlitia_dataset.csv cuando se solicite.
6. Ejecutar inferencia y revisar las metricas.
7. Consultar las evidencias en results/.

La version de PyTorch observada fue:
2.11.0+cu130.

## Estructura del repositorio

- notebooks/: notebook reproducible.
- data/: dataset y particiones.
- results/: metricas, predicciones y figuras.
- docs/: manifiestos de integridad.
- requirements.txt: dependencias.

## Seguridad

No publicar tokens, contrasenas, credenciales
ni datos personales o bancarios confidenciales.

Este prototipo tiene exclusivamente fines
academicos y experimentales.
