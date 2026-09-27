# Pre-entrega Módulo 4: Consultas Multicapa para Análisis de Negocio

## 📌 Descripción del Proyecto
Este proyecto consiste en el desarrollo de un conjunto de consultas SQL avanzadas (multicapa) sobre una base de datos relacional de retail en **PostgreSQL**. El objetivo principal es transformar datos crudos de transacciones, clientes y productos en **inteligencia de negocio** para respaldar la toma de decisiones estratégicas.

---

## 🎯 Objetivos y Problemas de Negocio Resueltos

### 1. Rentabilidad por Categoría
* **¿Qué hice?:** Diseñé una consulta que une las tablas `ventas`, `productos` y `categorias` para calcular el total de unidades vendidas y los ingresos acumulados por cada categoría.
* **¿Cómo lo hice?:** Apliqué `INNER JOIN` entre las 3 tablas, agrupé los datos con `GROUP BY` y filtré los resultados agregados mediante `HAVING SUM(...) > 5000.00`.
* **¿Para qué lo hice?:** Para identificar qué líneas de productos generan la mayor facturación y superar la línea base operacional de $5,000. Permite al equipo directivo optimizar presupuestos de marketing y logística en los sectores más rentables.

### 2. Clientes sin Compras (Auditoría de Conversión)
* **¿Qué hice?:** Identifiqué a los usuarios registrados en el sistema que aún no han realizado su primera transacción.
* **¿Cómo lo hice?:** Utilicé un `LEFT JOIN` partiendo de la tabla `clientes` hacia `ventas` y `productos`, usando la función `COALESCE` para manejar los valores nulos (`NULL`) y reemplazar los montos por `$0.00`. Filtré los grupos mediante `HAVING COUNT(v.id_venta) = 0`.
* **¿Para qué lo hice?:** Para proveer al equipo de Marketing una lista limpia de "leads fríos", facilitando el diseño de campañas de re-engagement, cupones de primera compra o detección de fricciones en el proceso de registro.

### 3. Top de Compras por Cliente (Fidelización y Recencia)
* **¿Qué hice?:** Determiné el producto estrella (más comprado) por cada cliente y la fecha de su última interacción comercial.
* **¿Cómo lo hice?:** Utilicé una Expresión de Tabla Común (`WITH` / CTE) combinando `clientes`, `ventas` y `productos`, y apliqué la función de ventana `ROW_NUMBER() OVER (PARTITION BY ... ORDER BY ...)` para rankear las preferencias de cada usuario.
* **¿Para qué lo hice?:** Para personalización de ventas cruzadas (*cross-selling*) y análisis de recencia/retención (prevenir el abandono o *churn* de clientes según el tiempo transcurrido desde su última compra).

---

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Motor de Base de Datos:** PostgreSQL
* **IDE / Cliente de BD:** DBeaver 
* **Control de Versiones:** Git y GitHub
* **Lenguaje:** SQL 

---

## 📁 Estructura del Repositorio
```text
├── pre-entrega-modulo4.sql   # Script principal con las 3 consultas explicadas
└── README.md                 # Documentación técnica y de negocio del proyecto