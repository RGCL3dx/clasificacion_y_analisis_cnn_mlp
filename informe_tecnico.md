# Informe técnico de proyecto

## Clasificación multiclase de razas de perro mediante red neuronal convolucional

**Fecha del informe:** 13 de octubre de 2026  
**Autor:** Ronald Cerda, Francisco Fierro e Ignacio Rodríguez. 

---

## 1. Resumen ejecutivo

Este documento presenta los resultados del diseño, entrenamiento y evaluación de una red neuronal convolucional creada para identificar **25 razas de perros**.

Aunque la fase de limpieza y organización de los datos se ejecutó correctamente, los resultados del modelo entrenado durante 10 épocas muestran limitaciones importantes. El sistema no logró aprender a identificar correctamente las razas en imágenes nuevas, demostrando que la arquitectura de la red y la cantidad de datos actuales son insuficientes para resolver un problema visual tan detallado.

## 2. Gestión del alcance

El trabajo se centró exclusivamente en la especie canina, analizando un total de **4.990 imágenes**.

Se descartó el uso de fotografías de gatos para evitar distorsiones en el aprendizaje. El proyecto también excluyó el uso de modelos preentrenados, ya que el objetivo principal era medir la capacidad de aprendizaje de una red construida completamente desde cero.

Esta restricción limitó el rendimiento final, pero permitió evaluar el comportamiento de un sistema básico frente a un problema complejo.

## 3. Gestión de los requisitos y la calidad

El requisito principal era lograr que el modelo distinguiera diferencias sutiles entre razas que se parecen mucho visualmente.

Para intentar cumplir este estándar, las imágenes se organizaron procurando que todas las razas tuvieran una representación equilibrada en los conjuntos de entrenamiento, validación y prueba.

Sin embargo, la calidad del aprendizaje se vio afectada por la incapacidad del algoritmo para manejar las variaciones normales de una fotografía, como:

- Cambios en la iluminación.
- Variaciones en la postura del animal.
- Diferencias en el fondo de las imágenes.
- Similitudes físicas entre distintas razas.

Estas condiciones dificultaron la identificación de características visuales generalizables a imágenes nuevas.

## 4. Gestión de riesgos del proyecto

Durante la planificación se identificó el riesgo de que el modelo no pudiera manejar la gran variación visual existente dentro de una misma raza.

Como medida, se utilizó una red neuronal convolucional (CNN) para detectar patrones visuales y características espaciales presentes en las imágenes.

No obstante, el riesgo se materializó debido a la cantidad limitada de imágenes por categoría. Esto provocó que el modelo comenzara a memorizar parcialmente las imágenes de entrenamiento en lugar de aprender características suficientemente representativas de cada raza.

Este comportamiento se conoce como **sobreajuste (*overfitting*)**.

## 5. Gestión de la ejecución e ingeniería de datos

El proceso de preparación de la información se completó de forma ordenada.

Las principales actividades realizadas fueron:

1. Extracción de las etiquetas de las razas desde los nombres de los archivos.
2. Conversión de las etiquetas a valores numéricos.
3. División de las imágenes en tres conjuntos:
   - **Entrenamiento:** utilizado para ajustar los parámetros del modelo.
   - **Validación:** utilizado para evaluar el rendimiento durante el entrenamiento.
   - **Prueba:** destinado a evaluar el rendimiento final con datos independientes.
4. Organización equilibrada de las clases para facilitar una evaluación justa del algoritmo.

La preparación de los datos permitió establecer una base adecuada para el entrenamiento, aunque la cantidad y diversidad de imágenes disponibles no fueron suficientes para alcanzar el rendimiento esperado.

## 6. Resultados del entrenamiento

Los resultados obtenidos después de **10 épocas de entrenamiento** evidencian un problema de sobreajuste y una capacidad de generalización limitada.

### 6.1. Métricas principales

| Indicador | Resultado |
|---|---:|
| Número de razas | 25 |
| Total de imágenes | 4.990 |
| Épocas de entrenamiento | 10 |
| Precisión en entrenamiento | 49,38 % |
| Precisión en validación | 22,06 % |

### 6.2. Análisis del rendimiento

Al finalizar el entrenamiento, el modelo alcanzó una precisión del **49,38 % en los datos de entrenamiento**. Sin embargo, al evaluar imágenes nuevas en el conjunto de validación, la precisión disminuyó hasta un **22,06 %**.

Esta diferencia evidencia que el modelo no logró generalizar adecuadamente los patrones visuales aprendidos.

Además, el indicador de error comenzó a aumentar progresivamente a partir de la sexta época de entrenamiento. Esto sugiere que, después de ese punto, el modelo comenzó a presentar mayores dificultades para mejorar su rendimiento con imágenes que no había visto anteriormente.

Aunque una precisión del 22,06 % supera la referencia aleatoria del 4 % para 25 clases equilibradas, el resultado sigue siendo insuficiente para una aplicación práctica confiable.

## 7. Conclusión

El proyecto permitió establecer un proceso ordenado para la gestión, limpieza y preparación de datos destinados a la clasificación multiclase de razas de perros.

Sin embargo, el modelo desarrollado no alcanzó la calidad necesaria para su aplicación práctica. Los resultados demuestran que entrenar una red neuronal convolucional desde cero con la cantidad de imágenes disponible no fue suficiente para distinguir de manera confiable las características físicas que diferencian a las 25 razas.

### 7.1. Recomendaciones futuras

Para mejorar el rendimiento del sistema, se proponen las siguientes acciones:

- **Aumento de datos (*Data Augmentation*):** aplicar transformaciones a las imágenes, como rotaciones, volteos y variaciones de iluminación, para mejorar la robustez del modelo.
- **Ampliación del conjunto de datos:** incorporar más imágenes reales y diversas por raza.
- **Optimización de hiperparámetros:** ajustar la tasa de aprendizaje, el tamaño del lote y los parámetros de regularización.
- **Control del sobreajuste:** implementar técnicas como *Early Stopping*, *Dropout* y regularización.
- **Evaluación detallada:** utilizar matrices de confusión y métricas por clase para identificar las razas con mayores dificultades de clasificación.

La implementación de estas mejoras permitiría desarrollar un sistema más robusto, con mayor capacidad de generalización y mejores resultados al clasificar nuevas imágenes. Ya que, el modelo requiere mejoras en la estrategia de entrenamiento, la cantidad de datos y la arquitectura utilizada antes de considerar su aplicación práctica.

---