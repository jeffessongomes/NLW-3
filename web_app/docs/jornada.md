# Dia 1
Primeiro passo preparar o ambiente:

Nodejs
Yarn

#bug seguindo as orientações do site do nwl deu um problema ao instalar o yarn.
usei as recomendações do site:
*install
sudo apt-get install yarn
*update
$ curl --compressed -o- -L https://yarnpkg.com/install.sh | bash

# Conceitos 
## SPA Single Page Application
Trocar conteúdos da tela em componentes sem precisar recarregar toda a pagina.
## React 
Construção de interfaces fluidas usando o conceito SPA.
## typescript
Superset :conjuto de ferramentas colocadas em cima do javascript.

# aula 1

## Criar projeto React:

name_my_app é literalmente um nome que você pode escolher para o app.

$ yarn create react-app web_app --template typescript

Limpando arquivos indesejados.
- readme 
- public/ todos exceto index.html (index.html tbm teve uma limpeza no arquivo =D)
-src/ todos exceto index.js e App.js (algumas modificações foram feitas)

Testando aplicação.
$ yarn start
### estrutura do projeto.
-web_app/
--public/
---index.html
--src/
---index.js
---App.js
---images/
----images.svg
---styles
----global.css
----pages/

Percebi que meu projeto não ficou em typescript  =D
Abri a documentação e achei meu erro =D 
-[documentação react](https://react-typescript-cheatsheet.netlify.app/docs/basic/setup)

## Conceitos React
ReactDom: Integração do react com a árvore de elementos do HTML(DOM)
Componentes: funções que retornam um html.
Intercace: descreve o tipo do objeto que a função usa. 

### Entendendo os arquivos 
index.tss  vai renderizar a page index.html, no nosso caso estamos colocando o App.ts dentro do index.ts.
App.ts - Nosso primeiro componente. =D

## Criandon layout do projeto (landing page)
Link com as infos https://www.notion.so/Layout-Happy-OmniStack-faac4d4d638343fe8bab627125a7557c
Pede pra exportar a ilustra_02, no meu figma a opção de export estava no menu lateral lá embaixo.
- Criaruma pasta images/ e salvar as imagens pedidas no video.
- Criar pasta styles/
-- criação do estilo global
Fonte do google fontes , numnito   600,700,800.
colocamos no index.html.
-- criação da pasta pages/
---crialçao do estilo landing

IMPORTANTE: todas importações devem ser feitas nos js dos componentes e não no index.html.

### povoando a page seguindo o figma
Dentro de app.ts criar wma div content-wrap, digite .content.wrap e se nao parecer sugestão use o ctrl+space =D

seguimos as isntruções do video, porém a div mais externa não esta ficando centralizada =z
instalando pacote de icones
$ yarn add react-icons    vem pacote pra porra.

Visualmente estava com uma aparecencia estranha devido ao tamanho da tela do meu pc.
adicionei algumas propriedades ao componente no arquivo landing.css. 

#landing-page .content-wrapper{
  max-height: 630px;   
 [abaixo detodos os estilos]
background-size: contain;
}

### Criando rotas
React router DOM
$ yarn add react-router-dom & yarn add @types/react-router-dom
Înstale também o @types do modulo para mostrar as dependncias na IDE
$ yarn add @types/react-router-dom

deu merda porque isntalei os modulos em niveis errados, salvei as pastas src e public,
recriei o projeto, e substitui as pastas.

agora com as rotas criadas, criamos as paginas como componentes e usamos o Link no lugar da tag <a>
para evitar recarregar toda a pag

para evitar avisos chatos comenta a linha anterior com //eslint-disable-next-line

# Dia 3 integração Back e Front.

## Página de mapas
Começamos implementando a adição de marcadores ao mapa, usando as ferramentas do leaflet-react e leaflet.
Trabalharemos na tela `OrphanageMaps.tsx`.
### usando marcadores de mapas
importar a classe que vai cuidar do marcador Marker, que será o nosso tag componente <Marker/>.
Ele tem um atributo "position" que é as coordenadas onde ele aparecerá. Funcionou tranquilo porém não apareceu o pin (icone de localização).
Para usar icones personalizados teremos que usar o modulo leaflete e criar um objeto para carregar o incone. Com isso basta customizar basta passar o atributo icon ainda no Marker.

para inserir a descrição no local do mapa, adicionamos ao marcador uma tag/componente PopUp, do proprio leafleat-react. A estilização desse box foi feita por css.

### css do icon

Não funcionou ainda. =D

