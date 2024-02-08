# Trabalhando com Machine Learning na Prática no Azure ML

## 🎈 Como criar um modelo de previsão 


### 1° Passo - Crie um Recurso

- Clique no botão localizado no canto superior esquerdo ___Criar um recurso___.
- Na barra de pesquisa, digite ___Machine Learning___.
- Após ter localizado o recurso ___Azure Machine Learning___ , clique em ___Criar___.

### 2° Passo - Preencha as informações solicitadas

- Em ___Grupo de recursos___, caso você não tenha, clique em ___Criar novo___. Escolha um nome qualquer para ele.
- Em ___Nome___, escolha um nome para a área de trabalho.
- Em ___Região___, escolha _East US_.
- Não altere as outras informações. 
- Na parte inferior da página, clique em ___Examinar + criar___.
- Espere o recurso ser criado. Clique no botão ___Ir para o recurso___.
- Clique no botão ___Iniciar o estúdio___.
 
### 3° Passo - Crie o modelo

- No menu localizado no canto esquerdo da tela, clique em ___ML automatizado___ e em seguida clique em ___Novo trabalho de ML automatizado___. 
- Em ___Configurações básicas___, preencha as informações solicitadas utilizando as seguintes informações:
- ___Nome do trabalho___: mslearn-bike-automl
- ___Novo nome do experimento___: mslearn-bike-rental
- ___Descrição___: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- Clique em ___Avançar___.
- Em ___Tipo de tarefa e dados___, selecione o tipo da tarefa como ___Regressão___. 
- Em ___Selecionar os dados___, clique em ___Criar___ e em seguida, defina o nome do ativo de dados como _alugueldebicicletas_, a descrição como _dados históricos do aluguel de bicicletas_ e o tipo como _Tabular_.
- Escolha Arquivos da Web como fonte para o ativo de dados e clique em ___Avançar___.
- Em ___URL da Web___, insira o seguinte link: ___https://aka.ms/bike-rentals___ e clique em ___Avançar___.
- Em ___Configurações___, vá em ___Cabeçalhos de coluna___ e altere para _Somente o primeiro arquivo tem cabeçalhos_. Em seguida, após o carregamento dos dados, clique em ___Avançar___. 
- Em ___Esquema___, clique em ___Avançar___.
- Em ___Examinar___, clique em ___Criar___.
- Clique em _alugueldebicicletas_, que estará na cor azul, e em seguida em ___Avançar___. 
- Em ___Configurações de tarefas___, selecione _rentals(Integer)_ como coluna de destino.
- Logo abaixo, clique em ___Exibir definições de configuração adicionais___.
- Desmarque as opções ___Explicar o melhor modelo___ e ___Usar todos os modelos suportados___.
- Em ___Modelos permitidos___, selecione _RandomForest_ e _LightGBM_. Após, clique em ___Salvar___.
- Expanda a aba ___Limites___ e insira os seguintes números, de cima para baixo, iniciando em ___Máximo de avaliações___ e finalizando em ___Tempo limite de iteração___: 3, 3, 3, 0.085, 15, 15. 
- Marque a opção ___Habilitar encerramento antecipado___. 
- Em ___Tipo de validação___, selecione _Divisão de validação de treinamento_. Clique em ___Avançar___
- Em ___Computação___, não mexa em nada. Apenas clique em ___Avançar___.
- Em ___Examinar___, analise se as informações estão corretas. Caso esteja tudo certo, clique em ___Enviar trabalho de treinamento___. 
- Na aba ___Propriedades___, aguarde o _Status_ estabelecer-se como _Concluído_. 
- Na aba ___Melhor resumo de modelo___, clique no texto abaixo de _Nome do algoritmo_.
- Em seguida, clique em ___Implantar___ e em ___Serviço Web___.
- Implante o modelo com as seguintes informações:
- ___Nome___: predict-rentals
- ___Descrição___: Predict cycle rentals
- ___Tipo de computação___: Azure Container Instance
- Selecione ___Habilitar autenticação___.
- Espere a implantação do modelo ser finalizada com sucesso. 
- No menu à esquerda, vá para ___Modelos___ e selecione o modelo criado. Em seguida, clique no texto abaixo de ___Criado por trabalho___, localizado na aba ___Atributos___. 
- Localize o botão ___Métricas___.

### 4° Passo - Teste o modelo

- Na barra esquerda, clique em ___Pontos de extremidade___ e localize o modelo _predict-rentals_.
- Clique nele, em seguida vá para ___Testar___.
- Em ___Inserir dados para teste de ponto de extremidade___, insira o seguinte código e clique em ___Testar___:

```
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```
- Observe o resultado do teste. Meu resultado foi o seguinte:
```
{
  "Results": [
    352.6350349989648
  ]
}
```

 



---

