# vusJsStudy

### Um resumo sobre o que aprendi fazendo esse projeto.

O VueJs é um framework javascript que foi feito para facilitar desenvolvimento da parte front-end da aplicação. Ele é um sistema reativo (Reactive System), que quer dizer que qualquer parâmetro que for trocado no arquivo vue será automaticamente trocado no front do projeto, sem a necessidade de atualização de página ou compilação do código. 

Quando falamos em página web, podemos notar que existem diversos elementos na página, como: header, buttons, banner, forms e etc. 

Cada elemento da página pode ser um componente diferente e independente, ou seja, cada componente tem o seu próprio código js, sue próprio HTML (conhecido como template no VueJs) e se necessário o seu próprio CSS. 

Esses elementos ficam dentro da pasta components/ do projeto e são instanciados através de import no componente que depende dele. 

A aplicação VueJs começa por uma div principal, que em nosso exemplo chamaremos de #app. A div #app é inserida dentro de um arquivo HTML 5 padrão. Esse arquivo chama index.html e ele fica dentro da pasta public/ do projeto. Podemos notar que ele está sozinho nessa pasta, não existindo nenhum arquivo .html com ele. Isso é devido ao projeto ser em VueJs, a possibilidade em que ele nós abre permite que a gente tenha apenas um arquivo HTML sendo o restante do código feito em .vue e .js ou .ts. 

O VueJs não é enviado para a produção, pois é feito a construção do projeto. Para construir ou "buildar" o seu projeto, acesse pelo terminal, vá na pasta raiz e execute o comando npm run build. Esse comando irá fazer a construção do projeto e você perceberá o surgimento da pasta dist/. Essa pasta que deve ser enviada para o ambiente de produção. Tenha atenção para não esquecer de executar o comando npm install, antes de "buildar" o projeto, porque existem dependências do node_modules que o projeto precisa para ser construído.

O arquivo mais.js é responsável por plugar a aplicação vue ao arquivo index.html está procurando. Por exemplo: Digamos que o arquivo index.html tem uma div principal cujo o id seja teste-projeto. Como é feita essa conexão? A conexão é feita através do main.ts que vai apontar para o arquivo raiz TesteProjeto.vue. O arquivo main pode ser encarado como o coração da aplicação é por ele que tudo vai começar. Esse arquivo tem a função de iniciar o core da aplicação, através dele serão chamados todos os componentes do projeto, que irão chamar outros componentes e assim sucessivamente. 

A questão que fica é: Como que esses componentes se comunicam? Como fazemos para transmitir um evento? O que seria um evento?

Vamos começar primeiro entendendo o que seria um evento. O evento seria uma forma de comunicação entre os componentes. Quando o usuário faz uma interação com a página, isso se traduz em um evento para aplicação, que vai captar a ligação que o usuário está tentando fazer e devolver a resposta dessa ligação. 

Temos então o conceito de bind (ligação). Quando queremos exibir uma imagem em nosso site, por exemplo, colocamos o path da imagem dentro da função data do arquivo .vue que está sendo chamado. Sendo assim, em vez de usarmos <img src=".image/path-da-imagem/foto.jpg">, podemos usar algo muito mais fácil, que seria a ligação do path da imagem  que seria a expressão dentro de data com o atributo src do HTML. O resultado ficaria da seguinte forma: <img :src="image".> ou <img v-bind:src="image">.


E quando a gente tem uma condição para exibir no front? Vamos supor que estamos fazendo um sistema para um consultório médico, em que ele vai mostrar no monitor da sala de espera quais são os médicos que estão livres e quais são os que estão ocupados. Fazendo o template do vue precisaríamos colocar duas divs condicionais, como: <div v-if="isFree">Médico livre para atendimento.</div><div v-else>Médico ocupado e em atendimento.</div> Para isso funcionar somente seria necessário colocar a expressão isFree dentro da função data, dizendo se isFree é true ou se é false. É importante lembrar que o v-if não precisa vir acompanhando de um v-else para funcionar. 


Além disso se a questão for apenas visibilidade podemos utilizar o v-show. No entanto é preciso tomar cuidado, porque o v-show apenas dá um display:none no elemento. Então se abrir o navegador para ver os elementos dos código, vai aparecer o dado no HTML mas escondido para visualização. 

A existência do v-for é para exibir uma lista de dados no front. O seu conceito é simples, digamos que temos a collection abaixo no data:
compras: [arroz, feijão, batata, frango]

Para exibir a collection "compras", teríamos apenas que utilizar um alias, que no caso pode ser "compra" para ficar mais fácil de entender e o resultado seria:
<ul>
    <li v-for="compra in compras">{{ compra }}</li>
</ul>  

Se a collection tiver variantes dentro dela, como: [ { marca: x; nome: arroz}, {marca: y; nome: feijão}, {marca: z; nome: batata}]
O resultado seria:
<ul>
    <li v-for="compra in compras">
          <p>{{ compra.marca }}</p>
          <p>{{ compra.nome }}</p>
    </li>
</ul>

Para lidar com eventos no vue usamos a diretriz v-on. Essa diretriz funciona como se a gente estivesse criando um ouvido ou escutador (listener) para aquele elemento. Assim esse elemento pode escutar os eventos, por exemplo v-on:click está ouvindo o evento de clique do mouse do usuário. Quando o usuário clicar em cima desse elemento, ele chamará uma ação. 

As diretrizes do vue podem ter "shorthands", que seriam abreviações. Por exemplo:
- o v-bind é igual a  :   
- o v-on é igual a @ 

Em questão de estilo do front podemos aplicar de duas formas. 
1) Usando o style
2) Usando a class
Além disso, nós conseguimos usar se for o caso, condicionais dentro dessas formas. 
Por exemplo, digamos que uma classe só deve ser aplicada se o médico estiver ocupado. O resultado seria:
<button :class="{ disableClass: !isFree }" :disabled="!isFree">Chamar médico</button>

Ou seja, se o médico não estiver livre será adicionada a classe disableClass ao elemento e o elemento será desabilitado.

Quando o objetivo é concatenar duas variáveis, podemos utilizar a propriedade computada, para isso precisamos criar a propriedade do escopo do script como "computed". Essa propriedade serve para retirar concatenação de variáveis do template do projeto.  Além do mais, as propriedades que foram computadas e criadas, só serão atualizada se alguma de suas variáveis forem editadas. Caso contrário ela permanece salva em cache e não existe a necessidade de refazer a concatenação toda vez que a página é renderizada.


Componentes. Tudo em uma página HTML pode ser um componente em VueJs. Por exemplo: em um sistema de cadastro de clientes, o botão Cadastrar por ser um componentes, o form pode ser um componente, a header do arquivo pode ser um componente, entre muitas outras coisas. Para exemplificar ainda melhor, o VueJs pode ser encarado como uma caixa de legos e cada componente equivale a uma peça que pode ser encaixada em outra. Um componente não precisa estar sozinho, ele pode ter componentes filhos (component child) dentro dele, que possuem outros componentes filhos. Com os componentes nós conseguimos encapsular código para reutilizar em vários lugares. 

Os componentes precisam se comunicar entre eles, pois cada um está em um arquivo separado. Para isso vamos precisar emitir para o componente parente que aquele evento esta acontecendo. Para fazer isso precisamos user o this.$emit, ou seja, estamos avisando o emissor daquele componente e ele precisa emitir uma informação para o componente pai. O componente pai vai precisar ter um listener que ouve a emissão do componente filho, por exemplo: Se o componente filho está emitindo this.$emit('add-invoice'), o componente pai vai ter um listener @add-invoice="addInvoice".
