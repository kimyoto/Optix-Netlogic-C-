# Optix Netlogic C#
Aqui serão colocados os tutoriais de como programar em C# e exportar pro Optix via Netlogic
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
> É necessário instanciar o botão pra alterar as propriedades dele </br>
Também é necessário setar o método criado (MudarCorBotao) a algum evento (por exemplo, o click do botão)
