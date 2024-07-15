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
