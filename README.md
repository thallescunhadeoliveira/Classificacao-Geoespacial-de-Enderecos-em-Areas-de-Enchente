# Levantamento de Localizações Afetadas pelas Enchentes na Região Metropolitana de Porto Alegre
# Objetivo:
Neste repositório trago como buscar a localização através de uma lista de endereços e como consultar quais pontos estão dentro ou próximos de uma área

<div align=center>
  <img src="https://github.com/thallescunhadeoliveira/Levantamento-de-Localiza-es-Afetadas-pelas-Enchentes-POA-/blob/main/Supermercados%20Porto%20Alegre.jpg" alt="pontos-geolocalizacao" width=75% >
</div>

# Motivação:
Com as enchentes no Sul em maio de 2024 e a situação catastrófica, os dados podem salvar vidas e ajudar grupos e o poder público com previsibilidade e informação sobre áreas alagadas.

Nesse sentido, quero compartilhar esse repositório de informações geográficas sobre a tragédia no Rio Grande do Sul, mantido pela UFRGS (tinyurl.com/sitemapas).

Dentre os dados disponíveis, temos um mapeamento de possíveis áreas alagadas pelas chuvas feito por geoprocessamento de satélite e que está disponível para consulta e download.

Esses dados podem ser úteis de inúmeras formas e gostaria de compartilhar uma forma simples de conseguir plotar esse gráfico no Power BI, classificando uma lista de endereços para mapear se foram atingidas pelas enchentes ou não, o que pode ajudar na tomada de decisão em diversos tipos de cenário.

# Preparando os dados:

🌎 Acesse o link (https://www.google.com/maps/d/viewer?) para ter acesso ao mapa no Google Earth. Aqui você pode baixar o arquivo no formato KML.

⚙️ Acesse mapshaper.org e converta o arquivo em GeoJson (.json). 

👥 Levante uma lista de endereços do que deseja utilizar para consulta. No caso desse repositório, uso como exemplo uma lista de supermercados de Porto Alegre encontrada na internet (https://www.tiendeo.com.br/Lojas/porto-alegre/supermercados#google_vignette)

# Classificando a lista de endereços:

📌 Tendo uma lista de endereços ou CEPs, é necessário encontrar as coordenadas geográficas (latitude, longitude) para cada ponto. Uma maneira de fazer isso é consultando o endereço usando a API pública do geopy com o módulo Nominatim, que usa os dados do Open Street Map. Passando uma string com o endereço, ele irá retornar as coordenadas dos seus registros.

📋 Com os dados de geolocalização em mãos, precisamos classificar esses pontos como (a) dentro da área afetada, (b) fora da área porém próximo, e (c) distante da área. Para isso, podemos consultar se as coordenadas estão dentro do "multipolígono" no arquivo que baixamos. Importando o arquivo KML e usando a API do opengis, é possível construir uma lista de polígonos referente as áreas de alagamento e iterar com a lista de pontos de geolocalização classificando entre aqueles dentro da área, fora porém até 500 metros, ou em áreas seguras.

🗺️ Com essa classificação e coordenadas, basta importar os dados no Power BI. Recomendo a extensão gratuita do IconMap, que permite importar mapas personalizados, passando uma URL pública com os dados GeoJson, que podem ser publicadas via repositório GitHub (mais detalhes nesse tutorial https://www.youtube.com/watch?v=0OjejZnEt1g). Com isso, basta preencher os campos "Category" com a granularidade que precisa (algum campo como Nome ou ID), campos de latitude e longitude (sumarizar pela média) e em "Size", escolher o campo para definir o tamanho de bolha no mapa.
Obs: Caso queira uma URL de um arquivo GeoJson das regiões alagadas para colocar no IconMap, pode usar essa URL desse repositório(https://raw.githubusercontent.com/thallescunhadeoliveira/Levantamento-de-Localiza-es-Afetadas-pelas-Enchentes-POA-/main/Mapeamento%20Areas%20Alagadas%20Rio%20Grande%20do%20Sul%20(GeoJson).json)

☑️ Com isso, você terá uma lista de registros (seja de voluntários, pessoas, clientes, estabelecimentos etc) que foram atingidos, potencialmente atingidos ou que estão em áreas próximas.
Como exemplo, busquei endereços de supermercados de Porto Alegre disponíveis na internet.

# Arquivos

🐍 "Classificando Localizações de Acordo com uma Área.ipynb" - Arquivo Jupyter Notebook com o código para extrair latitude e longitude com base em um endereço e consultar se essas coordenadas estão dentro ou próximas de uma área.

🛒 "Supermercados Porto Alegre.xlsx" - Um arquivo no formato do Microsoft Excel com dados de endereços de supermercados encontrados através desse site (https://www.tiendeo.com.br/Lojas/porto-alegre/supermercados#google_vignette).

🌐 "Mapeamento Areas Alagadas Rio Grande do Sul.json" - Arquivo em formato GeoJson com as coordenadas das áreas possivelmente alagadas extraído desse mapa da UFRGS (https://www.google.com/maps/d/viewer)