## Implementação de navegação entre telas
As páginas novas foram baixadas do curso, apenas coloquei nas pastas do client e fiz a implementação das rotas.
- Importar as rotas no topo assim como as que ja existem.
- Descrever as rotas
- Alterar os liks nos botões criados.
## abstraindo componentes

O primeiro componente criado foi a sidebar,uma função que exporta um html que usa seu proprio css, muito legal!
separamos tudo em pastas nos respectivos diretorios.  src/style/components e src/componets. 

depois de refatorar os arquivos que continham o sidebar antigo, fui dado a opção de fazer um bodieplate do 
"Icone" do mapa, criamos uma pasta "utils" para deixar esse trecho de codigo que se repete, não é um coponente pois não tem html...

## conectando cliente e API.  (back e front)

Já vamos começar instalando a lib. axios.
$ yarn add axios

Uma das vantages dessa biblioteca é o fato dela encurta a url.  localhost:port é o '/' e pronto   =D

Criamos a pasta services e dentro dela a configuração da comonicação com a API.   api.ts

Basicamente é isso =D.   

## consumindo a api.


Agora vamos deixar os elementos das páginas dinamicos de acordo com os dados da api.
### começamos na tela do mapa.
usando o UseState e o UseEffects vamos fazer um hook e salvar os valores ou estados das variaveis da api.
O react nao guarda valores como o js tradicional, precisamos desses "estados" para ser mais eficiente.
Sempre que precisar alterar uma variavel que sera usada pelo componente é ideal usar estados.

```
const [array_de_estados, função_que_permite_editar_o_array] = userState()
exemplo: função_que_permite_editar_o_array([arry_atualizado]) 
```

criamos o estado e usamos a função map para percorrer o hook e criar os componentes markers.

testei criar outros orfanatos e o render funcionou tranquilo.

parei no tempo 00:47 do video. (metade)

### carregando pagina de orfanato.(usei o typora pra documentar)

https://typora.io/

requisição por ID na api funcionando, porém os dados estão vindo duplicados, como se tivesse alguma estrutura de repetição.
Até então parece que a Useeffects é chamada sempre que o [] (ultimo parametro da função) é alterado. no caso criamos o `paramns.id` pra isso.

Com a chamada funcionando vamos configurar a interface da imagem para corresponder com a view da api. Ou seja um array de imagens com dois parametros.

existem duas formas de setar a interface com um array

images : {
  params:tipo,
}[]

ou 
images : Array<{
  url : string,
}>

Tive um problema com a exibição das imagens na pagina, minha backend/src/view da api não adiconava o "Http://"
na URL o que gerou erro de "url schema". Resolvi apenas editando a view no backend para funcionar corretamente.

Para usar o if dentro do html fica assim:
a condição pode ser uma variavel, o '? abre o 'if' e o ':' abre o 'else'.

{ 'condição' ? "if_do" : "else_do" }

ainda não tratei a questão do boolean então vai ser sempre else.

adicionamos a funcionalidade de ver no google maps. bem simples usando uma new page pra buscar no prorio google maps a nossa localização e do orfanato.

em seguida criamos um novo state pra verificar qual imagem esta selecionada no "carrocel" de imagens.

## Criando orphanatos (POST)

- Criar a função que pega a coordenada clicada no map.(handleMapClick)
- Adiconar o atributo onClick ao <Map>
- criar um useState pra posição.

Vamos criar varios states para cada campo do formulário, porque? sei lá.

input e text area criados.
funcão onSubmit= HandleSubmit criada pra impedir que envia automaticamente.

criamos a ultima variavel state e setamos ela como bolean para o botão de finais de semana.

editamos o botao de upload image e transformamos em um tag <label  htmlfor="id do input"  >
que aponta para um <input id="id do input ">

tive um bug pra esconder esse emput, que não sei como foin resolvido, tentei de tudo, depois ele so sumiu.
agora que temos a opção deupar fotos, vamos lidar com os files.
Criamos a função "handlerImage". 

As mesmas imagens enviadas pra api, serão usadas pro preUpload da criação do orfanato. Como isso?
Foram criadas algumas funções que até ja achei um bug que não permite voce adicionar mais imagens, ele sobre escreve.

Depois eu volto aqui e comento como foi feito e como resolvi o bug.

Em tese agora temos todos os campos do forms pronto para o submite, porém ainda precisamos criar o forms de acordo com o suportado pela API.

para isso vamos usar o FormData()

FormData implementado com sucesso, tive alguns bugs devido a uma variavel está escrita errada "longetude" deveria ser longitude, tive que editar praticamente todos os  arquivos tanto no front quanto no back.

encontrei o erro no log network do f12.






