---
toc: false
---

<style>

.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: var(--sans-serif);
  margin: 4rem 0 8rem;
  text-wrap: balance;
  text-align: center;
}

.hero h1 {
  margin: 2rem 0;
  max-width: none;
  font-size: 14vw;
  font-weight: 900;
  line-height: 1;
  background: linear-gradient(30deg, var(--theme-foreground-focus), currentColor);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero h2 {
  margin: 0;
  max-width: 34em;
  font-size: 20px;
  font-style: initial;
  font-weight: 500;
  line-height: 1.5;
  color: var(--theme-foreground-muted);
}

@media (min-width: 640px) {
  .hero h1 {
    font-size: 50px;
  }
}

</style>

<div class="hero">
    <h1>Trabalho de Visualização de Dados</h1>
    <h2>Curso de Visualização de Dados (SI & PGC - UFF)<br>Prof. Marcos Lage</h2>
     <h2><br>Alunos: Augusto Santos e Lucas Alexandre</h2>
</div>

---
# Objetivos do Trabalho:

O objetivo do trabalho é analisar o dataset Most Streamed Spotify Songs 2023 aplicando os conhecimentos obtidos durante as aulas de Visualização de dados. 

Dataset localizado no Kaggle:
https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023

```js
const dataset = FileAttachment("spotify.csv").csv({typed: true});
view(Inputs.table(dataset))
```
---
## Instruções gerais

Neste trabalho serão analisados, utilizando visualizações, o conjunto de dados fornecido no link acima. 

### Perguntas a serem respondidas, com análises:

1) Existe alguma característica que faz uma música ter mais chance de se tornar popular?

    (a) Um conjunto de visualizações;

    (b) Uma discussão sobre as razões que motivaram a escolha das visualização desenvolvidas, e;

    (c) Uma análise das informações que podem ser obtidas com a interpretação da visualização.

2) O conjunto das top 10 músicas e dos top 10 artistas varia muito se considerarmos apenas musicas lançadas no mesmo ano?

    (a) Um conjunto de visualizações;

    (b) Uma discussão sobre as razões que motivaram a escolha das visualização desenvolvidas, e;

    (c) Uma análise das informações que podem ser obtidas com a interpretação da visualização.

3) Discuta as diferenças entre as plataformas (Spotify, Deezer, Apple Music e Shazam)?

    (a) Um conjunto de visualizações;

    (b) Uma discussão sobre as razões que motivaram a escolha das visualização desenvolvidas, e;

    (c) Uma análise das informações que podem ser obtidas com a interpretação da visualização.

---
**Observações:**
1. Escreva sua argumentação de forma clara, direta e organizada. Sendo assim, evite respostas muito curtas ou textos longos demais.
2. Caso a sua argumentação dependa de interações ou parâmetro modificados pelo usuário na interface, é importante que você descreva os passos necessários para reporduzir sua análise.

### Design utilizados
Por fim, você deve justificar a escolha dos designs das visualizações construídas nos trabalhos.  
Utilize esta área para esta finalidade.

**Observações:**
1. Descreva quais marcadores e canais visuais foram utilizados.
2. Argumente se existe algum viés que pode ser causado pelo design escolhido.
3. Discuta sobre outros temas vistos em aula como separabilidade e discriminabilidade dos canais visuais.
---

## Mais informações a respeito do dataset:
 O conjunto de dados contém uma lista abrangente das músicas mais famosas de 2023 listadas no Spotify. O conjunto de dados oferece uma variedade de recursos além do que normalmente está disponível em conjuntos de dados semelhantes. Ele fornece informações sobre os atributos, popularidade e presença de cada música em várias plataformas musicais. O conjunto de dados inclui informações como nome da faixa, nome do(s) artista(s), data de lançamento, listas de reprodução e paradas do Spotify, estatísticas de streaming, presença do Apple Music, presença do Deezer, paradas do Shazam e vários recursos de áudio.

