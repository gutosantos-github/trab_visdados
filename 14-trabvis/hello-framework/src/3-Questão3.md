---
theme: dashboard
title: 3 - Questão 3
toc: true
---

<style>
    body, div, p, li, ol { max-width: none; }
</style>


# 3 - Questão 3

---
```js
/*
const dataset = await FileAttachment("spotify.csv").csv({typed: true});
view(Inputs.table(dataset));
*/
```

## Colunas Correlacionadas
```js
//const selection = view(Inputs.table(dataset, {required: false}));
const dataset = await FileAttachment("spotify.csv").csv({typed: true});

const selection = view(Inputs.table(dataset, 
        {
        columns:[ 
            "artist(s)_name",
            "streams",
            "released_year",
            "in_spotify_playlists",
            "in_apple_playlists",
            "in_deezer_playlists"
                ],/*
        header:{
            "artist(s)_name": "Nome do Artista",
            "streams": "Mais Ouvidos",
            "in_spotify_playlists": "Playlist do Spotify",
            "in_apple_playlists": "Playlist da Apple",
            "in_deezer_playlists": "Playlist da Deezer"
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
        <h2 class="title"> Top 10 Musicas</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${ vl.render(ex01(divWidth - 200)) }
        </div>
    </div>
    <div id="ex02" class="card grid-colspan-2">
        <h2> Gráfico 2</h2>
        <div style="width: 100%; margin-top: 15px;">
            ${ vl.render(ex02(divWidth - 55)) }
        </div>
    </div>
</div>

<!--Tamanho dos cards. Caso vcs usem cards de multiplos tamanhos, 
    será necessário criar um generator para cada classe de card.
-->
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
            "transform": [{
                "filter":{ 
                    "field": "in_spotify_playlists", 
                    "range": [50, 100]},
                }],
            "mark": {
                "type":"line",
                "point":"true",
                "clipe":"true"
            },
            "encoding":{
                "x":{
                    "aggregate":"average", 
                    "timeUnit":"year", 
                    "field":"released_year",
                    "type":"temporal"
                },
                "y":{
                    "aggregate":"average", 
                    "field":"in_spotify_playlists", 
                    "type":"quantitative"
                },
                "color": {"field": "artist(s)_name", "type": "nominal"},
                "groupby": ["artist(s)_name"]
            }
        }
    }
}

function ex02(divWidth) {
    return {
        spec: {
            width: divWidth,
            data: {
                values: spotify
            },
            "transform": [{
                "filter":{ 
                    "field": "in_spotify_playlists", 
                    "range": [50, 100]},
                }],
            "mark": {
                "type":"line",
                "point":"true",
                "clipe":"true"
            },
            "encoding":{
                "x":{
                    "timeUnit":"year", 
                    "field":"released_year",
                    "type":"temporal"
                },
                "y":{
                    "aggregate":"mean", 
                    "field":"in_spotify_playlists", 
                    "type":"quantitative"
                },
                "color": {"field": "artist(s)_name", "type": "nominal"}
            }
        }
    }
}


```

## Análise
Você deve responder cada pergunta formulada no enunciado com base nas visualizações construídas.  
Utilize essa área para esta finalidade.

### Perguntas 
3) Discuta as diferenças entre as plataformas (Spotify, Deezer, Apple Music e Shazam)?

(a) Um conjunto de visualizações;

(b) Uma discussão sobre as razões que motivaram a escolha das visualização desenvolvidas, e;

(c) Uma análise das informações que podem ser obtidas com a interpretação da visualização.

