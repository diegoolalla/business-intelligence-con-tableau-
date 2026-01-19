# Guía Rápida - Creación del Archivo .twbx

## 🎯 Objetivo
Esta guía te ayudará a crear el archivo Tableau Packaged Workbook (.twbx) con todos los dashboards configurados.

## 📋 Pre-requisitos
- Tableau Desktop instalado (versión 2023.1 o superior)
- Archivo `data/easy_loans_2023.csv` disponible
- Documentación leída: `docs/tableau_implementation_guide.md`

## 🚀 Pasos Rápidos

### 1. Conectar Datos (5 minutos)
```
1. Abrir Tableau Desktop
2. Connect → Text File
3. Seleccionar: data/easy_loans_2023.csv
4. Verificar tipos de datos:
   - Fechas: Date
   - Montos: Number (decimal)
   - IDs, nombres: String
5. Rename Data Source: "Easy Loans 2023"
```

### 2. Crear Campos Calculados Base (10 minutos)
En la pestaña Data Source, crear:

```tableau
// Diferencia_Monto
[Monto_Solicitado] - [Monto_Aprobado]

// Tasa_Aprobacion
([Monto_Aprobado] / [Monto_Solicitado]) * 100

// Porcentaje_Reembolso
([Monto_Pagado] / [Monto_Aprobado]) * 100

// Monto_Pendiente
[Monto_Aprobado] - [Monto_Pagado]

// Mes_Solicitud (para agrupación)
MONTH([Fecha_Solicitud])
```

### 3. Crear Hojas de KPIs (15 minutos)

#### KPI 1: Total Préstamos
```
Nueva Hoja → "KPI - Total Prestamos"
Drag: COUNTD([ID_Prestamo]) a Text
Format: Number (standard), Font Size 36
Color: #1f77b4 (azul)
Title: "Total Préstamos"
```

#### KPI 2: Monto Total Aprobado
```
Nueva Hoja → "KPI - Monto Total"
Drag: SUM([Monto_Aprobado]) a Text
Format: Currency $ ###,###, Font Size 36
Color: #2ca02c (verde)
Title: "Monto Total Aprobado"
```

#### KPI 3: Tasa de Recuperación
```
Nueva Hoja → "KPI - Recuperacion"
Calculated Field: SUM([Monto_Pagado]) / SUM([Monto_Aprobado])
Drag a Text
Format: Percentage ##.#%, Font Size 36
Color: Conditional
  - >90%: Verde
  - 70-90%: Amarillo
  - <70%: Rojo
Title: "Tasa de Recuperación"
```

#### KPI 4: Tasa de Mora
```
Nueva Hoja → "KPI - Mora"
Calculated Field: 
  COUNTD(IF [Estado_Prestamo] = "Moroso" THEN [ID_Prestamo] END) / 
  COUNTD([ID_Prestamo])
Format: Percentage ##.#%, Font Size 36
Color: #d62728 (rojo)
Title: "Tasa de Mora"
```

#### KPI 5: Monto Promedio
```
Nueva Hoja → "KPI - Promedio"
Drag: AVG([Monto_Aprobado]) a Text
Format: Currency $ ###,###, Font Size 36
Color: #ff7f0e (naranja)
Title: "Monto Promedio"
```

### 4. Crear Mapa Geográfico (10 minutos)
```
Nueva Hoja → "Mapa Geografico"
1. Drag [Longitud] a Columns
2. Drag [Latitud] a Rows
3. Change both to Dimension (right-click → Dimension)
4. Drag SUM([Monto_Aprobado]) a Size
5. Drag AVG([Tasa_Interes]) a Color
6. Drag [Ciudad] a Label
7. Map Style → Normal
8. Color: Red-Yellow-Green (reversed)
9. Size: Adjust for visibility
10. Tooltip: Customize con Ciudad, Monto, Tasa, Cantidad
```

### 5. Crear Gráfico Acumulado (10 minutos)
```
Nueva Hoja → "Evolucion Acumulada"
1. Drag MONTH([Fecha_Desembolso]) a Columns
2. Drag SUM([Monto_Aprobado]) a Rows
3. Quick Table Calculation → Running Total
4. Duplicate axis: Ctrl+Drag SUM([Monto_Aprobado]) axis
5. Change second to SUM([Monto_Pagado])
6. Quick Table Calculation → Running Total
7. Dual Axis → Synchronize Axis
8. Format:
   - Monto Aprobado: Blue line
   - Monto Pagado: Green line
9. Add Reference Lines: Average, Trend
10. Title: "Evolución Acumulada de Montos"
```

