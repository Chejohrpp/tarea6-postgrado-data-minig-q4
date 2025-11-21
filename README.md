# Tarea 6: Predicción de Tipo de Violencia Intrafamiliar usando Random Forest

## Descripción del Proyecto

Este proyecto implementa un modelo de **Random Forest** en R para predecir el tipo de violencia intrafamiliar en Guatemala, utilizando datos del Instituto Nacional de Estadística (INE) correspondientes al año 2024.

### Objetivo

El objetivo principal es predecir si un caso de violencia intrafamiliar corresponde a **violencia física/sexual con contacto** o a **violencia psicológica/patrimonial**, utilizando variables demográficas y contextuales de víctimas y agresores.

## Dataset

El dataset utilizado proviene del recurso público del INE de Guatemala:
- **Fuente**: [Violencia Intrafamiliar - INE Guatemala](https://datos.ine.gob.gt/dataset/violencia-intrafamiliar/resource/73875737-52c9-41b3-accf-37b44e534bec)
- **Archivo**: `base-de-datos-violencia-intrafamiliar-ano-2024_v3.xlsx`
- **Año**: 2024

## Variable Objetivo (Target)

La variable a predecir es **`TIPO_BINARIO`**, una clasificación binaria que agrupa los tipos de violencia en dos categorías:

- **`FISICA_CONTACTO`**: Incluye violencia física y/o sexual (con contacto físico)
- **`PSICO_PATRIMONIAL`**: Incluye violencia psicológica y/o patrimonial (sin contacto físico)

Esta variable se deriva de `HEC_TIPAGRE` mediante ingeniería de características.

## Variables Predictoras

El modelo utiliza las siguientes variables:

### Variables Demográficas
- `VIC_EDAD`: Edad de la víctima
- `AGR_EDAD`: Edad del agresor
- `VIC_SEXO`: Sexo de la víctima
- `AGR_SEXO`: Sexo del agresor
- `VIC_GRUPET`: Grupo étnico de la víctima
- `HEC_DEPTO`: Departamento donde ocurrió el hecho

### Variables Contextuales
- `VIC_REL_AGR`: Relación entre víctima y agresor
- `HEC_AREA`: Área geográfica (Urbano vs Rural)
- `VIC_TRABAJA`: Estado laboral de la víctima
- `AGR_TRABAJA`: Estado laboral del agresor

### Variables Calculadas (Feature Engineering)
- `GAP_EDAD`: Diferencia de edad entre agresor y víctima
- `TIPO_RELACION`: Agrupación de relación (Pareja vs Familia)

## Metodología

### 1. Limpieza de Datos
- Eliminación de valores "99" y "9" (códigos de "Ignorado")
- Eliminación de registros con valores faltantes (NA)

### 2. Ingeniería de Características
- Creación de la variable objetivo binaria a partir de `HEC_TIPAGRE`
- Cálculo del gap de edad entre agresor y víctima
- Agrupación de tipos de relación en categorías más amplias
- Conversión de variables categóricas a factores

### 3. División de Datos
- **80%** para entrenamiento
- **20%** para prueba
- Semilla aleatoria: `555` (para reproducibilidad)

### 4. Modelo Random Forest
- **Número de árboles**: 400
- **Cutoff personalizado**: `c(0.45, 0.55)` para optimizar la sensibilidad
- **Importancia de variables**: Habilitada

## Requisitos

### Paquetes de R necesarios:
```r
install.packages(c("readxl", "dplyr", "randomForest", "caret", "stringr"))
```

### Archivos necesarios:
- `base-de-datos-violencia-intrafamiliar-ano-2024_v3.xlsx` (debe estar en el directorio del proyecto)

## Cómo Ejecutar

1. Clonar o descargar este repositorio
2. Asegurarse de que el archivo Excel esté en el directorio raíz
3. Abrir `ScriptR6.Rmd` en RStudio
4. Ejecutar todas las celdas (Knit o Run All)

Alternativamente, ejecutar directamente en R:
```r
source("ScriptR6.Rmd")
```

## Resultados

El modelo genera:
1. **Resumen del modelo Random Forest**: Estadísticas generales del modelo
2. **Matriz de confusión**: Métricas de precisión, sensibilidad y especificidad
3. **Gráfico de importancia de variables**: Visualización de las variables más relevantes para la predicción

### Interpretación de la Predicción

El modelo permite identificar qué factores están más asociados con violencia física/sexual versus violencia psicológica/patrimonial. Las variables más importantes (según el gráfico de importancia) indican los factores de riesgo más relevantes para cada tipo de violencia.

## Estructura del Proyecto

```
Tarea6/
├── README.md
├── ScriptR6.Rmd              # Script principal de análisis
├── ScriptR6.nb.html          # Output HTML del notebook
├── base-de-datos-violencia-intrafamiliar-ano-2024_v3.xlsx
└── .gitignore
```

## Autor

**Sergio Rolando Hernandez Perez**

## Notas Importantes

- Este análisis utiliza un enfoque diferente a los filtros y predicciones de la Sesión 7, como se especifica en los requisitos de la tarea.
- El modelo está optimizado para detectar casos de violencia física/sexual mediante el ajuste del cutoff.
- Los resultados deben interpretarse en el contexto de políticas públicas y prevención de violencia doméstica.

## Repositorio

[Enlace al repositorio de código](https://github.com/Chejohrpp/tarea6-postgrado-data-minig-q4)

---

**Nota**: Este proyecto es parte de una tarea académica sobre Data Mining y utiliza técnicas de aprendizaje supervisado para análisis de datos sociales.

