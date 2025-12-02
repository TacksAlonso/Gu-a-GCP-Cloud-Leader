High latency: hace referencia a la distancia de conexion a donde esta almacenada la pagina o servicio, por ejemplo si tengo un servicio desplegado en London, y un usuario se conecta en España y otro en Chile, aunque ambos cuenten con buena conexion de internet, el usuario de chile presentara una lentitud mayor por la distancia de conexión.

Low availability: Es cuando de 4 servidores donde se despliega estos servicios, caen 2 por cualquier motivo, se tiene este estado, donde para la demanda se tiene pocos puntos de accesos disponibles.

Global Footprint: Huella mundial, creación de aplicaciones que pueden tener un despliegue internacional.

Adhere to government regulations: Normar regulatorias de cada pais.

Multiple data center: Es cuando tenemos más de un centro de datos, aunque este en su misma región
- Pro
    - Se puede operar en caso de que un centro de datos no funcione, el otro esta disponible
- Contras
    - El tema de latencia, sigue existiendo
    - En caso que en la region pase algo puede no se tenga conexion, debido a un desastre natural o algo por el estilo
Multiple region: Es cuanto tenemos más de un centro de datos en mpas de de una región 
- Pro
    - Se puede operar en caso de que un centro de datos no funcione, el otro esta disponible
    - La latencia puede mejorar aunque sigue dependiendo de la distribución de los centros de datos
- Contras
    - El tema de latencia, sigue existiendo

Hay que entender que este despliege de centros de datos no es barato, y accesible, por lo cual entra en juego los servicios en la nube.

Region: Lugar especifico, geograficamente y que agrupa varias zones, en GCP se tiene almenos 3 zonas dentro de una región

Zone: Es una subdivisión de la región y dentro de cada zona cuenta con almenos un Discrete Clusters o más que estan conectado por medio de una baja latencia.

Discrete Clusters: Centro de datos