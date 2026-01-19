# Guía de Implementación en Tableau - Análisis Easy Loans 2023

## 1. Configuración Inicial

### 1.1 Conexión de Datos
1. Abrir Tableau Desktop
2. Conectar a archivo de texto: `data/easy_loans_2023.csv`
3. Verificar que los tipos de datos sean correctos:
   - Fechas: Fecha_Solicitud, Fecha_Aprobacion, Fecha_Desembolso, Fecha_Ultimo_Pago
   - Números: Montos, tasas, edad, score, coordenadas
   - Texto: Nombres, ciudades, tipos, estados

### 1.2 Preparación de Datos (Data Source)
Crear los siguientes campos calculados en la fuente de datos:

#### Campos Calculados Básicos
```
// Diferencia entre Solicitud y Aprobación
Diferencia_Monto
[Monto_Solicitado] - [Monto_Aprobado]

// Tasa de Aprobación (%)
Tasa_Aprobacion
([Monto_Aprobado] / [Monto_Solicitado]) * 100

// Porcentaje de Reembolso
Porcentaje_Reembolso
([Monto_Pagado] / [Monto_Aprobado]) * 100

// Días hasta Aprobación
Dias_Aprobacion
DATEDIFF('day', [Fecha_Solicitud], [Fecha_Aprobacion])

// Días hasta Desembolso
Dias_Desembolso
DATEDIFF('day', [Fecha_Aprobacion], [Fecha_Desembolso])

// Monto Pendiente
Monto_Pendiente
[Monto_Aprobado] - [Monto_Pagado]

// Intereses Totales (simplificado)
Intereses_Totales
[Monto_Aprobado] * ([Tasa_Interes]/100) * ([Plazo_Meses]/12)

// Mes de Solicitud
Mes_Solicitud
MONTH([Fecha_Solicitud])

// Trimestre de Solicitud
Trimestre_Solicitud
DATEPART('quarter', [Fecha_Solicitud])
```

## 2. Cálculos Clave (Calculados en Hojas)

### 2.1 Cálculos de Promedio
```
// Promedio de Monto Aprobado
AVG([Monto_Aprobado])

// Promedio de Tasa de Interés
AVG([Tasa_Interes])

// Promedio de Plazo
AVG([Plazo_Meses])

// Promedio de Score de Crédito
AVG([Score_Credito])

// Promedio de Reembolso por Tipo
{ FIXED [Tipo_Prestamo] : AVG([Porcentaje_Reembolso]) }
```

### 2.2 Cálculos Acumulados
```
// Monto Acumulado Aprobado
RUNNING_SUM(SUM([Monto_Aprobado]))

// Monto Acumulado Pagado
RUNNING_SUM(SUM([Monto_Pagado]))

// Número Acumulado de Préstamos
RUNNING_COUNT([ID_Prestamo])

// Porcentaje Acumulado
RUNNING_SUM(SUM([Monto_Aprobado])) / TOTAL(SUM([Monto_Aprobado]))
```

### 2.3 Cálculos de Reembolso
```
// Tasa de Recuperación
SUM([Monto_Pagado]) / SUM([Monto_Aprobado])

// Monto Total Pendiente
SUM([Monto_Pendiente])

// Porcentaje de Préstamos Completados
COUNTD(IF [Estado_Prestamo] = "Completado" THEN [ID_Prestamo] END) / 
COUNTD([ID_Prestamo])

// Porcentaje de Mora
COUNTD(IF [Estado_Prestamo] = "Moroso" THEN [ID_Prestamo] END) / 
COUNTD([ID_Prestamo])
```

### 2.4 Análisis de Desviación
```
// Desviación Absoluta del Monto
ABS([Monto_Solicitado] - [Monto_Aprobado])

// Desviación Porcentual
(([Monto_Solicitado] - [Monto_Aprobado]) / [Monto_Solicitado]) * 100

// Desviación vs Promedio
[Monto_Aprobado] - WINDOW_AVG(SUM([Monto_Aprobado]))

// Categoría de Desviación
IF [Tasa_Aprobacion] >= 100 THEN "Aprobado Completo"
ELSEIF [Tasa_Aprobacion] >= 90 THEN "Aprobado Alto"
ELSEIF [Tasa_Aprobacion] >= 75 THEN "Aprobado Medio"
ELSE "Aprobado Bajo"
END
```

