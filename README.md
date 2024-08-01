Programação realizada dentro do [[FactoryTalk Optix]].

## Criando um botão dinamicamente e manipulando as propriedades

``` C#
var newButton = InformationModel.Make<Button>("MyNewButton");
newButton.Width = 100;
newButton.Height = 50;
newButton.Text = "Clique em mim";
```

### Definindo a cor de fundo

``` C#
newButton.BackgroundColor = Colors.SeaGreen;
```

## Adicionando o botão ao Panel1 já existente no Optix
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

É necessário criar um link dinâmico entre o `Alias` (`NodeId`) e o atributo `NodeId` do painel.

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

## Como criar um objeto com variáveis via código, preencher os valores e exibir os valores
![image](https://github.com/user-attachments/assets/a3130820-2ba4-4847-9c35-763db91c27e2)

## Como obter os objetos dentro de algum elemento e acessar suas variáveis
![image](https://github.com/user-attachments/assets/04f4f294-e679-4a76-b479-c2e33a515904)

## Como pegar o valor da seleção de uma ComboBox e fazer uma ação (switch)
![image](https://github.com/user-attachments/assets/988c6dc7-457e-4d43-a192-23ba50f8e11c)

## Como importar valor de TAGs de CLPs via Optix

``` C#
        // Instancia a estação (CLP conectado)
        var station = Project.Current.Get<FTOptix.RAEtherNetIP.Station>("CommDrivers/RAEtherNet_IPDriver1/RAEtherNet_IPStation1");

        // Importa a TAG
        var tagProducao = station.Get<FTOptix.CommunicationDriver.Tag>("Tags/Controller Tags/outLED").RemoteRead();

        // Transforma o valor da tag em texto pra conseguir comparar
        var status = tagProducao.Value.ToString();

        if (status == "True")
        {
            Log.Info("Produção iniciada em " + DateTime.Now.ToString());
        }
        else
        {
            Log.Info("Parada iniciada em " + DateTime.Now.ToString());
        }
```

## Lista de comandos SQL dentro do Optix

https://github.com/FactoryTalk-Optix/NetLogic_CheatSheet/blob/main/pages/database-interaction.md

### Como inserir valores em um database (banco de dados) dentro do Optix (MÉTODO INSERT)

#sqlinsert

``` C#
// Obtém a o banco de dados do Optix (Embedded Database)
var myStore = Project.Current.Get<Store>("DataStores/EmbeddedDatabase1");

// Obtém a tabela específica dentro do banco de dados
var myTable = myStore.Tables.Get<Table>("DadosProd");

// Define quais são as colunas da tabela
string[] columns = { "Status", "Observacao", "DataInicio", "DataFim"};

// Cria um objeto bidimensional para representar quantas linhas e colunas serão adicionadas ao banco de dados
var values = new object[1, 4]; // 1 linha, 4 colunas

// Define o valor de cada coluna com base na posição do Array. Ex: [0,0] define o valor pra coluna "Status", [0,1] define o valor pra coluna "Observacao"
values[0, 0] = "Produção";
values[0, 1] = "Produção normal";
values[0, 2] = DateTime.Now.ToString();
values[0, 3] = DateTime.Now.ToString();

// Execute a inserção de dados
myTable.Insert(columns, values);
```

### Como atualizar valores dentro de um database (banco de dados) dentro do Optix (MÉTODO UPDATE)

#sqlupdate

``` C#
// Obtém a o banco de dados do Optix (Embedded Database)
var myStore = Project.Current.Get<Store>("DataStores/EmbeddedDatabase1");

// Cria o output para pegar o resultado (obrigatório)
Object[,] ResultSet1;
String[] Header1;

// Atualiza os dados no banco de dados
myStore.Query($"UPDATE DadosProd SET DataFim='{DateTime.Now.ToString()}' WHERE ID={value}", out Header1, out ResultSet1);
```

### Como contar quantas linhas existem dentro de um database (banco de dados) do Optix (MÉTODO COUNT)

#sqlcount

``` C#
// Obtém a o banco de dados do Optix (Embedded Database)
var myStore = Project.Current.Get<Store>("DataStores/EmbeddedDatabase1");
 
// Cria o output para pegar o resultado (obrigatório)
Object[,] ResultSet;
String[] Header;

// Conta quantas linhas existem na tabela selecionada dentro do banco de dados
myStore.Query("SELECT COUNT(*) FROM DadosProd", out Header, out ResultSet);
int value = Convert.ToInt32(ResultSet[0, 0]);
```

### Como puxar os valores já preenchidos no database (banco de dados) do Optix (MÉTODO SELECT)

#sqlselect

``` C#
// Obtém a o banco de dados do Optix (Embedded Database)
var myStore = Project.Current.Get<Store>("DataStores/EmbeddedDatabase1");

// Instancia a label do Optix no NetLogic
var label1 = Project.Current.Get<Label>("UI/Screens/TelaCLP/PainelTelaCLP/Label1");

// Create the output to get the result (mandatory)
Object[,] ResultSet2;
String[] Header2;
// Perform the query
myStore.Query("SELECT * FROM DadosProd WHERE ID=3", out Header2, out ResultSet2);

// Muda o texto da variável conforme a pesquisa do banco
label1.Text = (String)ResultSet2[0, 3];
```

#### Como trabalhar com os dados extraídos do database (banco de dados)

#sqlselect

É necessário converter o valor extraído do banco de dados para armazenar ele numa `string`se utilizando do conversor `(String)` no começo da declaração de qual valor do banco de dados deverá ser extraído.

``` C#
// Cria a variável pra armazenar os valores do banco de dados
List <string[]> dadosGrafico = new List <string[]>();

// Passa por cada linha do DB e armazena numa lista
for (int i = 0; i < ResultSet.GetLength(0); i++)
{
    //Log.Info($"Teste de teste {ResultSet[i, 0]}");
    dadosGrafico.Add(new string[] { (String)ResultSet[i, 0], (String)ResultSet[i, 2], (String)ResultSet[i, 3] });
}
```
## Como preencher os dados de um banco de dados (database) em um DataGrid

Primeiro é necessário adicionar uma coluna, e na propriedade `Texto` dessa coluna, é necessário clicar em link dinâmico.

![[Pasted image 20240726103858.png]]

Na tela que abrir, ir em `Aliases` e encontrar o `DataGrid` criado, selecionar o `PointedNode` e escrever o nome da coluna do banco de dados de onde será puxado o valor.

![[Pasted image 20240726103901.png]]

## Como popular uma ComboBox com valores de um database (banco de dados)

**Passos:**
1. Criar um objeto no Optix que irá armazenar as variáveis (dados do banco de dados)
2. Nas propriedades da ComboBox alvo, selecionar o ``Modelo`` como o objeto criado
![[Pasted image 20240730172455.png]]
3. Criar o código pra extrair os dados do banco de dados, criar as variáveis para armazenar e adicionar elas ao objeto
``` C#
// Obtém a o banco de dados do Optix (Embedded Database)
var meuBanco = Project.Current.Get<Store>("DataStores/EmbeddedDatabase1");

// Declara variáveis para armazenar o resultado da consulta e os cabeçalhos das colunas
Object[,] ResultSet;
string[] Header;

// Executa a consulta e armazena os resultados
meuBanco.Query("SELECT * FROM DadosProd", out Header, out ResultSet);

// Cria a variável pra armazenar os valores do banco de dados
List<string[]> dadosConsulta = new List<string[]>();

// Filtra os dados e armazena pra posteriormente calcular os dados pro gráfico
for (int i = 0; i < ResultSet.GetLength(0); i++)
{
    // adiciona ao dadosConsulta os valores de: Status, Observacao, DataInicio, DataFim
    dadosConsulta.Add(new string[] { (String)ResultSet[i, 0], (String)ResultSet[i, 1], (String)ResultSet[i, 2], (String)ResultSet[i, 3] });
}

// Instancia o objeto a ser populado com os valores de DataInicio
var objectValoresDataInicio = Project.Current.Get<UAObject>("Model/objDataInicio");

// inputar variáveis novas dentro de um objeto já criado no Optix
foreach (var linha in dadosConsulta)
{
    objectValoresDataInicio.Add(InformationModel.MakeVariable(linha[2].ToString(), OpcUa.DataTypes.String));
}
```
