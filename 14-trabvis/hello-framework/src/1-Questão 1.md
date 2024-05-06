---
theme: dashboard
title: 1 - Questão 1
toc: true
---

<style>
    body, div, p, li, ol { max-width: none; }
</style>

### Pergunta 1: 
<b>Existe alguma característica que faz uma música ter mais chance de se tornar popular?</b>

Para respondê-la, geramos oito scatter plots que com o objetivo de observar a relação da variável "Streams" com "Danceability", "Valence", "Energy", "Acousticness", "Instrumentalness", "Liveness", "Speechiness" e "BPM", respectivamente. Os gráficos que apresentam uma tendência mais forte, indicando características presentes em músicas populares são: "Streams X Danceability" e "Streams X Energy". O gráfico "Streams X Speechiness" apresenta também uma tendência, mas de forma inversa. 

Nos dois primeiros gráficos apontados é possível perceber que "Streams" (em bilhões) mostra uma tendência de aumento à medida que "Danceability" e "Energy" crescem. Quanto ao gráfico "Streams X Speechiness", percebe-se no gráfico que a maior parte dos pontos se concentram na parte esquerda, evidenciando que músicas com baixa "speechiness" têm um grande número de streams sendo, portanto, mais populares. Por outro lado, à medida que “speechiness” aumenta, há menos pontos, sugerindo que músicas com alta “speechiness” geralmente não são tão populares.

(a) Um conjunto de visualizações;
(b) Uma discussão sobre as razões que motivaram a escolha das visualização desenvolvidas, e;
(c) Uma análise das informações que podem ser obtidas com a interpretação da visualização.

## Colunas Correlacionadas
```js

const dataset = await FileAttachment("spotify.csv").csv({typed: true});
//view(Inputs.table(dataset));
//const selection = 
view(Inputs.table(dataset, 
        {
        columns:[ 
            "streams",
            "danceability_%",
            "valence_%",
            "energy_%",
            "acousticness_%",
            "instrumentalness_%",
            "liveness_%",
            "speechiness_%"
                ],
        /*header:{
            "artist(s)_name": "Nome do Artista",
            "streams": "Mais Ouvidos",
            "in_spotify_playlists": "Spotify",
            "in_apple_playlists": "Apple",
            "in_deezer_playlists": "Deezer"
                },*/
        sort: "streams", reverse: true
        }
    )
);
```
---
## Visualizações

<div class="grid grid-cols-2">
    <div id="ex01" class="card grid-colspan-2" >
        <h2 class="title"> Danceability X Streams</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${ vl.render(ex01(divWidth - 200)) }
        </div>
    </div>
    <div id="ex02" class="card grid-colspan-2">
        <h2> Energy x Streams</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${ vl.render(ex02(divWidth - 50)) }
        </div>
    </div>
        <div id="ex03" class="card grid-colspan-2">
        <h2> Gráfico 3</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${ vl.render(ex02(divWidth - 55)) }
        </div>
    </div>
</div>

<!--Tamanho dos cards. Caso vcs usem cards de multiplos tamanhos, 
    será necessário criar um generator para cada classe de card.
-->
---
```js
const divWidth = Generators.width(document.querySelector("#ex01"));
```
```js
//To load data in the browser, use FileAttachment:
//const spotify = await FileAttachment("spotify.csv").csv({typed: true});
```

```js
import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";

const vl = vegaLiteApi.register(vega, vegaLite);

const spotify = await FileAttachment("spotify.csv").csv({typed: true});


function ex01(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: spotify
            },
            "transform": [
                {"calculate": "datum.streams", "as": "streams in billions"}
                ],            
            "mark": {
                "type": "bar",
                "size": 10
            },
            "encoding": {
                "y": {
                    "field": "streams in billions",
                    "type": "quantitative"
                },
                "x": {
                    "field": "danceability_%",
                    "type": "quantitative"   
                }
            }
        }
    };
}

function ex02(divWidth){
    return{
        spec:{
            width: divWidth,
            data:{
                values: spotify
            },
            "transform": [
                {"calculate": "datum.streams", "as":"streams in billions"}
            ],
            "mark": {
                "type":"bar",
                "size": 50
            },
            "encoding":{
                "x":{
                    "bin": true, 
                    "field": "energy_%", 
                    "type":"ordinal"
                    },
                "y":{
                    "field": "streams in billions", 
                    "type":"quantitative", 
                    "aggregate": "count"}
            }
        }
    };
}

```



