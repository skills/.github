<!DOCTYPE html><html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heron - IA de Tarefas</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-900">
  <!-- Tela de Login -->
  <div id="loginPage" class="flex items-center justify-center min-h-screen">
    <div class="bg-white p-8 rounded-2xl shadow-md w-full max-w-md">
      <h2 class="text-2xl font-bold mb-4 text-center">Login no Heron</h2>
      <input type="text" id="loginEmail" placeholder="Email" class="w-full p-2 mb-3 border rounded">
      <input type="password" id="loginPassword" placeholder="Senha" class="w-full p-2 mb-3 border rounded">
      <button onclick="login()" class="w-full bg-blue-600 text-white p-2 rounded hover:bg-blue-700">Entrar</button>
      <p class="text-center text-sm mt-4">Não tem conta? <a href="#" onclick="showRegister()" class="text-blue-600 hover:underline">Cadastre-se</a></p>
    </div>
  </div>  <!-- Tela de Cadastro -->  <div id="registerPage" class="hidden flex items-center justify-center min-h-screen">
    <div class="bg-white p-8 rounded-2xl shadow-md w-full max-w-md">
      <h2 class="text-2xl font-bold mb-4 text-center">Cadastro no Heron</h2>
      <input type="text" id="registerEmail" placeholder="Email" class="w-full p-2 mb-3 border rounded">
      <input type="password" id="registerPassword" placeholder="Senha" class="w-full p-2 mb-3 border rounded">
      <button onclick="register()" class="w-full bg-green-600 text-white p-2 rounded hover:bg-green-700">Cadastrar</button>
      <p class="text-center text-sm mt-4">Já tem conta? <a href="#" onclick="showLogin()" class="text-blue-600 hover:underline">Entrar</a></p>
    </div>
  </div>  <!-- Dashboard -->  <div id="dashboard" class="hidden p-6">
    <h1 class="text-3xl font-bold mb-6">Bem-vindo ao Heron!</h1>
    <h2 class="text-xl font-semibold mb-4">Matérias</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <div class="bg-white p-4 rounded-2xl shadow hover:shadow-lg">
        <h3 class="text-lg font-bold">Matemática</h3>
        <button onclick="openTask('Matemática')" class="mt-2 bg-blue-500 text-white px-4 py-1 rounded">Enviar Tarefa</button>
      </div>
      <div class="bg-white p-4 rounded-2xl shadow hover:shadow-lg">
        <h3 class="text-lg font-bold">Português</h3>
        <button onclick="openTask('Português')" class="mt-2 bg-blue-500 text-white px-4 py-1 rounded">Enviar Tarefa</button>
      </div>
      <div class="bg-white p-4 rounded-2xl shadow hover:shadow-lg">
        <h3 class="text-lg font-bold">História</h3>
        <button onclick="openTask('História')" class="mt-2 bg-blue-500 text-white px-4 py-1 rounded">Enviar Tarefa</button>
      </div>
    </div>
  </div>  <!-- Envio de Tarefas -->  <div id="taskPage" class="hidden p-6">
    <h2 id="subjectTitle" class="text-2xl font-bold mb-4">Enviar Tarefa</h2>
    <textarea id="taskText" rows="6" placeholder="Cole sua tarefa aqui..." class="w-full p-4 border rounded mb-4"></textarea>
    <button onclick="submitTask()" class="bg-green-600 text-white px-6 py-2 rounded hover:bg-green-700">Enviar</button>
    <button onclick="backToDashboard()" class="ml-4 text-gray-700 underline">Voltar</button>
  </div>  <script>
    function showRegister() {
      document.getElementById('loginPage').classList.add('hidden');
      document.getElementById('registerPage').classList.remove('hidden');
    }

    function showLogin() {
      document.getElementById('registerPage').classList.add('hidden');
      document.getElementById('loginPage').classList.remove('hidden');
    }

    function login() {
      const email = document.getElementById('loginEmail').value;
      const pass = document.getElementById('loginPassword').value;
      if (email && pass) {
        document.getElementById('loginPage').classList.add('hidden');
        document.getElementById('dashboard').classList.remove('hidden');
      } else {
        alert('Preencha todos os campos.');
      }
    }

    function register() {
      const email = document.getElementById('registerEmail').value;
      const pass = document.getElementById('registerPassword').value;
      if (email && pass) {
        alert('Cadastro realizado! Faça login.');
        showLogin();
      } else {
        alert('Preencha todos os campos.');
      }
    }

    let currentSubject = '';

    function openTask(subject) {
      currentSubject = subject;
      document.getElementById('dashboard').classList.add('hidden');
      document.getElementById('taskPage').classList.remove('hidden');
      document.getElementById('subjectTitle').innerText = `Enviar Tarefa - ${subject}`;
    }

    function submitTask() {
      const task = document.getElementById('taskText').value;
      if (task.trim()) {
        alert(`Tarefa de ${currentSubject} enviada com sucesso!`);
        document.getElementById('taskText').value = '';
        backToDashboard();
      } else {
        alert('Cole sua tarefa antes de enviar.');
      }
    }

    function backToDashboard() {
      document.getElementById('taskPage').classList.add('hidden');
      document.getElementById('dashboard').classList.remove('hidden');
    }
  </script></body>
</html>
