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
            "in_spotify_playlists",
            "in_apple_playlists",
            "in_deezer_playlists"
                ],
        header:{
            "artist(s)_name": "Nome do Artista",
            "streams": "Mais Ouvidos",
            "in_spotify_playlists": "Spotify",
            "in_apple_playlists": "Apple",
            "in_deezer_playlists": "Deezer"
                },
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
const spotify = await FileAttachment("spotify.csv").csv({typed: true});
```

```js
import * as vega from "npm:vega";
import * as vegaLite from "npm:vega-lite";
import * as vegaLiteApi from "npm:vega-lite-api";

const vl = vegaLiteApi.register(vega, vegaLite);

function ex01(divWidth){
    return {
        spec: 
        {
            width: divWidth,
            data: {
                values: spotify
            },    
                "transform": [
                {
                    "window": [{
                    "op": "rank",
                    "as": "rank"           
                }],
                    "sort": [{ "field": "Mais Ouvidos", "order": "descending" }]
                }, {
                    "filter": "datum.Mais Ouvidos <= 5"
                }]
        }
    };
}



function ex02(divWidth) {
    return {
        spec: {
                width: divWidth,
                data: {
                    values: spotify
                },
                mark: {
                    "type": "bar",
                    "size": 10
                },
                "encoding": {
                    "y": {
                        "field": "artist(s)_name", 
                        "type": "ordinal", 
                        "sort": "-x",
                        "title": "Playlist do Spotify",
                    },
                    "x":{
                        "aggregate": "count",
                        "field": "in_spotify_playlists",
                        "title": "Playlist do Spotify",
                    }
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

