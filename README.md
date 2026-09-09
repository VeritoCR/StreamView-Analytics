# StreamView Analytics — Visual Analytics para el Catálogo Audiovisual

**Autores:** Ginno Andrades-Verónica Cereceda
**Fecha:** Septiembre de 2026
**Versión:** 1.0
**Asignatura:** Visualización de Datos — Evaluación Parcial N°1

---

## 1. Justificación de Herramientas Colaborativas

Para garantizar la reproducibilidad y el control de versiones del proyecto, se seleccionaron dos herramientas principales:

* **GitHub:** repositorio (`StreamView-Analytics`) usado para versionar el notebook, los datasets, las imágenes generadas, el informe y los dashboards, manteniendo sincronizado el trabajo del equipo.
* **Deepnote:** entorno de notebooks usado para el análisis exploratorio, permitiendo ejecutar y documentar el proceso de limpieza, cálculo de KPIs y visualizaciones en un mismo lugar.
* **Power BI:** herramienta usada para construir los dashboards interactivos finales.
---

## 2. Descripción del Problema de Negocio y Objetivos

### 2.1 Problema de Negocio

StreamView Analytics es una plataforma de streaming que creció rápido en los últimos años y hoy administra un catálogo de miles de películas y series. El problema es que cada área maneja sus propios reportes, con criterios distintos entre sí, lo que genera varias versiones del mismo indicador y dificulta ver tendencias claras para tomar decisiones de adquisición, producción y posicionamiento de contenidos.

El equipo trabaja como consultora externa de Visual Analytics, encargada de transformar el catálogo corporativo en información visual clara que apoye esas decisiones, con foco en la Gerencia de Adquisición y Gestión de Contenidos.

### 2.2 Objetivos del Proyecto

* **Objetivo General:**
Diseñar e implementar una solución de Visual Analytics que comunique información relevante del catálogo audiovisual mediante dashboards interactivos, narrativas visuales y productos gráficos que apoyen la toma de decisiones de la Gerencia de Adquisición y Gestión de Contenidos.

* **Objetivos Específicos:**
  * Integrar los datasets de películas y series en un catálogo único, documentando y justificando cada decisión de limpieza.
  * Explorar el catálogo mediante visualizaciones que respondan preguntas de género, país, idioma, popularidad, valoración y rentabilidad.
  * Evaluar la relación entre popularidad y calificación del público, y entre presupuesto e ingresos en películas.
  * Construir dashboards ejecutivos con KPIs, filtros y navegación para distintos perfiles de usuario.
  * Formular recomendaciones de adquisición sustentadas en la evidencia encontrada.

---

## 3. Definición de KPIs

### 3.1 KPIs del Catálogo

* **Total de contenidos:** 32.000 (16.000 películas + 16.000 series).
* **Países representados:** 123. **Idiomas disponibles:** 83. **Géneros distintos:** 29.
* **Concentración de géneros:** Drama, Comedy y Animation suman más del 51% del catálogo.
* **Concentración geográfica y de idioma:** Estados Unidos concentra más de 8.100 títulos y el inglés está presente en cerca de 14.000 contenidos.

### 3.2 KPIs de Popularidad y Valoración

* **Popularidad promedio:** 42,6. **Calificación promedio (vote_average):** 5,7 / 10.
* **Relación popularidad–calificación:** correlación casi nula (r = 0,04); lo más popular no es necesariamente lo mejor evaluado.

### 3.3 KPIs Financieros (solo películas)

* **Cobertura de datos financieros:** 3.540 de 16.000 películas (22,1%) tienen budget y revenue válidos.
* **Tasa de rentabilidad:** 63,2% de esas películas generó ingresos superiores al presupuesto.
* **ROI mediano por género:** Horror lidera con 2,81x, por sobre géneros de mayor presupuesto promedio como Acción (1,93x) o Aventura (1,94x).

---

## 4. Fuentes de Datos y Metodología

### 4.1 Fuentes de Datos

* **Archivos:** `netflix_movies_detailed_up_to_2025.csv` y `netflix_tv_shows_detailed_up_to_2025.csv`, entregados como extracto del catálogo corporativo del caso StreamView Analytics.
* **Cantidad de datos:** 16.000 filas y 18 columnas en películas; 16.000 filas y 16 columnas en series (sin budget ni revenue).
* **Contenido de las columnas:** identificación del contenido (show_id, title, type), producción (director, cast, country, release_year, date_added), características (genres, language, duration, rating), desempeño (popularity, vote_count, vote_average) y datos financieros exclusivos de películas (budget, revenue).

### 4.2 Metodología

El proyecto sigue las etapas definidas en el caso semestral del ramo, cubriendo en esta primera entrega la Etapa 1:

