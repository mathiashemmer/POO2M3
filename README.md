
# POO2M3
Repositório para armazenar o conteudo pertinente ao trabalho T1 da M3 de Programação Orientada a Objetos

# Unity

A Unity não é uma IDE para desenvolvimento android. Na verdade, é um framework, com editor gráfico, para criação de diversas aplicações, voltada a criação de jogos. Com a Unity, o trabalho de desenvolver diversas partes que rodam por baixo dos panos se torna mínimo. Muitos dos processos já estão prontos, como:
* Cálculo de shaders e renderização de luz ambiente;
* Simulação de colisão e física;
* Simulação de partículas;
* Gerenciamento de animções e transições de estado;
Utilizando **C#** como linguagem, a Unity consegue, alêm de tudo, ser portatil para diversos sistemas. Não é nescessário muita alteração para, por exemplo, ter um código rodando em um computador com Linux, e um celular com Android.

# O Projeto

O objetivo deste projeto é demonstrar uma aplicação desenvolvida para o sistema Android. Para isso, foi criado um simples jogo baseado no esporte _Curling_. No jogo, deve-se jogar o disco o mais próximo possível do centro do alvo. Todo o código e assets foram desenvolvidos manualmente e são de uso livre pra qualquer fim desejado.

Para visualização/edição, é recomendado que se utilize o aplicativo Unity Remote, disponível na Google Play. Este auxilía no desenvolvimento, sincronizando o modo de jogo da máquina com o celular, como um emulador em tempo real.

# Tutorial

## Instalando Unity
* Em um navegador, acesse o link ``https://unity3d.com/get-unity/download`` e inicie o download da Unity Hub.
	 * Unity Hub é um gerenciador de versão e projetos para as aplicações desenvolvidas na unity.