### 6. Crear Análisis de Desviación (10 minutos)
```
Nueva Hoja → "Analisis Desviacion"
1. Drag [Tipo_Prestamo] a Rows
2. Drag AVG([Diferencia_Monto]) a Columns
3. Sort descending by value
4. Color by: Calculated Field
   IF AVG([Diferencia_Monto]) < 0 THEN "Negativo" ELSE "Positivo" END
   Red for positive (rechazado), Green for negative (aprobado más)
5. Add labels with values
6. Title: "Desviación Promedio por Tipo de Préstamo"
```

### 7. Gráficos Adicionales (15 minutos)

#### Distribución por Tipo (Pie Chart)
```
Nueva Hoja → "Distribucion Tipos"
Marks: Pie
Angle: COUNT([ID_Prestamo])
Color: [Tipo_Prestamo]
Label: Percentage
```

#### Heatmap Tasa de Interés
```
Nueva Hoja → "Heatmap Tasas"
Columns: [Tipo_Prestamo]
Rows: QUARTER([Fecha_Solicitud])
Marks: Square
Color: AVG([Tasa_Interes])
Text: AVG([Tasa_Interes]) formatted as ##.##%
Color Scheme: Red-Yellow-Green (reversed)
```

### 8. Crear Filtros Globales (5 minutos)
```
En cualquier hoja:
1. Drag [Fecha_Solicitud] → Filters
   - Range of Dates → Select range
   - Show Filter → Date Range
   
2. Drag [Tipo_Prestamo] → Filters
   - Select all
   - Show Filter → Multiple Values (dropdown)
   
3. Drag [Estado_Prestamo] → Filters
   - Select all
   - Show Filter → Multiple Values (dropdown)
   
4. Drag [Ciudad] → Filters
   - Select all
   - Show Filter → Multiple Values (list with search)
   
5. Drag [Monto_Aprobado] → Filters
   - Range → Min to Max
   - Show Filter → Range slider
```

### 9. Crear Parámetros (5 minutos)
```
1. Create Parameter → "Objetivo_Recuperacion"
   Data Type: Float
   Range: 0.7 to 1.0
   Current Value: 0.85
   Display Format: Percentage
   
2. Create Parameter → "Top_N_Ciudades"
   Data Type: Integer
   Range: 5 to 20
   Current Value: 10
   
3. Create Parameter → "Metrica_Principal"
   Data Type: String
   List: "Monto Aprobado", "Número de Préstamos", "Tasa de Recuperación"
   Current Value: "Monto Aprobado"
   
Show Parameter Control for each
```

### 10. Crear Dashboard Principal (15 minutos)
```
New Dashboard → "Overview Easy Loans 2023"
Size: Fixed (1920 x 1080) or Automatic

Layout:
1. Top Row (Height 150px):
   - Horizontal container
   - Add 5 KPI sheets
   - Equal sizing
   
2. Middle Row:
   - Horizontal container (50/50)
   - Left: Mapa Geografico
   - Right: Evolucion Acumulada
   
3. Bottom Row:
   - Horizontal container (50/50)
   - Left: Distribucion Tipos
   - Right: Analisis Desviacion

4. Sidebar (Right):
   - Add all filters
   - Add parameters
   - Width: 250px

5. Apply Filters to All Worksheets:
   - Click each filter → Apply to Worksheets → All Using This Data Source

6. Add Actions:
   - Dashboard → Actions → Add Action
   - Filter: Click on Map → Filters other sheets
   - Highlight: Hover on elements
```

### 11. Dashboards Adicionales (Opcional, 20 minutos)

#### Dashboard "Análisis de Riesgo"
```
Components:
- Scatter: [Score_Credito] vs [Estado_Prestamo]
- Bar Chart: Mora por [Tipo_Prestamo]
- Table: Detalles de préstamos morosos
```

#### Dashboard "Análisis Financiero"
```
Components:
- Bar Chart: Top ciudades por monto
- Table: Resumen por tipo
- Timeline: Préstamos por mes
```