1. **Etapa 1 — Comprensión del Negocio y Exploración Visual (EP1):** definición del stakeholder y objetivos de comunicación, integración de fuentes, revisión de calidad de datos, cálculo de KPIs y primeras visualizaciones. *(completada)*
2. **Etapa 2 — Diseño de Dashboards (EP2):** construcción de dashboards interactivos con filtros, navegación e interacción.
3. **Etapa 3 — Evaluación y Optimización (EP3):** evaluación crítica y rediseño de la solución.
4. **Etapa 4 — Presentación Ejecutiva (EFT):** entrega integral con defensa oral.

---

## 5. Resumen del Análisis Exploratorio de Datos (EDA)

* **Calidad de los datos:**
  * *Nulos:* budget y revenue están vacíos en el 100% de las series (esperado, según regla de negocio). La variable director tiene un 34,7% de valores nulos.
  * *Identificadores duplicados:* se detectaron 406 valores repetidos en show_id al unir ambas fuentes — 397 eran colisiones de numeración entre películas y series (obras distintas con el mismo número por azar) y 9 eran duplicados reales dentro de series. Se resolvió creando una clave compuesta (unique_content_id).
  * *Limitación relevante:* el catálogo tiene exactamente la misma cantidad de películas y series por cada año entre 2010 y 2025, lo que indica que la muestra fue balanceada artificialmente con fines académicos. Por eso, la evolución temporal se interpreta como composición del catálogo por año, no como crecimiento real de la industria.
* **Relación con la popularidad:**
  * Los contenidos más populares corresponden a series de emisión constante, no a películas de estreno, porque la popularidad mide interacción reciente y no calidad percibida.
  * La correlación entre popularidad y calificación es prácticamente nula (r = 0,04): un contenido puede ser muy visto sin estar bien evaluado, y viceversa.
* **Relación con la rentabilidad:**
  * Solo el 22,1% de las películas tiene datos financieros completos; de ese grupo, el 63,2% es rentable.
  * Un presupuesto alto no garantiza mejor retorno: géneros de menor costo promedio como Horror rinden mejor en ROI mediano que producciones más costosas.

---

## 6. Visualizaciones y Dashboards

* **Visualizaciones exploratorias:** gráficos de barras (composición del catálogo, top géneros/países/idiomas/directores), líneas (evolución de estrenos), dispersión (popularidad vs. calificación, presupuesto vs. ingresos), guardados en `imágenes/` con su justificación de diseño documentada en el notebook y el informe ejecutivo.
* **Dashboard de Eficiencia Financiera de las Películas:** KPIs de presupuesto, ingresos y ROI, con filtros por año, país y género; incluye ranking de ROI por género y comparativa histórica de presupuesto vs. ingresos.
* **Dashboard Estratégico de Catálogo:** KPIs generales del catálogo, ranking de mercados productores, evolución de la calificación en el tiempo y popularidad por género, con filtros por tipo de contenido, año y país.

Ambos dashboards están en `panel/`.

---

## 7. Limitaciones y Consideraciones

* **Datos balanceados artificialmente:** la cantidad idéntica de estrenos por año y tipo de contenido no representa el volumen real de producción de la industria, por lo que los análisis de "evolución" deben leerse como composición del catálogo, no como tendencia real.
* **Cobertura financiera parcial:** los indicadores de ROI y rentabilidad se calculan solo sobre el 22,1% de las películas que tienen datos válidos, por lo que no pueden generalizarse al catálogo completo.
* **Datos faltantes en director:** un tercio de los registros no tiene director asociado, lo que limita el análisis por creador.
* **Documentación de supuestos:** cada decisión de limpieza e integración queda documentada en el notebook y en el informe ejecutivo, para que cualquier persona que retome el proyecto entienda el alcance y las limitaciones del trabajo ya hecho.

---

## 8. Estructura del Repositorio

```text
StreamView-Analytics/
├── data/
│   ├── netflix_movies_detailed_up_to_2025.csv
│   └── netflix_tv_shows_detailed_up_to_2025.csv
├── notebooks/
│   └── 01_EDA_StreamView_Analytics.ipynb
├── images/
│   ├── Composición película vs serie.png
│   ├── Distribución del catálogo por calificación promedio.png
│   ├── Evolución de estrenos por año y tipo de contenido.png
│   ├── Presupuesto vs Ingresos.png
│   ├── Relación entre calificación del público y popularidad.png
│   ├── Top 10 contenidos más populares.png
│   ├── Top 10 directores con mayor cantidad de contenidos.png
│   ├── Top 10 géneros con mayor cantidad de contenidos.png
│   ├── Top 10 idiomas con mayor cantidad de contenidos.png
│   ├── Top 10 países productores de contenido.png
│   └── Top Géneros por Eficiencia Financiera.png
├── dashboard/
│   └── (dashboards de Eficiencia Financiera y Catálogo Estratégico)
├── doc/
│   └── Informe_EP1_StreamView_Analytics.pdf
├── src/
└── README.md
```