* Instale o Unity Hub onde for mais conveniente.
* Abra o gerenciador. Para criar e editar projetos, é preciso de uma licença. Uma conta na Unity deve ser criada, esta é gratuita e a licença pessoal é livre de quaisquer transações ou cadastros informações financeiras.
![teste](https://github.com/mathiashemmer/POO2M3/blob/master/tutorialIMG/UnityHubStart.PNG)
* Clique na engrenagem no canto superior direito da Unity Hub. Lá é possivel logar-se com sua conta, ou com uma conta do Google/Facebook
![teste](https://github.com/mathiashemmer/POO2M3/blob/master/tutorialIMG/UnityHubSignIn.PNG)
* Após logar-se, entre na aba **Installs**, e clique em **ADD**
![teste](https://github.com/mathiashemmer/POO2M3/blob/master/tutorialIMG/UnityHubVersions.PNG)
* Selecione a versão **2019.3.0a5**
![teste](https://github.com/mathiashemmer/POO2M3/blob/master/tutorialIMG/UnityHubVersions2.PNG)
* Na janela que segue, é preciso selecionar os módulos que veem junto com a versão da Unity selecionada. É **muito importante** que seja selecionado ``Adroid Build Suport`` e ``Android SDK & NDK tools`` como mostra a imagem. Sem eles, a instalação do SDK deve ser feita manualmente, e é obrigatório para a compilação android. A instalação do Visual Studio é opicional, caso já tenha na máquina, porém um editor de código é obrigatório, já que a unity não possui.
![teste](https://github.com/mathiashemmer/POO2M3/blob/master/tutorialIMG/UnityHubVersions3.PNG)
* Prossiga com a instalação, e espere a Unity ser instalada.

## Criando e Configurando o Projeto
* De volta a aba **Projects**, clique em **New**
* Selecione **2D**, de um nome e escolha a pasta em que o projeto será salvo
* Selecione **File** no canto superior, navegue até **Build Settings** (Ctrl+Shift+B)
* Selecione a plataforma _Android_ e clique em **Switch Platform** no canto inferior direito
* Selecione **Edit** no canto superior, navegue até **Project Settings**
* Vá no menu **Editor** e altere a opção _Device_ em _Unity Remote_ para _Any Android Device_
* Feche a Unity (Caso contrário, o editor em tempo real não funcionara com o celular)
* Conecte o celular na máquina e inicie o aplicativo Unity Remote
* Reabra a Unity e seu projeto.
* Baixe o arquivo ``CurlingGame.unitypackadge``
* De volta a unity, selecione a aba **Assets** no canto superior, navegue até **Import Packedge** e selecione **Custom Packedge**
* Selecione o arquivo acima, e uma tela de confirmação de quais arquivos você deseja importar irá aparecer. Deixe todos marcados e clique em **Import**
* A Unity irá pedir para alterar a Main Scene, clique em **OK**
	* Caso não acontece, abra a pasta _Scenes_ e de dois cliques em _SampleScene_
* Clique no botão **Play**. O jogo deve iniciar na máquina, e logo em seguida, no celular. Utilize o celular para jogar!

## Explicação do Código/Projeto

A Unity trabalha com uma _pool_ (Piscina, no literal, ou uma lista) de objetos de jogo, chamados de _GameObjects_. Estes são compostos por vários módulos separadas, cada um responsável por executar uma tarefa, que acaba classificando o _GameObject_ de certa forma. O que não é nada mais que falar que são vários objetos, compostos por diferetes classes, que juntos transformam esse _GameObject_ no desejado.

No canto esquerdo, é possível ver todos os _GameObjects_ que são partes da _Scene_ em tempo de compilação. Novos objetos podem ser criados durante a execução. Como exemplo, o objeto _Goal_ nada mais é que um objeto composto pelos módulos _Transform_ e _Sprite Renderer_. O primeiro é obrigatório para todos os objetos na _Scene_, ele indentifica o posicionamento do objeto no mundo do jogo. O segundo apenas renderiza uma sprite na _Scene_, baseado na posição, ou seja, no _Transform_.

Alguns objetos não são vistos pelo jogador, como o _InputHandler_. Seu propósito é meramente executar a lógica do jogo. Dentro dele, pode-se ver um módulo _Input Manager_, que é um script em **C#** que foi desenvolvido por fora, ou seja, não fou a Unity que disponibilizou. Acessando o menu **Assets -> Scripts** no canto inferior esquerdo, um ícone de arquivo com um _#_ irá aparecer. Clicando duas vezes, o editor de script de sua preferência irá abrir para alterar o arquivo.

Uma grande vantagem, é que certas opções são editaveis pelo menu da Unity. Por exemplo, no objeto _InputHandler_, na seção do script _Input Manager_, existem várias opções editaveis. Algumas delas não devem ser alteradas, pois são referências a outros objetos de _Scene_. Localize a opção _Force Amplify_ e edite para 1000. Clique em play e de um pequeno toque na tela. O Disco se moverá muito mais dessa vez. Vale ressaltar que estas alterações são **por GameObject**, ou seja, não irão afetar outros objetos na _Scene_ que tenham esse módulo.

### Ciclo de Execução

Ao apertar play, duas coisas muito importantes acontecem nos objetos. Para toda a pool de objetos da _Scene_, é chamado o método _Start()_. Este é executado **uma vez** que o objeto é instanciado na _Scene_. Durante todos os frames do jogo, ou seja, em todos os ciclos do loop de jogo, é chamado o método _Update()_. A Unity trabalha com otimizações para garantir que os códigos inseridos nesses métodos não travem a aplicação.

A maior parte do jogo ocorre no método _Update()_, já que é alí que podemos fazer a interação do jogador com o jogo. Um exemplo disso é na linha 67, onde verificamos se há algum toque na tela, com o acesso a variavel global _Input.touchCount_. Este armazena quantos toques na tela existem no frame atual. O prefixo _Input_ é uma classe disponibilizada pela Unity que guarda informações dos periféricos de acesso, como o mouse, o teclado, o touchscreen, dentre outros.

Atraves destes, podemos criar/desenvolver aplicações utilizando a Unity para o sistema Android.




