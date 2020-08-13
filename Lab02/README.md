
# Lab02 - Data Flow & Mensagens

## Tarefa sobre Components em Java

No diretório abaixo é possivel acessar a tarefa que foi desempenhada para entender a conceito e utilização de componentes em java:
~~~
└── notebook   <- arquivo do notebook
~~~
[Abrir o arquivo Jupyter Notebook](https://github.com/ronagalvao/Laboratorios/tree/master/Lab02/notebooks/components-01-catalog.ipynb)

# Data Flow e Componentes (parte 2)

## Tarefa Web Components 1

Crie quatro botões com rótulos `Mundo`, `Brasil P`, `Brasil E` e `Bahia` que, ao serem clicados, publiquem notícias nos seguintes tópicos (conteúdo a sua escolha):
* `noticia/mundo/politica`
* `noticia/brasil/politica`
* `noticia/brasil/esporte`
* `noticia/bahia/esporte`

O segundo nível do tópico indica a região da notícia e o terceiro o assunto. Associe a cada tópico o texto de uma mensagem de sua criação.

Crie três personagens (`doctor`, `nurse` e `patient`) usando o `<dcc-lively-talk>`. Cada um deles deve mostrar seletivamente (em seu balão) notícias publicadas pelos botões, conforme os seguintes critérios:
* `doctor` - mostra notícias sobre política (independentemente de região);
* `nurse` - mostra notícias cuja região é o Brasil (independentemente do assunto);
* `patient` - mostra todas as notícias.


### Concepção dos Componentes Web

_Para visualizar os componentes utilize o ambiente [DCC Playground](https://santanche.github.io/component2learn/labs/02-data-flow_messages/notebooks/messages/dccs/playground/)._

~~~html
<dcc-trigger id="mundo_politica" 
   label="Mundo" 
   action="noticia/mundo/politica" 
   value="<p>O candidato democrata à Presidência dos EUA, Joe Biden, anunciou na 
             terça-feira (11/08) quem será sua companheira de chapa na disputa com 
             Donald Trump no pleito de novembro.
          </p>
           <p>Kamala Harris, senadora pela 
             Califórnia, foi escolhida em uma lista que tinha estimado 13 nomes de 
             mulheres, incluindo pesos-pesados, como a senadora e ex-pré-candidata 
             Elizabeth Warren. <a href='https://www.bbc.com/portuguese/internacional- 
             53745981' target='blank'>Ler mais...</a>">
         </p>">
</dcc-trigger>

<dcc-trigger id="brasil_politica" 
   label="Brasil P" 
   action="noticia/brasil/politica" 
   value="<p><b>‘Debandada’: Por que auxiliares de Paulo Guedes estão abandonando o 
                 governo Bolsonaro?</b></p>
          <p><a href='https://www.bbc.com/portuguese/brasil-53754781' 
                      target='blank'>Matéria completa...</a</p>">
</dcc-trigger>

<dcc-trigger id="brasil_esporte" 
   label="Brasil E" 
   action="noticia/brasil/esporte" 
   value="<p><b>Acompanhe a tabela e os jogos do Brasileirão 2020...</b></p>
          <p><a href='https://www.uol.com.br/esporte/futebol/campeonatos/brasileirao/' 
                      target='blank'>Click aqui...</a</p>">
</dcc-trigger>

<dcc-trigger id="bahia" 
   label="Bahia" 
   action="noticia/bahia/esporte" 
   value="<p><b>Ultimas noticias sobre esportes na Bahia...</b></p>
          <p><a href='https://www.bahianoticias.com.br/esportes/' 
                      target='blank'>Click aqui...</a</p>">
</dcc-trigger>

<dcc-lively-talk 
   id="doctor"
   duration="1s"
   character="doctor"
   speech="<i>Notícias sobre política do Brasil e no Mundo:</i>">
  <subscribe-dcc topic="noticia/+/politica"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
   id="nurse"
   duration="2s"
   character="nurse"
   speech="<i>Notícias sobre o Brasil:</i>">
   <subscribe-dcc topic="noticia/brasil/+"></subscribe-dcc>
   <subscribe-dcc topic="noticia/bahia/esporte"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
   id="patient"
   duration="3s"
   character="patient"
   speech="<i>Todas as notícias, você encontra aqui:</i>">
   <subscribe-dcc topic="noticia/#"></subscribe-dcc>
</dcc-lively-talk>
~~~

---

## Tarefa Web Components 2

Crie dois componentes RSS usando o `<dcc-rss>` que assinem os canais:
  * canal 1 (ciência): https://www.wired.com/category/science/feed
  * canal 2 (design): https://www.wired.com/category/design/feed

Crie um agregador de mensagens usando o `<dcc-aggregator>` para notícias de ciência.

Crie três personagens (`doctor`, `nurse` e `patient`) usando o `<dcc-lively-talk>`. Cada um deles deve mostrar seletivamente (em seu balão) RSSs ou agregados, conforme os seguintes critérios:
* `doctor` - mostra notícias agregadas de ciências;
* `nurse` - mostra notícias de ciências;
* `patient` - mostra notícias de design.


### Concepção dos Componentes RSS Web 

_Para visualizar os componentes utilize o ambiente [DCC Playground](https://santanche.github.io/component2learn/labs/02-data-flow_messages/notebooks/messages/dccs/playground/)._

~~~html
<dcc-trigger label="Noticias <- clique aqui" action="next/rss"> 
</dcc-trigger>

<dcc-rss source="https://www.wired.com/category/science/feed" publish="rss/science">
  <subscribe-dcc topic="next/rss" role="step"></subscribe-dcc>
</dcc-rss>

<dcc-rss source="https://www.wired.com/category/design/feed" publish="rss/design">
  <subscribe-dcc topic="next/rss" role="step"></subscribe-dcc>
</dcc-rss>

<dcc-aggregator publish="aggregate/science" quantity="5">
  <subscribe-dcc topic="rss/science"></subscribe-dcc>
</dcc-aggregator>

<dcc-lively-talk 
    id="doctor"
    character="doctor"
    speech="<i>Lista de notícias sobre ciência:</i>">
  <subscribe-dcc topic="aggregate/science"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="nurse"
    character="nurse"
    speech="<i>Notícia sobre ciência:</i>">
  <subscribe-dcc topic="rss/science"></subscribe-dcc>
</dcc-lively-talk>

<dcc-lively-talk 
    id="patient"
    character="patient"
    speech="<i>Notícia sobre design:</i>">
  <subscribe-dcc topic="rss/design"></subscribe-dcc>
</dcc-lively-talk>
~~~

---
