# Optix Netlogic C#
Aqui serão colocados os tutoriais de como programar em C# e exportar pro Optix via Netlogic
## Coisas que dá pra fazer com o Optix
- Criar vários estilos pré definidos de interface
- Criar objetos arrastáveis (exemplo aqui: https://github.com/FactoryTalk-Optix/FeaturesDemo2 - Tela: UI Design/Object Draggin)
- Criar um DialogBox padrão e alterar as variáveis definidas nele via código
## Definições
* Aliases ou `AliasNode` (são `NodeId` type) são referências que permitem apontar para outros objetos ou nós dentro do projeto de forma abstrata e dinâmica.
> Um alias funciona como uma referência indireta a um objeto ou nó. Em vez de usar o caminho completo para referenciar um objeto, você usa um alias, que aponta para esse caminho.
## Ideias
- Criar gráficos via código C#, salvar o gráfico como PDF e apresentar ele no Optix com o PDF Viewer nativo do Optix
- Criar gráficos na WEB com integraçaõ a banco de dados (WebBrowser)
## Como acessar os elementos do Optix
- https://github.com/FactoryTalk-Optix/NetLogic_CheatSheet/blob/main/pages/accessing-project-nodes.md#accessing-project-nodes
* Mais tutoriais: https://github.com/FactoryTalk-Optix/NetLogic_CheatSheet
## Criando um botão dinamicamente e manipulando as propriedades
`var newButton = InformationModel.Make<Button>("MyNewButton");`</br>
`newButton.Width = 100;`</br>
`newButton.Height = 50;`</br>
`newButton.Text = "Clique em mim";`</br>
### Definindo a cor de fundo
`newButton.BackgroundColor = Colors.SeaGreen;`</br>
### Adicionando o botão ao Panel1 já existente no Optix
`var panel = Project.Current.Get<Panel>("UI/Screens/Screen1/Panel1");`</br>
`panel.Add(newButton);`
## Alterando propriedades de um botão já existente no Optix
`[ExportMethod]` </br>
`public void MudarCorBotao(NodeId botao){` </br>
`var botaoOptix = InformationModel.Get<Button>(botao);` </br>
`botaoOptix.BackgroundColor = new Color(255, 0, 0, 0);}`
- É necessário instanciar o botão pra alterar as propriedades dele
- Também é necessário setar o método criado (MudarCorBotao) a algum evento (por exemplo, o click do botão)
- No método, é necessário selecionar o elemento que vai ser alterada a propriedade
![image](https://github.com/user-attachments/assets/b0c6d602-4c22-4f80-8315-3db767530b5b)
## Criar um timer via código (Periodic Task)
![image](https://github.com/user-attachments/assets/91ef76cf-9784-4afa-802c-b9f9ec703d66)
## Como importar variáveis e alterar o valor delas
![image](https://github.com/user-attachments/assets/59865ca9-7cb5-4d5a-9a08-4864818d2c91)
## Como importar um objeto com variáveis dentro delas e alterar o valor das variáveis
![image](https://github.com/user-attachments/assets/25b59f94-ed5c-4d22-a968-70b14ce6f216)
## Como criar elementos dinamicamente (via código) com base em modelos definidos no Optix e com NetLogic
Precisa existir o modelo no `Project view` do Optix com o evento MouseClick já selecionado para algum método dentro do NetLogic </br>

![image](https://github.com/user-attachments/assets/3f49170e-4cd7-450d-8759-a6fc1dfcc052) ![image](https://github.com/user-attachments/assets/c6c91fc9-9372-447e-b816-e846058e3598) </br>

Dentro do NetLogic (C#) é só preencher dentro do `.Make<>` o nome do modelo do elemento (btnStackedBarChart, por exemplo) e dar um nome pra ele: </br>

![image](https://github.com/user-attachments/assets/2b8a284c-c6c9-4350-92c1-d05886231282) </br>

> Também é necessário adicionar ele a algum painel para ser exibido
## Criar dinamicamente elementos (DialogBox, por exemplo) por evento MouseClick de botão criado dinamicamente (via código)
Para poder criar objetos via código no evento de MouseClick de um botão que foi criado via código, é necessário que o painel passe o valor NodeId dele pro input argument do botão que vai criar o novo objeto.

### Criação do painel
É necessário adicionar `Alias` para o painel criado clicando no `+` das propriedades do objeto. </br>

![image](https://github.com/user-attachments/assets/e7cfcb76-924f-465f-8d90-47fcfcfa5111)
> O nome do Alias pode ser qualquer um.

É necessário criar um link dinâmico entre o `Alias` (`NodeId`) e o atributo `NodeId` do painel. </br>

![image](https://github.com/user-attachments/assets/d481ea33-cdb7-4d9b-8b2e-946c04c4c3a3)

### Adicionando o botão de forma dinâmica no painel
É necessário criar um NetLogic dentro do painel. </br>

![image](https://github.com/user-attachments/assets/fd0d112c-fd99-4265-a2e5-724ec8693ec2) </br>

Um dos jeitos de adicionar é esse:

![image](https://github.com/user-attachments/assets/79c45a3a-c4b9-40ac-b525-56db63b16598)


### Criação do botão
É necessário criar um modelo padrão de botão para dentro do Project view e dentro dele criar um NetLogic. </br>

No evento MouseClick, selecionar o `método` criado no NetLogic para criar o objeto e criar um link dinâmico no `Input arguments` com o atributo `NodeId` do painel a partir de seu `Alias`:</br>

![image](https://github.com/user-attachments/assets/3426347d-00ab-4354-ae80-e1446e0c1e45) <br/>
![image](https://github.com/user-attachments/assets/043a7d0b-355a-4dd4-bae9-84303b9e20b4)

Configuração do NetLogic para importar o valor do painel e criar dentro dele o DialogBox: </br>

![image](https://github.com/user-attachments/assets/30f25f82-a178-4324-871b-83fa89334b58) </br>

> O modelo do objeto a ser criado precisa existir dentro do Optix pra funcionar