## 3. Visualizaciones Requeridas

### 3.1 Dashboard de KPIs Principales
Crear hojas individuales para cada KPI:

**Hoja 1: Total Préstamos**
- Métrica: `COUNTD([ID_Prestamo])`
- Tipo: Texto grande con formato
- Color: Azul (#1f77b4)

**Hoja 2: Monto Total Aprobado**
- Métrica: `SUM([Monto_Aprobado])`
- Formato: Moneda ($ ###,###)
- Color: Verde (#2ca02c)

**Hoja 3: Tasa de Recuperación**
- Métrica: `SUM([Monto_Pagado]) / SUM([Monto_Aprobado])`
- Formato: Porcentaje (##.#%)
- Color condicional: >90% Verde, 70-90% Amarillo, <70% Rojo

**Hoja 4: Tasa de Mora**
- Métrica: `COUNTD(IF [Estado_Prestamo] = "Moroso" THEN [ID_Prestamo] END) / COUNTD([ID_Prestamo])`
- Formato: Porcentaje (##.#%)
- Color: Rojo (#d62728)

**Hoja 5: Monto Promedio**
- Métrica: `AVG([Monto_Aprobado])`
- Formato: Moneda
- Color: Naranja (#ff7f0e)

### 3.2 Mapa Geográfico
**Configuración:**
- Tipo: Mapa de símbolos
- Latitud: [Latitud] (dimensión geográfica)
- Longitud: [Longitud] (dimensión geográfica)
- Tamaño: SUM([Monto_Aprobado])
- Color: AVG([Tasa_Interes])
- Etiquetas: [Ciudad] y SUM([Monto_Aprobado])
- Tooltip personalizado con:
  - Ciudad
  - Número de préstamos
  - Monto total aprobado
  - Tasa de interés promedio
  - Estado predominante

### 3.3 Gráfico de Evolución Acumulada
**Configuración:**
- Tipo: Líneas dobles
- Eje X: MONTH([Fecha_Desembolso])
- Eje Y (dual):
  - Línea 1: RUNNING_SUM(SUM([Monto_Aprobado]))
  - Línea 2: RUNNING_SUM(SUM([Monto_Pagado]))
- Colores diferenciados
- Añadir líneas de referencia para:
  - Promedio mensual
  - Tendencia
- Formato con separadores de miles

### 3.4 Análisis de Desviación
**Gráfico de Barras - Desviación por Tipo de Préstamo:**
- Filas: [Tipo_Prestamo]
- Columnas: AVG([Diferencia_Monto])
- Color: por signo (positivo/negativo)
- Ordenar por magnitud

**Scatter Plot - Monto Solicitado vs Aprobado:**
- Columnas: [Monto_Solicitado]
- Filas: [Monto_Aprobado]
- Color: [Tipo_Prestamo]
- Tamaño: [Score_Credito]
- Añadir línea de tendencia
- Línea de referencia diagonal (y=x)

### 3.5 Gráficos Adicionales

**Distribución por Tipo de Préstamo (Pie Chart):**
- Ángulo: COUNT([ID_Prestamo])
- Color: [Tipo_Prestamo]
- Etiquetas: Porcentaje

**Timeline de Préstamos (Gantt Chart):**
- Filas: [ID_Prestamo] (top 20)
- Columnas: [Fecha_Solicitud]
- Marca: Gantt
- Tamaño: DATEDIFF('day', [Fecha_Solicitud], [Fecha_Ultimo_Pago])
- Color: [Estado_Prestamo]

**Heatmap de Tasa de Interés:**
- Columnas: [Tipo_Prestamo]
- Filas: [Trimestre_Solicitud]
- Color: AVG([Tasa_Interes])
- Etiquetas: Valor promedio
- Esquema de color: Rojo-Amarillo-Verde (invertido)

## 4. Configuración de Dashboards Interactivos

### 4.1 Dashboard Principal: "Overview Easy Loans 2023"
**Layout (1920x1080):**
```
+---------------------------+---------------------------+
|         KPI Cards (5 columnas, arriba)              |
+---------------------------+---------------------------+
|  Mapa Geográfico        |  Gráfico Acumulado        |
|  (50% ancho)            |  (50% ancho)              |
+---------------------------+---------------------------+
|  Distribución Tipos     |  Análisis Desviación      |
|  (50% ancho)            |  (50% ancho)              |
+---------------------------+---------------------------+
```

**Filtros Globales (aplicar a todas las hojas):**
1. Rango de fechas: [Fecha_Solicitud]
2. Tipo de préstamo: [Tipo_Prestamo] (multi-select)
3. Estado del préstamo: [Estado_Prestamo] (multi-select)
4. Ciudad: [Ciudad] (multi-select con búsqueda)
5. Rango de montos: [Monto_Aprobado] (slider)

**Acciones de Dashboard:**
- Filtro al seleccionar en mapa → afecta otros gráficos
- Highlight al pasar sobre elementos
- Tooltip con drill-down a detalles

### 4.2 Dashboard Secundario: "Análisis de Riesgo"
**Componentes:**
1. Scatter Plot: Score Crédito vs Tasa de Mora
2. Box Plot: Distribución de Score por Estado
3. Heatmap: Mora por Ciudad y Tipo
4. Tabla detallada de préstamos morosos

### 4.3 Dashboard Terciario: "Análisis Financiero"
**Componentes:**
1. Waterfall Chart: Flujo de efectivo mensual
2. Gráfico de barras: Top 10 ciudades por monto
3. Tabla de resumen por tipo de préstamo
4. Indicadores de eficiencia de aprobación

## 5. Parámetros Ajustables

### 5.1 Crear Parámetros
```
Parámetro: Objetivo_Recuperacion
Tipo: Float
Rango: 0.7 - 1.0
Valor actual: 0.85
Formato: Porcentaje

Parámetro: Top_N_Ciudades
Tipo: Integer
Rango: 5 - 20
Valor actual: 10

Parámetro: Umbral_Mora
Tipo: Float
Rango: 0.01 - 0.15
Valor actual: 0.05
Formato: Porcentaje

Parámetro: Metrica_Principal
Tipo: String
Lista: "Monto Aprobado", "Número de Préstamos", "Tasa de Recuperación"
Valor actual: "Monto Aprobado"
```

### 5.2 Usar Parámetros en Cálculos
```
// Cálculo dinámico basado en parámetro
Metrica_Seleccionada
CASE [Metrica_Principal]
    WHEN "Monto Aprobado" THEN SUM([Monto_Aprobado])
    WHEN "Número de Préstamos" THEN COUNTD([ID_Prestamo])
    WHEN "Tasa de Recuperación" THEN SUM([Monto_Pagado])/SUM([Monto_Aprobado])
END

// Indicador de cumplimiento
Cumple_Objetivo
IF [Tasa_Recuperacion] >= [Objetivo_Recuperacion] THEN "✓ Cumple"
ELSE "✗ No Cumple"
END

// Top N dinámico
Ranking_Ciudades
IF RANK(SUM([Monto_Aprobado])) <= [Top_N_Ciudades] THEN [Ciudad]
ELSE "Otras"
END
```

### 5.3 Controles de Parámetros en Dashboard
- Agregar controles visibles para cada parámetro
- Ubicar en panel lateral o superior
- Usar tipos apropiados: slider, lista desplegable, etc.

## 6. Formatos y Estilo

### 6.1 Paleta de Colores
```
Tipo de Préstamo:
- Personal: #1f77b4 (Azul)
- Hipotecario: #2ca02c (Verde)
- Automotriz: #ff7f0e (Naranja)
- Empresarial: #d62728 (Rojo)

Estado:
- Activo: #2ca02c (Verde)
- Completado: #1f77b4 (Azul)
- Moroso: #d62728 (Rojo)
```

### 6.2 Formato de Números
- Montos: `$ ###,###` (sin decimales)
- Porcentajes: `##.#%`
- Tasas de interés: `##.##%`
- Fechas: `dd/mm/yyyy`

### 6.3 Tooltips Personalizados
Ejemplo para mapa:
```
<Ciudad>: <SUM(Monto_Aprobado)>
Préstamos: <COUNTD(ID_Prestamo)>
Tasa Promedio: <AVG(Tasa_Interes)>%
Recuperación: <SUM(Monto_Pagado)/SUM(Monto_Aprobado)>%
```

## 7. Exportación y Entrega

### 7.1 Crear Packaged Workbook (.twbx)
1. File → Save As
2. Seleccionar tipo: "Tableau Packaged Workbook (*.twbx)"
3. Nombre: `Easy_Loans_2023_Analisis_BI.twbx`
4. Verificar que incluya el archivo de datos

### 7.2 Publicación en Tableau Cloud (Bonus)
1. Server → Tableau Cloud → Sign In
2. Seleccionar proyecto destino
3. Establecer permisos y visibilidad
4. Publicar workbook y data source
5. Capturar URL de visualización
6. Tomar screenshot del dashboard publicado
7. Guardar screenshot en: `images/tableau_cloud_dashboard.png`

### 7.3 Checklist de Entrega
- [ ] Archivo .twbx funcional y completo
- [ ] Todos los dashboards configurados
- [ ] Filtros y parámetros operativos
- [ ] Tooltips personalizados
- [ ] Formato y estilo consistente
- [ ] Archivo de datos incluido en packaged workbook
- [ ] (Bonus) Screenshot de Tableau Cloud

## 8. Documentación de Insights

### 8.1 Crear Hoja de Story en Tableau
Estructura de la historia (7-10 puntos):

**Punto 1: Introducción**
- Dashboard Overview
- Resumen ejecutivo en caja de texto

**Punto 2: Volumen de Operaciones**
- Gráfico de préstamos por mes
- Insight: Tendencias estacionales

**Punto 3: Distribución Geográfica**
- Mapa con concentración
- Insight: Regiones de mayor actividad

**Punto 4: Análisis de Tipos**
- Comparativa por tipo de préstamo
- Insight: Rentabilidad por categoría

**Punto 5: Performance de Recuperación**
- Gráfico acumulado de pagos
- Insight: Tasa de éxito en cobranza

**Punto 6: Análisis de Riesgo**
- Préstamos morosos por segmento
- Insight: Factores de riesgo identificados

**Punto 7: Recomendaciones**
- Dashboard con métricas clave
- Texto con recomendaciones estratégicas

### 8.2 Plantilla de Insights Estratégicos
Documentar en archivo separado (ver `insights_estrategicos.md`):
- Hallazgos principales
- Oportunidades identificadas
- Riesgos detectados
- Recomendaciones operativas
- Acciones propuestas

## 9. Validación Final

### Checklist de Calidad:
- [ ] Datos cargan correctamente sin errores
- [ ] Todos los cálculos funcionan apropiadamente
- [ ] Filtros se aplican correctamente entre hojas
- [ ] Parámetros modifican las visualizaciones
- [ ] Mapas muestran todas las ubicaciones
- [ ] Gráficos acumulados calculan correctamente
- [ ] Tooltips muestran información relevante
- [ ] Formato es consistente y profesional
- [ ] Dashboard es responsive y legible
- [ ] Story cuenta una narrativa coherente
- [ ] Performance es aceptable (<5 seg carga)

## 10. Tips Avanzados

### 10.1 Optimización de Performance
- Usar extractos en lugar de conexiones en vivo
- Limitar el uso de cálculos table calculations
- Agregar datos en la fuente cuando sea posible
- Ocultar hojas no utilizadas

### 10.2 Interactividad Avanzada
- Usar acciones de URL para links externos
- Configurar acciones de cambio de hoja
- Implementar navegación con botones
- Crear filtros en cascada

### 10.3 Análisis Predictivo (Opcional)
- Agregar líneas de tendencia con R²
- Usar forecasting para proyecciones
- Análisis de clustering para segmentación
- Bandas de confianza en predicciones