### 12. Crear Story (15 minutos)
```
New Story → "Easy Loans 2023 - Insights"

Story Points:
1. "Overview General"
   - Add dashboard Overview
   - Caption: "Resumen ejecutivo 2023..."

2. "Distribución Geográfica"
   - Add Mapa sheet maximized
   - Caption: "Concentración en Buenos Aires..."

3. "Evolución Temporal"
   - Add Evolucion Acumulada
   - Caption: "Crecimiento sostenido durante el año..."

4. "Análisis de Riesgo"
   - Add sheets relevantes
   - Caption: "Tasa de mora controlada..."

5. "Recomendaciones"
   - Add dashboard Overview con anotaciones
   - Caption: "Acciones clave: Expansión geográfica..."
```

### 13. Formato y Estilo (10 minutos)
```
1. Workbook Theme:
   Format → Workbook → Default → Clean
   
2. Colors:
   Edit Colors → Create Custom Palette
   - Personal: #1f77b4
   - Hipotecario: #2ca02c
   - Automotriz: #ff7f0e
   - Empresarial: #d62728
   
3. Fonts:
   Format → Workbook → Fonts
   - Title: 14pt Bold
   - Text: 10pt Regular
   
4. Tooltips:
   All sheets → Tooltip → Include:
   - Relevant dimensions
   - Formatted measures
   - Remove "Command buttons"
```

### 14. Guardar como .twbx (2 minutos)
```
1. File → Save As
2. Save as Type: "Tableau Packaged Workbook (*.twbx)"
3. Filename: "Easy_Loans_2023_Analisis_BI.twbx"
4. Location: Project root directory
5. Click Save
6. Verify: File includes all data (check file size > 50KB)
```

## ✅ Checklist de Validación

### Datos
- [ ] CSV importado correctamente
- [ ] Todos los campos con tipo correcto
- [ ] Sin errores de parsing

### Cálculos
- [ ] Todos los campos calculados funcionan
- [ ] Fórmulas dan resultados esperados
- [ ] Table calculations computando correctamente

### Visualizaciones
- [ ] 5 KPIs visibles y con formato
- [ ] Mapa muestra todas las ciudades
- [ ] Gráfico acumulado con 2 líneas
- [ ] Desviación por tipo visible
- [ ] Colores consistentes

### Dashboard
- [ ] Todos los elementos alineados
- [ ] Filtros funcionan en todas las hojas
- [ ] Parámetros modifican visualizaciones
- [ ] No hay espacios blancos extraños
- [ ] Responsive o tamaño fijo apropiado

### Interactividad
- [ ] Filtros aplican a todos los elementos
- [ ] Click en mapa filtra otros gráficos
- [ ] Hover muestra tooltips
- [ ] Parámetros cambian visualizaciones

### Formato
- [ ] Títulos descriptivos
- [ ] Números con formato correcto
- [ ] Colores profesionales
- [ ] Tooltips personalizados

### Archivo
- [ ] Se guarda como .twbx
- [ ] Incluye los datos (packaged)
- [ ] Se puede abrir en otra computadora
- [ ] Tamaño razonable (<10MB)

## 🚨 Troubleshooting

### Problema: Mapa no muestra puntos
**Solución:**
- Verificar que Latitud y Longitud son Dimensions
- Check que no son agregadas (no deben tener SUM)
- Usar "Assign Geographic Role" si es necesario

### Problema: Cálculos acumulados incorrectos
**Solución:**
- Verificar "Compute Using" → Table (across)
- Check que fecha está en formato correcto
- Ordenar por fecha ascendente

### Problema: Filtros no afectan todas las hojas
**Solución:**
- Dashboard → Filter → Apply to Worksheets → All Using This Data Source
- Verificar que todas las hojas usan mismo data source

### Problema: Colores no son consistentes
**Solución:**
- Assign Colors manualmente a cada categoría
- Usar "Edit Colors" en cada gráfico
- Crear paleta personalizada en Preferences

## ⏱️ Tiempo Total Estimado
- Básico (KPIs + Dashboard simple): **60 minutos**
- Completo (con todos los dashboards): **120 minutos**
- Avanzado (con Story y optimización): **180 minutos**

## 📚 Recursos de Ayuda
- Guía completa: `docs/tableau_implementation_guide.md`
- Diccionario: `docs/data_dictionary.md`
- Insights: `docs/insights_estrategicos.md`

## 🎯 Resultado Final
Al completar esta guía tendrás:
- ✅ 10+ hojas de visualización
- ✅ 3 dashboards interactivos
- ✅ 1 story con narrativa
- ✅ Filtros y parámetros funcionales
- ✅ Archivo .twbx empaquetado y listo para entregar

---

**¡Éxito con tu implementación!** 🚀

Si encuentras problemas, consulta la documentación completa o revisa los tipos de datos en la fuente.
