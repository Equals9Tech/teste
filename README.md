<p align="center" >
<img width="300" src="https://equalsimages.s3.amazonaws.com/branca3.webp"/>
</p>
<h1 align="center">Teste para dev frontent da Equals9</h1>

## Índice 
   * [Introdução](#Introdução)
   * [Programas Necessários / Bibliotecas Utilizadas](#Programas)
   * [EndPoints da API](#EndPoints)
   * [Dicas](#Dicas)
   * [Considerações](#Considerações)

## Introdução

1. Faça um clone desse [repositório](https://github.com/Equals9Tech/teste).
2. Crie uma aplicação com create-react-app.
3. Adicione uma tela simples de login e registro utilizando [axios](https://axios-http.com/docs/intro) para comunicação com a api.
4. Ao receber a resposta da função de login, armazenar o token que será retornado pela requisição no localStorage to browser.
5. Após autenticar, adicionar duas telas com um menu utilizando a biblioteca [react-router-dom](https://v5.reactrouter.com/web/guides/quick-start) para fazer o controle das rotas.
6. Na primeira tela a finalidade é criar um ToDo, monte um input para adicionar uma tarefa e liste todas abaixo com um botão para deletá-la individualmente e um checkbox para concluir ou ativar novamente a tarefa.
7. Na segunda tela a finalidade é criar um jogo ou uma atividade simples e interativa, fica á sua escolha (como exemplo um jogo da velha ou uma calculadora).

## Programas

As ferramentas e bibliotecas para criar o projeto são (podendo utilizar outras caso necessário):

- [Node.js](https://nodejs.org/en/)
- [Git](https://git-scm.com/)
- [React](https://pt-br.reactjs.org/)
- [Axios](https://axios-http.com/docs/intro)
- [React Router](https://v5.reactrouter.com/web/guides/quick-start)
- [Material-UI (Opicional)](https://mui.com/pt/getting-started/installation/)

## EndPoints

<h1>API: http

<table align='center'>
  <thead>
    <tr>
      <td>Método</td>
      <td>EndPoint</td>
      <td>Body</td>
      <td>Descrição</td>
      <td>Retorno</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td>/signup</td>
      <td>{ username: "user", password: "pass" }</td>
      <td>Rota para criar usuário novo</td>
      <td>{</br>"msg": "Usuario criado com sucesso!"</br>}</td>
    </tr>
    <tr>
      <td>POST</td>
      <td>/auth</td>
      <td>{</br> username: "user", password: "pass" </br>}</td>
      <td>Rota para fazer requisição de login autenticando usuário</td>
      <td>{</br>
	"msg": "Usuário autenticado com sucesso!",</br>
	"token": "eyJhbGciOiJIUzI1N..."</br>
}</td>
    </tr>
    <tr>
      <td>GET</td>
      <td>/todo</td>
      <td>{ params: { page: 1 } }</td>
      <td>Retorna todos os items da lista de tarefas</td>
      <td>{</br>
	"docs": [{</br>
			"_id": "61cf4b45182b60288ed4553a",</br>
			"tarefa": "teste1",</br>
			"ativo": true,</br>
			"registro": "2021-12-31T18:26:13.742Z",</br>
			"__v": 0}],</br>
	"total": 1,</br>
	"limit": 20</br>
}</td>
    </tr>
    <tr>
      <td>POST</td>
      <td>/todo</td>
      <td>{ tarefa: "tarefa", ativo: true }</td>
      <td>Cria uma nova tarefa encaminhando os parâmetros acima</td>
      <td>{</br>
	"_id": "61cf4b45182b60288ed4553a",
	"tarefa": "teste1",
	"ativo": true,
	"registro": "2021-12-31T18:26:13.742Z",
	"__v": 0</br>
}</td>
    </tr>
    <tr>
      <td>DELETE</td>
      <td>/todo/:id</td>
      <td></td>
      <td>Deleta a tarefa que for passada como id no parâmetro</td>
      <td>{</br>
	"docs": [{</br>
			"_id": "61cf4b45182b60288ed4553a",</br>
			"tarefa": "teste1",</br>
			"ativo": true,</br>
			"registro": "2021-12-31T18:26:13.742Z",</br>
			"__v": 0}],</br>
	"total": 1,</br>
	"limit": 20</br>
}</td>
    </tr>
    <tr>
      <td>PATCH</td>
      <td>/todo/:id</td>
      <td>{tarefa:'nomeTarefa',ativo:false}</td>
      <td>Edita o valor da tarefa, podendo mandar somente um dos parâmetros para fazer atualização. (lembre de encaminhar o id da tarefa no parâmetro para modificar)</td>
    <td>[{</br>
			"_id": "61cf4b45182b60288ed4553a",</br>
			"tarefa": "teste1",</br>
			"ativo": true,</br>
			"registro": "2021-12-31T18:26:13.742Z",</br>
			"__v": 0}],</br>
	"total": 1,</br>
	"limit": 20</br>
}</td>
</tr>
  </tbody>
</table>

## Dicas

  - Clone do projeto por Https
  ```bash
  git clone https://github.com/Equals9Tech/teste.git .
  ```
  
  - Clone do projeto por SSH
  ```bash
  git clone git@github.com:Equals9Tech/teste.git .
  ```
  
  - Criar Projeto após o clone
  ```bash
  npx create-react-app .
  ```
  
  - Instalar as Bibliotecas 
  ```bash
  npm i axios react-router-dom 
  ```
  
  - Exemplo de utilização do axios para login
  ```jsx
  import React,{useRef} from 'react'
  import axios from 'axios';
  
  const App = () => {
    const usernameValue = useRef(null)
    const passwordValue = useRef(null)
    const endpoint = 'https://endpoint.com'

    const handleLogin = async () => {
      const submitLoginValue = {username: usernameValue.current?.value, password: passwordValue.current?.value}
      const submitLogin = await axios.post(`${endpoint}/login/`, submitLoginValue).catch(console.log)
      const resultado = submitLogin.data
      // utilizar o resultado para armazenar o token no localStorage do Browser
    }

    return (
      <>
        <input type='text' ref={usernameValue} placeholder='Username' />
        <input type='password' ref={passwordValue} placeholder='Password' />
        <Button type="primary" onClick={handleLogin}>Entrar</Button>
      </>
    )}
  ```
  
   - Exemplo de criação de conta
  ```jsx
    const handleCreateAccount = async (username,password) => {
      const createAccount = await axios.post(`${endpoint}/login/${id}`,{ username:username,password:password }).catch(console.log)
      const resultado = deleteTodo.data
      // Atualizar a lista de todos a partir do resultado
    }
  ```
  
  - Exemplo de criação tarefa
  ```jsx
    const handleCreateTodo = async (tarefa) => {
      const submitTodo = await axios.post(`${endpoint}/todo`, tarefa).catch(console.log)
      const resultado = submitTodo.data
      // Atualizar a lista de todos a partir do resultado
    }
  ```
  
   - Exemplo de atualização de tarefa
  ```jsx
    const handleUpdateStatus = async (id) => {
      const submitUpdatedValue = await axios.patch(`${endpoint}/todo/${id}`, { active:false }).catch(console.log)
      const resultado = submitUpdatedValue.data
      // Atualizar a lista de todos a partir do resultado
    }
    const handleUpdateTodoName = async (id) => {
      const submitUpdatedValue = await axios.patch(`${endpoint}/todo/${id}`, { tarefa:'novoNome' }).catch(console.log)
      const resultado = submitUpdatedValue.data
      // Atualizar a lista de todos a partir do resultado
    }
  ```
  
   - Exemplo de deleção de tarefa
  ```jsx
    const handleDeleteTodo = async (id) => {
      const deleteTodo = await axios.delete(`${endpoint}/todo/${id}`).catch(console.log)
      const resultado = deleteTodo.data
      // Atualizar a lista de todos a partir do resultado
    }
  ```
  - Exemplo de Utilização de redirecionamento do rect-router-dom para login caso não tenha token ainda.
  ```jsx
  <Route {...rest} render={() => (token ? <Component {...rest} /> : <Redirect to="/login" />)} />
  ```


## Considerações

  A tendência é a aplicação ser simples e direta, então levaremos em consideração a funcionalidade e a criatividade no layout.
  O endereço do meu discord é Ikira#1181, fique a vontade para tirar qualquer dúvida por mais que pareça simples. Buscar a informação é uma virtude, sanar as dúvidas é importante para o desenvolvimento, independente do nível de dificuldade =D.
  
  Um detalhe que é opcional porém seria muito bem visto por nós, seria utilizar a biblioteca do MetaMask para react para conectar e ler balanço da carteira
  
  biblioteca: [Metamask-React](https://www.npmjs.com/package/metamask-react)
  
  carteira do MetaMask: [Metamask](https://metamask.io/)
  
