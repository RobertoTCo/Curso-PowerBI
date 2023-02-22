# Curso-PowerBI
Datos, Ejercicios y Presentación Curso PowerBI Dextro

¡Bienvenidos! En este repositorio podéis encontrar un .doc con el contenido formativo del curso. También
disponéis de la presentación que se usará para comenzar el curso.

Los dos días de formación se dividirán en lo siguiente:

## Martes 21/02

1. Veremos una breve introducción a PowerBI, consejos para trabajar con datos y algunos ejemplos de informes.

2. Daremos un pequeño vistazo a PowerBI Desktop.

2. Haremos un ejercicio para aprender cómo cargar y preparar datos en un report. Podéis encontrar los
datos en un .csv en la carpeta Ejercicio 1 de este repositorio.

## Miércoles 22/02

1. Exploraremos PowerBI Desktop de forma más extensa.

2. Haréis de manera autónoma un ejercicio para preparar una dashboard. Podéis encontrar 3 tablas en el archivo
.xlsx en la carpeta Ejercicio 2 de este repositorio. A continuación tenéis algunos consejos para el ejercicio.

## Instalación PowerBI Desktop

La aplicación de escritorio se puede descargar de manera gratuita en <a href="https://powerbi.microsoft.com/es-es/desktop/">la página oficial de PowerBI</a>.
Recomendable instalarlo en español (los nombres de los elementos y objetos cambian). El curso está preparado en español.

## Tipos de acceso a datos

### 1. Importar datos
PowerBI carga los datos desde la fuente (local o remota) y convierte en un dataset que se guarda en el modelo.

Para mostrar cambios en los datos originales, requiere actualizar los datos desde el modelo de PowerBI (Tabla -> Actualizar datos). 
También se puede especificar un calendario de actualizaciones periodicas.

Importante: Cuando se actualiza los datos, se está creando 2 copias del mismo dataset (mucho consumo!). PowerBI mantiene la copia antigua para queries y distintas acciones que trabajan con el dataset. Esta copia no se elimina hasta que no se termina la actualización.


## Ejercicio 1

Podéis encontrar el archivo .csv "HPI_editado" que usaremos en la carpeta `Ejercicio 1`. 
Esta tabla muestra una serie de índices calculados para el precio de viviendas a nivel nacional y estatal en USA desde 1975 hasta 2022.

Haremos los siguientes pasos el día 1. Pero en caso de que necesitéis revisarlos más adelante, aquí están por orden:

### Cargar el archivo delimitado por comas.

1. Obtener datos -> Texto o csv. Seleccionar 'HPI_editado'.
2. Transformar datos.

### Preparamos los datos

1. Esta tabla tiene formato internacional. Los decimales están separados por punto. Eliminamos tipo cambiado (panel a la derecha).
2.	Filtramos `level` por "Estados" y `hpi_type` por "Tradicional". ¡Hay que seleccionar "Cargar más" antes de hacer el filtrado!
3. Comprobamos si hay valores faltantes (NA, NULL o blanco en cada filtro de columna).
4. Movemos la columna `quarter_1` (arrastramos) para situarla antes que `quarter_2`.
5. Anulamos dinamización de las columnas `quarter_1`,`quarter_2`,`quarter_3` y `quarter_4`.
6. Cambiamos nombres de las columnas `Atributo` por "Quarter", `Valor` por "Index".
7. En la columna `Quarter` reemplazamos valores "quarter_" por "" (en blanco). Así nos quedamos solo con el número.
8. Hay un NA escondido. En columna `Index` remplazamos valor "NA" por "" (en blanco). 
9. Cambiar columna `Index` de texto a decimal. Cambiar tipo -> Usar configuración regional -> Seleccionar "Inglés (Estados Unidos)".

### Editar consulta por errores

1. Reemplazar `place_id` para "Indiana". 

= Table.ReplaceValue(#"Valor reemplazado",each [place_id],each if [place_name] = "Illinois" then "IL" else [place_id],Replacer.ReplaceText,{"place_id"})

2. En `HPI_flavor` filtrar por "purchase-only".

### Crear nuevas columnas en la query
1. Creamos columna "Year - Q" seleccionando ambas columnas, y en la pestaña "Agregar columna" buscamos "Combinar columna".
   En "separador" podemos elegir Personalizada y escribir " - ". En nombre escribimos "Year - Q".


## Consejos Ejercicio 2.

Podéis encontrar el ejemplo del ejercicio 2 en <a href="https://community.powerbi.com/t5/Data-Stories-Gallery/IT-HELPDESK-DASHBOARD/m-p/3040804">este Data Story template de PowerBI</a>. Los imágenes no coincidirán, porque los datos no son iguales.

### Descripción de las tablas

- Clientes: está formada por Nombre de los usuario, Jerarquía, País donde trabajan, Género
- Tickets_apertura: ID de los tickets, fecha de apertura, OwnerName = Trabajador encargado, RequestorName = usuario/cliente, País del cliente, 
             Tipo de petición, Categoría de la ayuda, Status = Cerrado o abierto, Prioridad
- Tickets_cierre: ID de los tickets, Fecha de Cierre, OwnerName = Trabajador encargado, Status (Cerrado), Satisfacción del cliente, Nº días para cerrar.

### Consejos

1. En la carpeta `Ejercicio 2` tenéis un archivo .pbix (powerBI) con la plantilla para el reporte preparada y un excel (.xslx) con las tablas.

2. ¡Recordar revisar las tablas! Hay que especificar que cada columna sea del tipo de variable correcto.

3. ¡Cuidado con la variable género!. Está codificada. 0: Male, 1: Female

4. Para mostrar los días que han pasado desde que se abrió un ticket (`Days Open`) podeís crear una nueva columna
   con el siguiente código: " Date.From(DateTime.LocalNow()) - [OpenDate]"  (Columna OpenDate->Insertar). 
 Lo veremos juntos!
 
 5. Para crear el gráfico de área con tickets cerrados y abiertos hay que crear dos medidas rápidas. 
 
     a. Closed: Medida rápida -> Cálculo -> Valor filtrado: Valor base = `TicketsID` (Recuento), Filtro = `Status` (Closed)
  
     b. Open: Medida rápida -> Cálculo -> Valor filtrado: Valor base = `TicketsID` (Recuento), Filtro = `Status` (Open y Closed)
 
 Lo veremos juntos!

