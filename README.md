# Optix Netlogic C#
Aqui serão colocados os tutoriais de como programar em C# e exportar pro Optix via Netlogic
## Coisas que dá pra fazer com o Optix
- Criar vários estilos pré definidos de interface
- Criar objetos arrastáveis (exemplo aqui: https://github.com/FactoryTalk-Optix/FeaturesDemo2 - Tela: UI Design/Object Draggin)
- Criar um DialogBox padrão e alterar as variáveis definidas nele via código
## Definições
- `NodeID` é como se fosse o nó que possui vários elementos dentro dele (uma pasta, por exemplo)
- `AliasNode` é como se fosse a base pra criação de um elemento (por exemplo: você tem um modelo padrão de painel pra utilizar, então ele puxa automaticamente o modelo padrão da painel)
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
