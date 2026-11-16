# webscrapping-ejercicio
Entrega T2 del Grupo 13 del taller de web scraping (PUCP). Reúne las actividades de las clases 2 a 5 (APIs, endpoints ocultos, BeautifulSoup) y un proyecto final que extrae el pronóstico meteorológico diario de Lima desde la API pública de Open-Meteo y lo analiza con pandas.

Integrantes: Xiomara Diaz, Mariana Gomez y Luis Martinez.

Herramienta

Python, escrito como notebook de Google Colab (el .py es la exportación automática). Librerías:

Librería	Uso
requests	Peticiones HTTP a APIs y páginas
pandas	Tablas (DataFrame) con los datos extraídos
matplotlib	Gráficos
beautifulsoup4	Lectura del HTML de books.toscrape.com
lxml	Se instala junto con beautifulsoup4; el código usa el parser html.parser
Cómo correrlo

El archivo contiene comandos de Colab (!pip install, !curl) y display(), así que no corre con python t2_grupo_13.py: da error de sintaxis. Opciones:

Google Colab (recomendado): abre el notebook original (el enlace está en el encabezado del archivo) o sube el .py como notebook, y ejecuta las celdas en orden.
Jupyter local: pega el código en un notebook y quita o adapta las líneas !pip y !curl.

No necesita archivos de entrada ni claves de API. Sí necesita conexión a internet, porque todo se descarga en vivo.

Contenido por clase
Sección	Fuente	Qué hace
Clase 2	API del BCRP (series PD04637PD compra y PD04638PD venta)	Trae el tipo de cambio de compra de los últimos 15 días; define obtener_serie_bcrp y limpiar_tabla_bcrp y grafica el tipo de cambio de venta del último año (365 días)
Clase 3	scrapethissite.com (endpoint AJAX)	Recorre los años 2010 a 2015 con pausas de 1 s e imprime cuántas películas trae cada uno
	BVL (dataondemand.bvl.com.pe)	Consulta un endpoint de cotización diaria (VOLCABC1) como ejemplo del portal asignado
Reto clase 3	Urbania (/rplis-api/postings)	Documenta un endpoint oculto de búsqueda de departamentos en venta; el servidor respondió 403
Clase 4	books.toscrape.com	Extrae título y precio del tercer libro; arma tu_tabla con los 40 libros de las páginas 1 y 2 (título, precio en libras, valoración)
Clase 5	Firecrawl	Solo trae el enunciado de la actividad; no tiene código
Proyecto final	Open-Meteo (api.open-meteo.com/v1/forecast)	Extrae el pronóstico diario de Lima (temperatura máxima, mínima y lluvia), lo guarda en df_clima y grafica las temperaturas
Proyecto final: justificación

Se usa el Escalón 1 (API oficial pública) porque Open-Meteo no requiere llaves ni registro, entrega los datos ya estructurados y es la opción más barata y legítima para obtener variables climáticas actualizadas. Esa justificación está en una celda markdown al inicio del proyecto, como pide el criterio de evaluación.

Salidas

El script no guarda archivos: todo sale en pantalla (impresiones, tablas y gráficos). Como las consultas usan date.today() y pronósticos en vivo, los resultados cambian cada vez que se ejecuta.

Reglas éticas del taller

El encabezado recuerda cinco reglas: respetar robots.txt, preferir la API oficial, no recolectar datos personales, hacer pausas entre peticiones y usar un User-Agent honesto. El código aplica pausas con time.sleep(1) y un User-Agent identificado en las consultas al BCRP y a la BVL.

Observaciones sobre el código
Cookies en el !curl de Urbania: esa celda incluye cookies y tokens de una sesión real del navegador (cf_clearance, JSESSIONID, sessionId, etc.). Bórralos antes de compartir o subir el notebook a GitHub o a un repositorio.
Urbania: el servidor ya respondió 403 a la petición simple. Los intentos siguientes usan cabeceras que no corresponden (un Referer de scrapethissite, X-Requested-With) y un User-Agent de navegador, lo que choca con la regla del User-Agent honesto. Lo prudente es dejar esa parte solo como documentación del endpoint.
Verificación de robots.txt: en el BCRP y en Open-Meteo, el código agrega /robots.txt al final de la URL del endpoint, no a la raíz del dominio. Para que la comprobación sea válida, debe ir sobre el dominio (por ejemplo https://api.open-meteo.com/robots.txt).
Datos personales en el notebook: el User-Agent de la clase 2 incluye un correo institucional y el inicio del archivo lista los códigos de estudiante; conviene revisarlos antes de publicarlo.
URL de la BVL: lleva una fecha fija (today=2026-08-31); cámbiala para otra consulta.
Detalles menores: en el markdown del proyecto, el endpoint aparece cortado (.../v1/forecas); en el código está bien escrito. StringIO se importa pero no se usa.
