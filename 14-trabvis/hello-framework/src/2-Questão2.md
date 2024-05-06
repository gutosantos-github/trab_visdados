---
theme: dashboard
title: 2 - Questão 2
toc: true
---

<style>
    body, div, p, li, ol { max-width: none; }
</style>

# 2 - Pergunta 2:

O conjunto das top 10 músicas e dos top 10 artistas varia muito se considerarmos apenas musicas lançadas no mesmo ano?

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
            "track_name",
            "artist(s)_name",
            "streams"
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
import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";

const vl = vegaLiteApi.register(vega, vegaLite);
const spotify = await FileAttachment("spotify.csv").csv({typed: true});

function ex01(divWidth) {
   return {
        spec: {
            width: divWidth,
            padding: 15,   
            data: {
                values: spotify
            },
            "mark": {
                "type": "bar",
                "size": 30,
            },
            "transform": 
           [{
                "aggregate": 
                [{
                    "field": ["streams"],
                    "op": "sum", 
                    "as": "Stream_total",
                }],
                "groupby": ["artist(s)_name"],
            },
            {
                "filter": "datum.Stream_total >= 5000000000"
            }],      
                   
            "encoding": {
                "x": {
                    "field": ["artist(s)_name"],
                    "type": "nominal",
                    "aggregate": "artist(s)_name",
                    "sort": {
                        "field": "Stream_total",
                        "order": "descending"
                    },        
                    "title": "Nome(s) do(s) Cantor(es)",                                  
                },
                "y": {
                   "field": ["Stream_total"],
                    "type": "quantitative",
                    "title": "Total de Streams",    
                }
            }
        }
    }
}
```