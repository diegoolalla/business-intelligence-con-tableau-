# business-intelligence-con-tableau-
Tarea business intelligence con tableau 
Caso Práctico: Easy Loans- Análisis de Préstamos
Introducción
Easy Loans es una empresa financiera que concede préstamos para la adquisición de
productos en diferentes establecimientos. Tu tarea consiste en analizar las operaciones
realizadas durante el ejercicio 2023 utilizando Tableau para extraer insights que apoyen
la toma de decisiones estratégicas. Se espera que, a través de este análisis, puedas
identificar patrones de comportamiento, evaluar la calidad de los préstamos y
proporcionar recomendaciones para mejorar la eficiencia de las operaciones
financieras. Además, deberás aplicar técnicas avanzadas de visualización y análisis
para resaltar las áreas de oportunidad en las operaciones de la empresa.
El propósito de este caso práctico es que desarrolles una comprensión profunda de los
datos de Easy Loans, identificando no solo patrones evidentes, sino también posibles
anomalías y áreas de mejora que puedan ser optimizadas para aumentar la eficiencia y
rentabilidad de las operaciones. Este ejercicio te permitirá poner en práctica habilidades
avanzadas de análisis de datos y visualización en Tableau, mejorando así tu capacidad
de presentar información clara y accionable a los stakeholders del negocio.
Page 2 of 15
Objetivos
● Desarrollar un modelo de datos en Tableau que permita conectar las fuentes de
información de manera eficiente y efectiva, asegurando una adecuada integridad
y calidad de los datos.
● Explorar y analizar datos clave de Easy Loans para identificar tendencias,
comportamientos significativos y posibles riesgos en las operaciones de
préstamo.
● Crear visualizaciones que aporten valor al negocio, que sean comprensibles,
impactantes y útiles para la toma de decisiones por parte de los directivos de
Easy Loans. Estas visualizaciones deben permitir identificar fácilmente tanto los
puntos fuertes como las áreas de mejora de las operaciones.
● Mejorar la experiencia de usuario en el dashboard para garantizar que sea fácil
de usar y permita una exploración efectiva de los datos. Debes asegurarte de
que el dashboard sea accesible incluso para aquellos que no tienen experiencia
técnica.
Instrucciones Generales
1. Uso de la Plataforma
○ Utiliza Tableau Desktop para el desarrollo de la tarea. Si no estás
familiarizado con Tableau, revisa los recursos disponibles en el Campus
Virtual
para aprender a conectar fuentes de datos, realizar
transformaciones básicas y crear visualizaciones de alto impacto.
Además, se recomienda que te familiarices con las mejores prácticas para
el diseño de dashboards efectivos.
○ Lafuente de datos está disponible en el archivo Easy Loans Operaciones
2023.xlsx. Realiza el modelado y la conexión adecuadamente,
asegurándote de que los datos estén correctamente relacionados y
filtrados para el análisis. Asegúrate de revisar los datos importados para
identificar posibles problemas de calidad, como valores nulos o
inconsistentes.
Page 3 of 15
Descripción de las Tablas y sus Columnas
Para ayudarte en el análisis, a continuación se presenta una descripción detallada de
cada una de las tablas disponibles en el archivo de datos:
Tabla: Orders
● order_id: Identificador único de cada orden.
● created_at: Fecha y hora en la que se creó la orden.
● status: Estado del préstamo (e.g., CLOSED).
● amount: Importe total
● merchant_id: Identificador único del comercio.
● country: País donde se realizó la orden.
Tabla: Refunds
● order_id: Identificador único de cada orden asociada con un reembolso.
● refunded_at: Fecha y hora en la que se realizó el reembolso.
● amount: Importe del reembolso realizado.
Tabla: Merchant
● merchant_id: Identificador único de cada comercio.
● name:Nombre del comercio.
Modelado de Datos (1 punto)
● Paso 1: Conecta Tableau con el archivo Easy Loans Operaciones 2023.xlsx.
Asegúrate de revisar los datos cargados para comprobar que todos los campos
se han importado correctamente. Esto incluye verificar tipos de datos y
relaciones entre tablas para evitar problemas durante el análisis.
● Paso 2: Crea un modelo de datos utilizando relaciones entre las tablas
disponibles. Define claramente las relaciones entre las tablas "orders",
"merchants" y "refunds".
● Paso 3: Filtra los datos para que solo se muestren las operaciones en tiendas
Page 4 of 15
europeas, excluyendo las operaciones en Marruecos.
● Paso 4: Selecciona la opción "Extraer" y genera la extracción del modelo de
datos. Guárdalo en formato .twbx, este paso es muy importante para
compartir tu trabajo correctamente
Exploración y Análisis de Datos (2 puntos)
● Crea los siguientes cálculos para facilitar el análisis. Asegúrate de entender el
propósito detrás de cada cálculo y cómo estos permiten obtener insights
específicos sobre las operaciones de Easy Loans:
1. Promedio: Calcula el precio medio de todos los préstamos. Utiliza este
valor para analizar cuáles son los niveles típicos de financiación y cómo
varían entre diferentes tipos de establecimientos y productos. Además,
identifica posibles desviaciones y explora qué factores podrían estar
influyendo en estos valores promedio.
2. Total Comercios: Realiza el conteo de todos los comercios. Este cálculo
te ayudará a identificar la cobertura y distribución de Easy Loans en el
mercado, lo que a su vez puede proporcionar insights sobre la penetración
de mercado y las oportunidades de expansión.
3. Máximo: Calcula el precio máximo de los préstamos. Identifica las
operaciones más significativas y analiza si presentan características
particulares, como un mayor riesgo de incumplimiento o una mayor
concentración en ciertos tipos de clientes o establecimientos.
4. Mínimo: Calcula el precio mínimo de los préstamos. Analiza las
operaciones de menor cuantía y evalúa si tienen un mayor riesgo de
incumplimiento.
5. Valor Acumulado: Calcula el importe acumulado de los préstamos
utilizando la función RUNNING SUM. Este valor permitirá evaluar la
evolución de las operaciones a lo largo del tiempo y detectar patrones de
crecimiento.
6. Promedio Total: Fija el precio medio de las operaciones utilizando la
función FIXED. Este cálculo será útil para comparar el promedio global
Page 5 of 15
con los promedios de diferentes segmentos, como categorías de
productos o regiones.
7. Total Reembolsos: Realiza el conteo de los reembolsos. Este indicador te
ayudará a entender el comportamiento de los clientes respecto a la
devolución de productos. Explica cómo se podrían implementar políticas
para reducir las devoluciones.
Parámetro "Valor Préstamo Mínimo"
Para mejorar la capacidad de análisis de los usuarios y proporcionar una
herramienta poderosa para la toma de decisiones, se debe crear un parámetro
que permita filtrar los préstamos por un valor mínimo definido por el usuario. A
continuación, se detalla el proceso y los beneficios de este enfoque.
1. Crear un Parámetro en Tableau:
○ En Tableau, ve al panel de Datos y selecciona la opción para crear un
nuevo parámetro.
○ Nombre del parámetro: Define un nombre descriptivo, como "Valor
Préstamo Mínimo".
○ Tipo de datos: Selecciona un tipo de datos numérico, ya que el valor
representará una cantidad monetaria.
○ Valor inicial: Establece un valor predeterminado, por ejemplo, 0, que los
usuarios pueden ajustar según sus necesidades.
2. Definir el Campo Calculado:
○ Crea un campo calculado que compare el importe del préstamo con el
valor del parámetro creado Amount>Valor Préstamo Mínimo
○ Este campo calculado se utilizará como un filtro adicional en todas las
visualizaciones del dashboard.
3. Aplicar el Filtro en las Visualizaciones:
○ Utiliza el campo calculado para filtrar las operaciones en cada una de
las visualizaciones. De este modo, sólo se mostrarán aquellas que
cumplen con el criterio del valor mínimo definido (asegúrate de solo
seleccionar el valor True).
Page 6 of 15
4. Utilización del Parámetro para Filtrar:
○ Agrega este parámetro al dashboard como un control interactivo para
los usuarios, permitiéndoles ajustar el valor mínimo de préstamo para
explorar diferentes segmentos de operaciones. No agregues el filtro al
dashboard, debes de incluir el parámetro.
5. Impacto del Filtro en las Visualizaciones:
○ Todas las visualizaciones del dashboard se actualizarán
automáticamente para reflejar solo aquellos préstamos que cumplen con
el criterio definido. Esto afecta directamente a gráficos, tablas y otros
elementos visuales, proporcionando una vista clara y específica de los
préstamos más relevantes.
○ Este filtro permite una exploración dinámica de los datos y ayuda a los
usuarios a identificar tendencias y patrones en los préstamos de diferentes
cuantías, dependiendo del valor seleccionado.
Desarrollo del Contenido (6 puntos)
Visualizaciones Requeridas: Asegúrate de que cada visualización sea clara, aporte
valor al análisis y esté alineada con los objetivos del negocio.
○ Tabla de KPIs: Incluye los campos "Valor Acumulado", "Promedio",
"Promedio Total", "Máximo", "Mínimo", "Total Comercios" y "Total
Devoluciones". Esta tabla debe proporcionar una visión general del
rendimiento de las operaciones. Sigue estos pasos para su creación:
■ Paso 1: Crea un nuevo dashboard en Tableau y selecciona los
campos "Valor Acumulado", "Promedio", "Promedio Total",
"Máximo", "Mínimo", "Total Comercios" y "Total Devoluciones".
■ Paso 2: Diseña una tabla con estos KPIs y asegúrate de que los
valores se calculen correctamente para cada uno.
■ Paso 3: Ajusta los formatos de los números para mejorar la
legibilidad, como agregar separadores de miles donde sea
necesario.
○ Mapa: Colorea los países según el "Promedio". Utiliza un gradiente de
Page 7 of 15
colores que permita identificar claramente los países con mayores y
menores promedios de préstamos. Sigue estos pasos para su creación:
■ Paso1:Arrastra el campo "País" a la vista de mapa en Tableau.
■ Paso 2: Añade el campo "Promedio" como una medida y utiliza un
gradiente de colores para resaltar los diferentes valores.
■ Paso 3: Ajusta el rango de colores para que los valores extremos
sean fácilmente distinguibles.
○ Gráfico de Áreas: Muestra la suma acumulada de las operaciones ("Valor
Acumulado") por día, coloreando cada área según el país. Sigue estos
pasos para su creación:
■ Paso 1: Arrastra el campo "Fecha de Creación" al eje X (creando
el atributo de DÍA) y el campo "Valor Acumulado" al eje Y.
■ Paso 2: Colorea cada área según el país utilizando el campo "País"
como diferenciador.
■ Paso 3: Ajusta los valores del eje Y para que la acumulación se
muestre de forma clara.
○ Desviación: Crea una vista de desviación para identificar qué operaciones
están por encima y cuáles están por debajo del promedio. Esta
visualización te permitirá evaluar rápidamente las operaciones que
destacan del promedio, ya sea positiva o negativamente. Para elaborar
esta visualización, sigue estos pasos:
■ Paso 1: Crea un campo calculado que determine si una operación
está por encima o por debajo del promedio. Utiliza la siguiente
fórmula en Tableau: Promedio-AVG(Promedio Total)
■ Paso 2: Agrega este campo calculado a la vista como una etiqueta
o color. Utiliza colores distintivos para resaltar operaciones por
encima (e.g., verde) y por debajo (e.g., gris) del promedio.
Asegúrate de elegir la opción de color escalado en 2 pasos y
ordenado.
Page 8 of 15
○ Filtros Globales: Añade filtros de "País", "Fecha de Creación" (rango de
fechas) y "Límite Préstamo Mínimo" (solo valores True) y asegúrate que
aplican a todas las visualizaciones. Sigue estos pasos para su creación:
■ Paso 1: Añade el filtro "País" para permitir a los usuarios filtrar las
visualizaciones según un país específico.
■ Paso 2: Añade el filtro "Fecha de Creación" como un rango de
fechas, permitiendo a los usuarios seleccionar períodos
específicos.
■ Paso 3: Añade el filtro "Límite Préstamo" para que solo se
muestren aquellos préstamos que cumplen con ciertos criterios.
■ Paso4:Aplicar a todas las visualizaciones del dashboard.
○ Dashboard Final: Integra todas las visualizaciones, filtros y el parámetro
en un dashboard completo. Sigue estos pasos para su integración:
■ Paso 1: Crea un nuevo dashboard en Tableau y arrastra cada una
de las visualizaciones creadas previamente.
■ Paso 2: Ajusta el layout para asegurar que todas las
visualizaciones sean claramente visibles y fáciles de interpretar.
■ Paso 3: Añade títulos y etiquetas para cada visualización para
mejorar la comprensión de los usuarios.
○ Acciones en el Dashboard: Configura una acción para que al hacer clic
en el mapa, se filtren las demás visualizaciones. Sigue estos pasos para
su configuración:
● Paso 1: Pulsa el icono del embudo para que el clic en el
mapa afecte a las demás visualizaciones del dashboard.
● Paso 2: Asegúrate de que la acción esté configurada de
manera que las visualizaciones restantes se actualicen
automáticamente cuando el usuario haga clic en un país.
Page 9 of 15
NOTA: Los valores mostrados en la visualización son ilustrativos, no se deben tomar como evidencia de la solución final.
Page 10 of 15
Diseño Alternativo y Experiencia de Usuario (1 punto)
De manera opcional puedes aplicar un diseño de dashboard personalizado que mejore
la experiencia de usuario. Puedes modificar la estética, mejorar la navegación o la
visualización de los datos para que sea más intuitivo y efectivo. Aquí tienes algunos
ejemplos para inspirarte, no es necesario que las repliques, el objetivo es que el
resultado sea lo más personal posible.
● Funcionalidades Extra: Añade funcionalidades avanzadas para mejorar la
experiencia y la interacción con el dashboard. Esto incluye la implementación de
selectores de medidas que permitan al usuario cambiar entre diferentes
métricas (como ventas, beneficio, etc.), acciones de dashboard para
profundizar en los datos a diferentes niveles o visualizaciones adicionales que
muestren datos complementarios y ofrezcan más perspectivas sobre las
operaciones de Easy Loans. Puedes integrar cualquier elemento o dashboard
extra si lo deseas.
Page 11 of 15
● Experiencia de Usuario y Diseño: Integra elementos de diseño que mejoren la
interacción y la experiencia visual del dashboard. Considera el uso de iconos
que permitan identificar rápidamente las distintas secciones del dashboard,
contenedores ocultables que permitan mostrar u ocultar secciones adicionales
según las necesidades del usuario (facilitando así una navegación más limpia y
eficiente), y un diseño personalizado que se alinee con la identidad visual de
Easy Loans.
Page 12 of 15
Bonus: Publicación en Cloud
Para obtener el bonus, deberás publicar el dashboard siguiendo una de las dos
opciones descritas a continuación. Es importante cumplir con todos los requisitos para
garantizar que la entrega sea válida y recibas la calificación adicional correspondiente.
Opción 1: Publicar en Tableau Cloud y Compartir con el Profesor
1. Publicación en Tableau Cloud:
○ Inicia sesión en Tableau Cloud.
○ Sube el dashboard que has creado asegurándote de seguir los pasos
para publicarlo correctamente. Asegúrate de que el título del dashboard
contenga tu nombre completo, para que sea fácilmente identificable por el
profesor.
○ Configura los permisos: una vez publicado, debes configurar los
permisos para que solo el profesor pueda acceder al dashboard. Esto
incluye establecer configuraciones de privacidad y compartir el dashboard
únicamente con el correo electrónico del profesor.
2. Evidencia de Publicación:
○ Captura de pantalla: Toma una captura de pantalla donde se pueda
visualizar claramente que el dashboard está publicado y los permisos
están correctamente configurados.
○ Enlace al Dashboard: Proporciona el enlace al dashboard publicado.
Este enlace debe ser comprobado por el profesor para confirmar la
correcta configuración de los permisos y la accesibilidad.
Opción 2: Publicar en Tableau Public
1. Publicación en Tableau Public:
○ Accede a Tableau Public y asegúrate de tener una cuenta activa. Si no
tienes una, deberás crearla.
Page 13 of 15
○ Publica el dashboard asegurándote de incluir tu nombre completo en el
título. Recuerda que, al ser una plataforma pública, cualquier persona
podrá visualizar el contenido.
2. Evidencia de Publicación:
○ Captura de pantalla: Al igual que en la opción anterior, toma una captura
de pantalla que muestre el dashboard publicado en Tableau Public con tu
nombre claramente visible.
○ Enlace al Dashboard: Proporciona el enlace al dashboard publicado para
que el profesor pueda revisarlo. Recuerda que el enlace debe ser
funcional y accesible sin restricciones.
Entrega
Formato de Entrega
● Archivo .twbx: El archivo debe entregarse en formato .twbx exclusivamente a
través del Campus Virtual. Es muy importante que se entregue en este formato
para garantizar que los datos puedan ser revisados correctamente por el profesor
y que las conexiones y configuraciones estén preservadas.
Instrucciones de Entrega
1. Archivo .twbx:
○ El archivo debe contener todas las visualizaciones y configuraciones
realizadas. Esto incluye todas las hojas de trabajo, dashboards y
configuraciones que hayas implementado para cumplir con los requisitos
del proyecto.
○ Antes de entregar el archivo, asegúrate de revisar que todas las
interacciones y filtros funcionan correctamente. Verifica que cada
elemento interactivo responde como se espera y que no haya errores en
la navegación entre visualizaciones.
2. Archivo .pdf: Captura de Pantalla con la Publicación en Cloud (para optar al
BONUS)
3. Plataforma de Entrega:
Page 14 of 15
○ Laentrega se realizará únicamente a través del Campus Virtual. No se
aceptarán entregas por otros medios como correo electrónico u otras
plataformas, ya que el Campus Virtual es la vía oficial para registrar la
entrega y asegurar la revisión del archivo.
Consideraciones Finales
● Revisión de Visualizaciones: Revisa cuidadosamente que todas las
visualizaciones se carguen sin problemas y que los filtros y acciones funcionen
como se espera. Asegúrate de que no haya errores de conexión a los datos y
que todas las funcionalidades sean accesibles y operativas.
● Entrega a Tiempo: La entrega fuera de plazo solo será aceptada si existen
motivos justificados debidamente acreditados y aprobados previamente por el
profesor. Esto implica que cualquier eventualidad debe ser comunicada con
antelación y aprobada para evitar inconvenientes.
● Pruebas Finales: Realiza pruebas finales antes de la entrega para confirmar que
el archivo se abre correctamente en otra computadora o entorno diferente al que
usaste para desarrollarlo. Esto garantizará que no haya problemas con las
configuraciones de las conexiones o la visualización de los datos.
