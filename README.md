# Clasificación Multiclase de Razas de Perro (25 clases)

Proyecto de vision artificial que resuelve un problema de multiclase: determinar la raza de un perro a partir de su imagen, usando el Oxford-IIIT Pet Dataset.

## Descripción del problema

El dataset original contiene 37 clases (25 razas de perro y 12 de gato). En esta variante se descarta la especie gato y el problema queda restringido a:

- Una sola clase de especie: perro (`Dog`)
- 25 clases de raza: `american_bulldog`, `beagle`, `chihuahua`, `pomeranian`, `yorkshire_terrier`, etc.
- Métrica de referencia: *accuracy* Top-1 (raza exacta) y Top-5 (la raza verdadera entre las 5 predicciones más probables)

El dataset contiene 4.990 imágenes de perros, particionadas en 70% entrenamiento / 15% validación / 15% prueba, con estratificación por raza.

## Estructura del proyecto

| Archivo | Descripción |
| --- | --- |
| `CNN Clasificacion multicase solo Razas de Perros Modo Informe.ipynb` | **Informe final (CNN)**. Arquitectura convolucional basica. |
| `MLP Clasificacion multicase solo Razas de Perros Modo Informe.ipynb` | **Informe final (MLP)**. Perceptrón multicapa de basica. |

## Arquitectura CNN utilizada

```
Entrada (64, 64, 3)
Conv2D(32, 3x3, relu, padding='same')  ->  (64, 64, 32)      896 params
MaxPooling2D(2x2)                     ->  (32, 32, 32)
Conv2D(64, 3x3, relu, padding='same')  ->  (32, 32, 64)  18.496 params
MaxPooling2D(2x2)                     ->  (16, 16, 64)
Flatten                                ->  16.384
Dense(256, relu)                       ->  (256)     4.194.560 params
Dense(25, softmax)                     ->  (25)          6.425 params
```

- **Pérdida:** `sparse_categorical_crossentropy` (etiquetas enteras del `LabelEncoder`)
- **Optimizador:** Adam con `learning_rate=1e-4`
- **Entrenamiento:** 10 épocas, `batch_size=32`
- **Total:** 4.220.377 parámetros entrenables

## Esquema del informe

Ambos informes finales siguen la misma estructura:

1. Introducción
2. Comprensión y exploración del conjunto de datos
3. Preparación y preprocesamiento de los datos
4. Diseño del modelo
5. Entrenamiento del modelo
6. Evaluación del desempeño multiclase
7. Análisis de resultados y errores
8. Discusión de limitaciones y conclusiones

## Requisitos y ejecución

Los notebooks están pensados para ejecutarse directamente en **Google Colab**.

```bash
pip install kagglehub tensorflow pandas numpy scikit-learn matplotlib seaborn pillow
```

El dataset se descarga automáticamente desde Kaggle en la primera celda de código:

```python
import kagglehub
path = kagglehub.dataset_download("tanlikesmath/the-oxfordiiit-pet-dataset")
```

No se requiere cuenta de Kaggle si el dataset está disponible en la caché de Colab; en caso contrario, `kagglehub` solicitará las credenciales.

## Estructura de los datos

El nombre de cada archivo sigue el patrón `<raza>_<id>.jpg` (e.g. `beagle_115.jpg`). La regla de nombrado permite recuperar la especie de forma analítica:

- Nombre que **comienza en minúscula** → **perro** (`Dog`)
- Nombre que **comienza en mayúscula** → **gato** (`Cat`) — descartado en esta variante

## Resultados esperados

El reporte de clasificación multiclase, la matriz de confusión 25×25 y la lista de pares de clases mas confundidas permiten identificar las parejas de razas visualmente similares (e.g. `beagle` vs `english_cocker_spaniel`) que concentran los errores del modelo.

## Limitaciones conocidas

1. **Resolución baja:** las imágenes se redimensionan a 64×64, lo que pierde texturas finas de pelaje.
2. **Arquitectura básica:** sólo dos bloques convolucionales, sin aumentación de datos ni regularización avanzada.
3. **25 clases simultáneas:** un acierto por azar es 4%, por lo que el *accuracy* debe interpretarse junto al reporte macro (F1 por clase).

