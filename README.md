# Curso-PowerBI
Datos, Ejercicios y Presentación Curso PowerBI Dextro

¡Bienvenidos! Los dos días de formación se dividirán en lo siguiente:

## Martes 21/02

1. Veremos una breve introducción a PowerBI, cómo podemos trabajar con datos y algunos ejemplos.

2. Daremos un pequeño vistazo a PowerBI Desktop.

2. Haremos un ejercicio para aprender cómo cargar y preparar datos en un report. Podéis encontrar los
datos en un .csv en la carpeta Ejercicio 1 de este repositorio.

## Miércoles 22/02

1. Exploraremos PowerBI Desktop de forma más extensa.

2. Haréis de manera autónoma un ejercicio para preparar una dashboard. Podéis encontrar 3 tablas en el archivo
.xlsx en la carpeta Ejercicio 2 de este repositorio. A continuación tenéis algunos consejos para el ejercicio.

## Consejos Ejercicio 2.

Podéis encontrar el ejemplo del ejercicio 2 en <a href="https://community.powerbi.com/t5/Data-Stories-Gallery/IT-HELPDESK-DASHBOARD/m-p/3040804">este Data Story template de PowerBI</a>. Los imágenes no coincidirán, porque los datos no son iguales.

1. En la carpeta Ejercicio 2 tenéis un archivo .pbix (powerBI) con la plantilla para el reporte preparada.

2. ¡Recordar revisar las tablas! Hay que especificar que sean el tipo de variable correcto.

3. ¡Cuidado con la variable género. Está codificada. 0: Male, 1: Female

4. Para mostrar los días que han pasado desde que se abrió un ticket (Days Open) podeís crear una nueva columna
   con el siguiente código: " Date.From(DateTime.LocalNow()) - [OpenDate]"  (Columna OpenDate->Insertar). 
 Lo veremos juntos!
 
 5. Para crear el gráfico de área con tickets cerrados y abiertos hay que crear dos medidas rápidas. 
 
     a. Closed: Medida rápida -> Cálculo -> Valor filtrado: Valor base = TicketsID (Recuento), Filtro = Status (Closed)
  
     b. Open: Medida rápida -> Cálculo -> Valor filtrado: Valor base = TicketsID (Recuento), Filtro = Status (Open y Closed)
 
 Lo veremos juntos!

Descripción de las tablas:

- Clientes: está formada por Nombre de los usuarios, su jerarquía, país donde trabajan y género
- Tickets_apertura: ID de los tickets, fecha de apertura, OwnerName = Trabajador encargado, RequestorName = usuario/cliente, País del cliente, 
             Tipo de petición, Categoría de la ayuda, Status = Cerrado o abierto, Prioridad
- Tickets_cierre: ID de los tickets, Fecha de Cierre, OwnerName = Trabajador encargado, Status (Cerrado), Satisfacción del cliente, Nº días para cerrar.
