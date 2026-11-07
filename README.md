# telecom-analysis

# Análisis del comportamiento de clientes de ConnectaTel

## Objetivo

Analizar el comportamiento de los clientes de ConnectaTel con información registrada hasta 2024. El proyecto explora y limpia los datos, resume el uso de llamadas y mensajes por usuario, identifica posibles valores atípicos y crea segmentos por edad y nivel de uso. Los resultados permiten describir patrones de consumo y proponer oportunidades para mejorar los planes y la retención de clientes.

## Datasets utilizados

El análisis utiliza tres archivos CSV:

- `plans.csv`: información de los planes, como precio, minutos y datos incluidos, y costos por consumo adicional.
- `users_latam.csv`: información de los clientes, como edad, ciudad, fecha de registro, plan contratado y churn.
- `usage.csv`: registros de uso de llamadas y mensajes asociados a usuarios y fechas.
El notebook carga estos archivos en los DataFrames `plans`, `users` y `usage`. Las rutas originales son `/datasets/plans.csv`, `/datasets/users_latam.csv` y `/datasets/usage.csv`; pueden ajustarse según la ubicación de los archivos.

## Etapas del análisis

1. **Carga y exploración:** revisión de muestras, dimensiones, tipos de datos y valores no nulos.
2. **Diagnóstico de calidad:** inspección de valores faltantes, sentinels, categorías y fechas; se consideran datos registrados hasta 2024.
3. **Limpieza:** tratamiento del sentinel `-999` en `age`, del valor `?` en `city` y de fechas fuera de rango. Los nulos de las variables de uso se evalúan antes de decidir cómo tratarlos.
4. **Perfil de uso:** agregación por usuario del número de mensajes, llamadas y minutos de llamada. Luego se combina con la información de clientes para crear `user_profile`.
5. **Análisis visual y valores atípicos:** elaboración de histogramas por plan y boxplots; cálculo de límites superiores mediante el método IQR. Los valores señalados por IQR se consideran posibles atípicos, no errores confirmados.
6. **Segmentación:** clasificación de usuarios por nivel de uso (`Bajo uso`, `Uso medio`, `Alto uso`) y por edad (`Joven`, `Adulto`, `Adulto Mayor`).

## Cómo ejecutar el notebook en Google Colab

1. Descarga el archivo `.ipynb` del repositorio.
2. Abre Google Colab y selecciona **Archivo → Subir notebook**. Elige el archivo descargado.
3. Sube los tres archivos CSV a Colab, por ejemplo, dentro de una carpeta llamada `datasets`.
4. Ajusta la celda de carga para que las rutas correspondan a la ubicación de los archivos:

## Guía breve de reproducción

- Mantén el notebook y los tres archivos CSV disponibles y registra las rutas utilizadas.
- Verifica que los archivos incluyan las columnas esperadas, como `user_id`, `age`, `city`, `reg_date`, `plan`, `date` y `type`.
- Ejecuta el notebook de principio a fin para reproducir la limpieza, las métricas, los gráficos y los segmentos.
- Si los datos contienen varios años y quieres analizar solo 2024, filtra `usage` por año antes de agregar los datos por usuario.
- No elimines automáticamente los valores que superen los límites IQR: primero comprueba si reflejan actividad real o errores de registro.
- Si modificas los umbrales de segmentación, actualiza también las interpretaciones y conclusiones.

## Requisitos

Python 3 y las bibliotecas `pandas`, `numpy`, `matplotlib` y `seaborn`.

## Archivos del proyecto

- Notebook: `S7 Version-Estudiante-Project-ConnectaTel.ipynb`
- Datos: `plans.csv`, `users_latam.csv` y `usage.csv`

