**Grupo SGS España**

**IT (Information Technology)**

**Estudio Viabilidad del Sistema**

CBE Automatización documentación i+D+i

v.3

28/08/2019

> Proprietary and Confidential - SGS Internal Use Only

Origen del documento

|                     |          |
| ------------------- | -------- |
| Autor               | División |
| Francisco Belinchón | IT       |

Historial de cambios

|         |            |                     |         |
| ------- | ---------- | ------------------- | ------- |
| Versión | Fecha      | Autor               | Cambios |
| V3      | 28/08/2019 | Francisco Belinchón |         |
|         |            |                     |         |

Revisión y Aprobación

|          |        |       |       |
| -------- | ------ | ----- | ----- |
| División | Nombre | Fecha | Firma |
|          |        |       |       |
|          |        |       |       |

Distribución

|          |        |              |        |
| -------- | ------ | ------------ | ------ |
| División | Nombre | Localización | Acción |
|          |        |              |        |
|          |        |              |        |
|          |        |              |        |
|          |        |              |        |

Índice

[1. INTRODUCCIÓN 4](#introducción)

[1.1 Objeto 4](#objeto)

[1.2 Alcance 4](#alcance)

[1.3 Áreas afectadas 4](#áreas-afectadas)

[2. Descripción de la situación actual 4](#descripción-de-la-situación-actual)

[3. REQUISITOS – características del nuevo sistema 4](#requisitos-características-del-nuevo-sistema)

[3.1 Requisitos funcionales 4](#requisitos-funcionales)

[3.1.1 Descripción general 4](#descripción-general)

[3.1.2 acceso a la aplicación 4](#acceso-a-la-aplicación)

[3.1.3 Diseño técnico de las plantillas Word. 4](#diseño-técnico-de-las-plantillas-word.)

[3.1.4 Restricciones definidas. 5](#restricciones-definidas.)

[3.1.5 opciones de configuración (tablas auxiliares) 6](#opciones-de-configuración)

[3.2 Requisitos Operativos 6](#requisitos-operativos)

[4. AnÁLISIS DE RIESGOS 6](#análisis-de-riesgos)

[5. ESTIMACION DE TIEMPOS y VALORACION ECONOMICA 7](#estimacion-de-tiempos-y-valoracion-economica)

[5.1 Desarrollo de la aplicación 7](#desarrollo-de-la-aplicación)

#   
INTRODUCCIÓN

##  Objeto

> Diseñar una aplicación que genere el formato oficial en XML a partir de plantillas Word para adjuntarlo directamente en el organismo oficial correspondiente.

##  Alcance

> Se creará una aplicación Web donde se podrán subir las plantillas rellenas con la información específica a cada trabajo.
> 
> La aplicación devolverá el XML con la estructura correcta para subirlo a la web del organismo oficial correspondiente.
> 
> Se han definido cuatro plantillas diferentes de trabajo.

##  Áreas afectadas

> CBE

# Descripción de la situación actual

> Actualmente se produce un proceso manual donde el evaluador rellena la información del fichero Word en un pdf oficial. Este pdf genera el fichero XML final.
> 
> El fichero generado tiene que ser tratado para solucionar problemas de codificación de caracteres.

# REQUISITOS – características del nuevo sistema

##  Requisitos funcionales

### Descripción general

Se va a desarrollar una aplicación web donde los usuarios puedan subir los ficheros Word cumplimentados y se obtendrá automáticamente el fichero XML con el formato oficial correcto. El fichero XML se valida con el esquema oficial para asegurar que el formato es el correcto.

No se almacenará ni el Word ni el XML generado.

Se han definido cuatro tipos de plantillas.

Se tomarán estas cuatro plantillas como base para generar las nuevas plantillas que tendrán las etiquetas asignadas a cada uno de los campos tratables del fichero. En base a estos datos obtendremos la información incorporada por el usuario en el fichero Word que sube a la aplicación.

La cuarta plantilla corresponde con el formato C eliminando el apartado **“4.0 Evaluación económica del proyecto”** y el punto **“5.2. ANÁLISIS DE LOS GASTOS”.**

### acceso a la aplicación

Se accede a la aplicación mediante usuario y contraseña. Existen tres tipos de perfiles.

  - Administrador general: puede dar de alta nuevos usuarios.

  - Perfil gestor: Este perfil puede generar los XML pero no puede crear o modificar usuarios.

### Diseño técnico de las plantillas Word.

Para poder tratar la información de los documentos Word se van a generar etiquetas en aquellos campos que el evaluador tiene que introducir información. El resto del documento será estático y no se podrá modificar.

Para desarrollar estas plantillas nos basaremos en las plantillas proporcionadas por el negocio. Es importante definir bien estas plantillas porque posteriormente no se podrá realizar cambios en el diseño (solamente se podrán realizar cambios sencillos en el texto fijo).

Los evaluadores utilizarán estas plantillas para rellenar la información del trabajo en cuestión. Al subir el fichero Word cumplimentado, la aplicación leerá los valores asociados a las etiquetas que hemos definido y generará el fichero XML final con la estructura correcta.

El negocio ha proporcionado los cuatro ficheros de esquema que deben cumplir los documentos XML generados.

### Restricciones definidas.

El fichero XML tiene que estar codificado como iso-8859-15. Estos son los caracteres permitidos.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2020-03-02-SGS_PLT_ESTUDIO-VIABILIDAD_CBEiDi_280819/media/image1.png)

En cuanto a las restricciones de la propia entrada de datos se definen los siguientes.

  - En el apartado 3 el porcentaje de desviación debe ser número real con dos decimales

  - En proyectos plurianuales la calificación recibida debe tener valor si el nº de expediente de Informe motivado está marcado.

El campo Organismo emisor debe estar vacío (no dejar meter nada).

Si hay algún valor en un campo se deben rellenar el resto (excepto Organismo emisor)

Los valores posibles de calificación recibida son: “I+D”,”IT”,”I+D+I”,”DESFAVORABLE”,”ANULADO”,”DESISTIDO” o “N/C”

<table>
<tbody>
<tr class="odd">
<td><strong>En proyectos plurianuales, consignar los informes motivados solicitados/emitidos en ejercicios anteriores.<sup>(3)</sup></strong></td>
</tr>
<tr class="even">
<td>Si dicho proyecto ha sido certificado en anualidades anteriores por cualquier entidad certificadora, pero no se han solicitado/emitido Informes motivados MITYC/MICINN/MINECO, se procederá a rellenar la totalidad de este documento como si fuera un informe de contenido y 1ª ejecución con el proyecto ya iniciado.</td>
</tr>
<tr class="odd">
<td><table>
<tbody>
<tr class="odd">
<td><strong>Ejercicio fiscal</strong></td>
<td><p><strong>Organismo</strong></p>
<p><strong>emisor</strong></p></td>
<td><strong>Nº de expediente de Informe Motivado</strong></td>
<td><p><strong>Fecha de</strong></p>
<p><strong>emisión</strong></p></td>
<td><strong>Calificación recibida</strong></td>
</tr>
<tr class="even">
<td>2019</td>
<td></td>
<td>☒</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>2020</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

  - Para Proyectos en cooperación.
    
      - Por cada fila se deben rellenar todos los campos

|                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Para proyectos en cooperación<sup>(4)</sup>, relacionar las entidades que han cooperado en el proyecto<sup>(3)</sup>, incluyendo la entidad solicitante en primer lugar, y de ellas, los informes motivados que, en su caso, hayan solicitado para el ejercicio fiscal objeto de evaluación.** |
|                                                                                                                                                                                                                                                                                                  |

<table>
<tbody>
<tr class="odd">
<td><strong>Nº</strong></td>
<td><strong>Razón Social</strong></td>
<td><strong>NIF<sup>(1)</sup></strong></td>
<td><p><strong>nº de Expediente</strong></p>
<p><strong>de Informe Motivado</strong></p></td>
</tr>
<tr class="even">
<td></td>
<td>Razon1</td>
<td>4324</td>
<td>3432432</td>
</tr>
<tr class="odd">
<td></td>
<td>Razon24343543</td>
<td>4545</td>
<td>435435</td>
</tr>
<tr class="even">
<td></td>
<td>45435</td>
<td>44444</td>
<td>444444</td>
</tr>
</tbody>
</table>

  - Campo “Título de la tabla “Planificación de las actividades del proyecto” del apartado “2.3 actividades del proyecto” tiene un máximo de 100 caracteres.

  - Campo “Título de la tabla “Actividades necesarias para el proyecto” del apartado “2.3 actividades del proyecto” tiene un máximo de 100 caracteres.

  - En Los siguientes campos se produce una validación de párrafo. Se puede escribir todo lo que se quiera, pero en párrafos inferiores a 1100 caracteres. Los párrafos se separan por retornos de carro y salto de linea, es decir que entre dos retornos de carro y salto de línea solo se pueden escribir 1100 caracteres. La composición del texto de los campos debería quedar de la siguiente manera

Ejemplo:

CRLF (Retorno de Carro y Salto de Linea)

“párrafo de hasta 1100 caracteres”+CRLF

CRLF

“párrafo de hasta 1100 caracteres”+CRLF

CRLF

“párrafo de hasta 1100 caracteres”+CRLF

…

Los campos a los que aplica esta restricción son los siguientes.

  - En el apartado “**Consignar cualquier otra consideración de tipo general que se considere oportuna para definir el proyecto o relativa al mismo.”**

  - En el apartado “**Consignar cualquier otra consideración de tipo general que se considere oportuna para definir el proyecto o relativa al mismo.”**

  - En el apartado “**Objetivo científico-tecnológico del proyecto.”**

  - En el apartado “**Estado del arte del proyecto. Referencias empleadas.”**

  - En el apartado “***Descripción y objetivos*”**

  - En el apartado “**Estado de ejecución global del proyecto.”**

  - En el apartado “**Idoneidad de las colaboraciones externas.”**

  - En el apartado “**Idoneidad de otras partidas de gasto.”**

### opciones de configuración 

  - **Perfiles de usuario**.

> Esta opción no tendrá una ventana de mantenimiento, pero existirá en Base de datos, conteniendo los distintos perfiles de acceso a la aplicación. Se manejarán los siguientes:

  - Administrador: será la persona que se encargue de gestionar el acceso para otros usuarios de la compañía. Además, podrá generar también los ficheros XML

  - Gestor: Este perfil puede generar los ficheros XML.

<!-- end list -->

  - Mantenimiento de **Usuarios**.

> Contendrá los usuarios que tienen acceso a la aplicación, así como el perfil de acceso de cada usuario.
> 
> El administrador de la aplicación será el que se encargue de dar acceso a otros usuarios.

### Generación de ficheros XML.

El usuario subirá el Word rellenando una de las cuatro plantillas definidas (las plantillas preparadas con las etiquetas). Con la información de este fichero Word se genera el fichero XML según el esquema correspondiente y las restricciones definidas.

No se almacena ni el fichero Word ni el XML generado. Solamente llevaremos una tabla para poder contabilizar el número de operaciones realizada por el usuario. Se almacena el código de usuario y la fecha (siempre que el XML se haya generado correctamente). Esto no permitirá en un futuro contabilizar las operaciones realizadas por un usuario en concreto. En esta versión solamente almacenamos la información. Será necesario realizar una ampliación de la aplicación si queremos desarrollar una pantalla para realizar estas consultas.

### 

##  Requisitos Operativos

> Se desarrollará el proyecto en base a la plantilla de SGS. Se utiliza .Net Framework 4.X

# AnÁLISIS DE RIESGOS

> El desarrollo se basa en las tres plantillas proporcionadas por el negocio. Si se produce un cambio en las plantillas será necesario realizar modificaciones en la aplicación, principalmente si se produce algún cambio en la salida XML.
> 
> El coste de la actualización dependerá de la importancia de los cambios.

# ESTIMACION DE TIEMPOS y VALORACION ECONOMICA

## Desarrollo de la aplicación

*Desglose de tareas y estimación de costes del proyecto. El coste total es de 9.400 €*

| **Fase**                 | **días** | **precio** | **total**   |
| ------------------------ | -------- | ---------- | ----------- |
| Análisis                 | 3        | 350        | 1.050 €     |
| Desarrollo               | 20       | 300        | 6.000 €     |
| Gestión proyecto         | 3        | 350        | 1.050 €     |
| Pruebas de entorno       | 2        | 300        | 600 €       |
| Estudio de viabilidad IT | 2        | 350        | 700 €       |
|                          |          | **Total**  | **9.400 €** |
