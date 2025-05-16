# Cobertura-de-suelo-RBB
# Bosawas_Landsat_Mosaico_2001_2005

Este repositorio contiene un script desarrollado en **Google Earth Engine (GEE)** en lenguaje **JavaScript**, destinado a la creación de un **mosaico mediano libre de nubes** a partir de imágenes **Landsat 5 y Landsat 7** para el periodo **2000–2005**, en el área de la **Reserva de la Biosfera Bosawas (Nicaragua)**. Forma parte del trabajo de investigación para el **Trabajo Fin de Máster (TFM)** de Gabriela Campos.
---
## Objetivo

Generar un mosaico representativo de la cobertura y uso del suelo de Bosawas durante el periodo 2001–2005 mediante imágenes Landsat corregidas atmosféricamente, aplicando:

- Filtrado por nubosidad
- Enmascaramiento píxel a píxel de nubes y sombras
- Aplicación de factores de escala (reflectancia y temperatura)
- Composición mediana para eliminar artefactos y anomalías
---
## Datos utilizados

- **Landsat 5 Surface Reflectance**: `LANDSAT/LT05/C02/T1_L2`
- **Landsat 7 Surface Reflectance**: `LANDSAT/LE07/C02/T1_L2`
- Nivel de corrección: **Collection 2 / Level 2 (T1_L2)**
- Resolución espacial: **30 metros**
- Periodo de análisis: **2000-12-01 a 2005-04-30**
- Área de estudio: **Reserva de Biosfera Bosawas (polígono AOI cargado como `asset`)**
---
## Procesos implementados

1. **Carga y visualización del área de estudio (AOI)**
2. **Filtrado de imágenes Landsat 5 y 7 por:
   - Área geográfica (`filterBounds`)
   - Periodo de tiempo (`filterDate`)
   - Nivel de nubosidad global (`CLOUD_COVER < 50%`)**
3. **Unión de colecciones**
4. **Enmascaramiento de nubes y sombras** mediante la banda `QA_PIXEL` (bits 3 y 4)
5. **Aplicación de factores de escala**:
   - Reflectancia: `SR_Bx * 0.0000275 - 0.2`
   - Temperatura: `ST_B6 * 0.00341802 + 149.0`
6. **Creación de un mosaico mediano**
7. **Visualización en color natural (SR_B3, SR_B2, SR_B1)**
---
## Visualización del resultado

```javascript
var RGB2005 = {
  bands: ['SR_B3', 'SR_B2', 'SR_B1'],
  min: 0.0,
  max: 0.3,
};
Map.addLayer(mosaico2005, RGB2005, 'Mosaico 2001–2005');
