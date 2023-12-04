# GTFS-CuencaSimulation
En el GTFS de Cuenca tendremos los siguientes archivos:
![image](https://github.com/AnaMarcillo/GTFS-CuencaSimulation/assets/138828744/f28e2862-44cf-4f61-be65-cada64989ff1)

Una observación aquí fue que el archivo calendar_dates.txt no existía en el archivo comprimido original, este fue construido manualmente.
Según la documentación de GTFS de sumo (https://sumo.dlr.de/docs/Tutorials/GTFS.html)
Se necesitan al menos los siguientes archivos para convertir el archivo GTFS a una simulación de SUMO:
- routes.txt 
- stops.txt
- stop_times.txt
- trips.txt
- calendar.txt
- calendar_dates.txt
Por esta razón era importante generar el archivo calendar_dates.txt
El siguiente paso fue generar los siguientes archivos:
- pt_vtypes.xml
- gtfs_pt_stops.add.xml
- gtfs_pt_vehicles.add.xml

Que son necesarios para la simulacion. Para esto, se ejecuto desde una ventana del CMD el siguiente comando:

python "ruta del archivo gtfs2pt.py" -n cuenca_sumo.net.xml --gtfs "Nombre del gtfs.zip" --date 20231006 --modes bus --vtype-output pt_vtypes.xml

Cabe destacar que para ejecutar este comando primero se debe instalar la libreria de eclipse (pip install eclipse-sumo)

Adicionalmente, para que la simulación funcione se necesita tener una red prediseñada en donde se pueda ejecutar la simulación. En caso de ya tener la red, simplemente es necesario correr el comando.
En este caso el archivo "cuenca_sumo.net.xml" utilizada en el comando anterior fue construida de la siguiente manera:
Se descargó un archivo .osm de Ecuador de GEOFABRIK (https://download.geofabrik.de/south-america.html), el archivo puede ser manipulado con la aplicación Netedit de Sumo o con osmosis (https://github.com/openstreetmap/osmosis), se trabajará con osmosis, ya que se conocen los límites del fragmento del mapa del Ecuador que queremos usar para la simulación. El siguiente comando fue utilizado desde el CMD:
osmosis --read-xml ecuador-latest.osm --bounding-box left=-79.1311 bottom=-3.0363 right=-78.8551 top=-2.7548 --write-xml cuenca.osm

Donde left=-79.1311 bottom=-3.0363 right=-78.8551 top=-2.7548 son los límites establecidos para la extracción del la red, para conocer estos límites, es sencillo obtenerlos desde el la página de Open Street Map, cuando seleccionamos la opcion exportar y Seleccionar manualmente un área diferente, salen los límites. Ejemplo:
![image](https://github.com/AnaMarcillo/GTFS-CuencaSimulation/assets/138828744/541e9580-acc2-4885-b39c-79162930935d)

Una vez que obtenemos el archivo cuenca.osm del paso anterior, usaremos la herramienta netconvert desde la línea de comandos para extraer nuestra red:
netconvert --osm-files=cuenca.osm --output-file=cuenca_sumo.net.xml

Cuando ya tenemos los archivos:
- pt_vtypes.xml
- gtfs_pt_stops.add.xml
- gtfs_pt_vehicles.add.xml
- cuenca_sumo.net.xml (Red prediseñada)
Podemos correr la simulación utilzando el siguiente comando:
sumo-gui -n cuenca_sumo.net.xmll --additional pt_vtypes.xml,gtfs_pt_stops.add.xml,gtfs_pt_vehicles.add.xml

# Errores

En caso de aparecer el siguiente error:
![image](https://github.com/AnaMarcillo/GTFS-CuencaSimulation/assets/138828744/5a6ec4c2-bef2-4261-b7fe-1fad7228dc64)

Significa que los id's tienen que estar en un formato hexadecimal encerrados entre comillas ("") y la conversión agregó algunos caracteres de más, esto se repite a lo largo de todo el documento "gtfs_pt_vehicles.add.xml", para solucionar este problema simplemente se tiene que reemplazar los caracteres '(' y ',)' por comillas dobles o simples, esto se puede hacer con un buscar y reemplazar desde cualquier editor de texto.

Los archivos se encuentran en:
https://drive.google.com/drive/folders/1Evu4plSBjqK0Al40snzEA2mdEYQQcfse?usp=sharing



# GTFS-CuencaSimulation

En el GTFS de Cuenca tendremos los siguientes archivos:
!image

Una observación aquí fue que el archivo `calendar_dates.txt` no existía en el archivo comprimido original, este fue construido manualmente.

Según la documentación de GTFS de sumo (https://sumo.dlr.de/docs/Tutorials/GTFS.html), se necesitan al menos los siguientes archivos para convertir el archivo GTFS a una simulación de SUMO:
- `routes.txt`
- `stops.txt`
- `stop_times.txt`
- `trips.txt`
- `calendar.txt`
- `calendar_dates.txt`

Por esta razón era importante generar el archivo `calendar_dates.txt`.

El siguiente paso fue generar los siguientes archivos:
- `pt_vtypes.xml`
- `gtfs_pt_stops.add.xml`
- `gtfs_pt_vehicles.add.xml`

Que son necesarios para la simulación. Para esto, se ejecutó desde una ventana del CMD el siguiente comando:

```bash
python "ruta del archivo gtfs2pt.py" -n cuenca_sumo.net.xml --gtfs "Nombre del gtfs.zip" --date 20231006 --modes bus --vtype-output pt_vtypes.xml

Cabe destacar que para ejecutar este comando primero se debe instalar la librería de eclipse (pip install eclipse-sumo).

Adicionalmente, para que la simulación funcione se necesita tener una red prediseñada en donde se pueda ejecutar la simulación. En caso de ya tener la red, simplemente es necesario correr el comando.

En este caso el archivo cuenca_sumo.net.xml utilizado en el comando anterior fue construido de la siguiente manera:

Se descargó un archivo .osm de Ecuador de GEOFABRIK (https://download.geofabrik.de/south-america.html), el archivo puede ser manipulado con la aplicación Netedit de Sumo o con osmosis (https://github.com/openstreetmap/osmosis). Se trabajará con osmosis, ya que se conocen los límites del fragmento del mapa del Ecuador que queremos usar para la simulación. El siguiente comando fue utilizado desde el CMD:

osmosis --read-xml ecuador-latest.osm --bounding-box left=-79.1311 bottom=-3.0363 right=-78.8551 top=-2.7548 --write-xml cuenca.osm

Donde left=-79.1311 bottom=-3.0363 right=-78.8551 top=-2.7548 son los límites establecidos para la extracción de la red. Para conocer estos límites, es sencillo obtenerlos desde la página de Open Street Map, cuando seleccionamos la opción exportar y “Seleccionar manualmente un área diferente”, salen los límites. Ejemplo: !image

Una vez que obtenemos el archivo cuenca.osm del paso anterior, usaremos la herramienta netconvert desde la línea de comandos para extraer nuestra red:

netconvert --osm-files=cuenca.osm --output-file=cuenca_sumo.net.xml

Cuando ya tenemos los archivos:

pt_vtypes.xml
gtfs_pt_stops.add.xml
gtfs_pt_vehicles.add.xml
cuenca_sumo.net.xml (Red prediseñada)
Podemos correr la simulación utilizando el siguiente comando:

sumo-gui -n cuenca_sumo.net.xml --additional pt_vtypes.xml,gtfs_pt_stops.add.xml,gtfs_pt_vehicles.add.xml

Errores
En caso de aparecer el siguiente error: !image

Significa que los id’s tienen que estar en un formato hexadecimal encerrados entre comillas (“”) y la conversión agregó algunos caracteres de más. Esto se repite a lo largo de todo el documento gtfs_pt_vehicles.add.xml. Para solucionar este problema simplemente se tiene que reemplazar los caracteres ‘(’ y ‘,)’ por comillas dobles o simples. Esto se puede hacer con un buscar y reemplazar desde cualquier editor de texto.

Los archivos se encuentran en: Google Drive


