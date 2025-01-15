<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestión de Amigos - AmigoSecretoPro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #4CAF50;
            color: white;
            text-align: center;
            padding: 1rem;
        }
        main {
            padding: 2rem;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 2rem;
            border-radius: 5px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .form-group {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
        }
        .form-group input {
            flex: 1;
            padding: 0.5rem;
            font-size: 1rem;
            margin-right: 1rem;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .form-group button {
            padding: 0.5rem 1rem;
            font-size: 1rem;
            color: white;
            background-color: #4CAF50;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .form-group button:hover {
            background-color: #45a049;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        ul li {
            background: #e8f5e9;
            margin: 0.5rem 0;
            padding: 0.5rem;
            border-radius: 4px;
            display: flex;
            justify-content: space-between;
        }
        ul li button {
            background: red;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            padding: 0.3rem 0.6rem;
        }
        ul li button:hover {
            background: darkred;
        }
        #resultadoSorteo {
            margin-top: 1rem;
            font-size: 1.2rem;
            font-weight: bold;
            color: #4CAF50;
        }
    </style>
</head>
<body>
    <header>
        <h1>Gestión de Amigos - AmigoSecretoPro</h1>
    </header>
    <main>
        <div class="container">
            <h2>Agrega tus amigos a la lista</h2>
            <div class="form-group">
                <input type="text" id="nombreAmigo" placeholder="Escribe el nombre del amigo">
                <button onclick="agregarAmigo()">Agregar Amigo</button>
            </div>
            <h3>Lista de Amigos</h3>
            <ul id="listaAmigos"></ul>
            <button onclick="sortearAmigo()">Sorteo Amigo Secreto</button>
            <div id="resultadoSorteo"></div>
        </div>
    </main>

    <script>
        // Array para almacenar los nombres de los amigos
        let listaDeAmigos = [];

        // Función para agregar un amigo
        function agregarAmigo() {
            const campoAmigo = document.getElementById("nombreAmigo");
            const nombreAmigo = campoAmigo.value.trim();

            if (nombreAmigo === "") {
                alert("Por favor, inserta un nombre válido.");
                return;
            }

            listaDeAmigos.push(nombreAmigo);
            actualizarListaAmigos();

            campoAmigo.value = "";
        }

        // Función para actualizar la lista en la pantalla
        function actualizarListaAmigos() {
            const listaElement = document.getElementById("listaAmigos");

            // Limpiar la lista existente
            listaElement.innerHTML = "";

            // Recorrer el arreglo y agregar cada amigo a la lista
            for (const amigo of listaDeAmigos) {
                const elementoLista = document.createElement("li");
                elementoLista.textContent = amigo;

                const botonEliminar = document.createElement("button");
                botonEliminar.textContent = "Eliminar";
                botonEliminar.onclick = () => eliminarAmigo(amigo);

                elementoLista.appendChild(botonEliminar);
                listaElement.appendChild(elementoLista);
            }
        }

        // Función para eliminar un amigo de la lista
        function eliminarAmigo(amigo) {
            listaDeAmigos = listaDeAmigos.filter(a => a !== amigo);
            actualizarListaAmigos();
        }

        // Función para seleccionar un amigo de manera aleatoria
        function sortearAmigo() {
            // Validar que haya amigos disponibles
            if (listaDeAmigos.length === 0) {
                document.getElementById("resultadoSorteo").textContent = "No hay amigos para sortear.";
                return;
            }

            // Generar un índice aleatorio
            const indiceAleatorio = Math.floor(Math.random() * listaDeAmigos.length);

            // Obtener el nombre sorteado
            const amigoSorteado = listaDeAmigos[indiceAleatorio];

            // Mostrar el resultado
            document.getElementById("resultadoSorteo").textContent = `El amigo secreto es: ${amigoSorteado}`;
        }
    </script>
</body>
</html>
