# web1-Compiladores
<!DOCTYPE html>
<html>
<head>    
    <title>Análise Léxica</title>
    <style>
    body {
        background-color: #D3D3D3;
        text-align: center;
    }
    h1 {
        color: #FFFFFF;
        background-color: #000000;
        padding: 10px;
    }
    table {
        border-collapse: collapse;
        margin-top: 20px;
        background-color:#FFFFFF;
        margin: 0 auto;
    }
    th, td {
        border: 1px solid black;
        padding: 8px;
    }
    th {
        background-color: #000000d2;
        color: #FFFFFF;
    }
    button {
        background-color: #000000;
        color: #FFFFFF;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
    }
    button:hover {
        background-color: #FFBF69;
    }
    .imagem-esquerda {
        float: left;
        margin-right: 20px;
    }
    .imagem-direita {
        float: right;
        margin-left: 20px;
    }
        img {
        width: 200px;
        height: 1700px;
        }
        
    </style>
</head>
<body>
    <h1>Análise Léxica</h1>
    <img class="imagem-esquerda" src="E:\teste HTML\WEB1\1.1.jpg" alt="Imagem à esquerda">
    <img class="imagem-direita" src="E:\teste HTML\WEB1\1.1.jpg" alt="Imagem à direita">
    <textarea id="input" rows="10" cols="50" autofocus></textarea>
    <br>
    <button onclick="analisar()">Analisar</button>
    <button onclick="limpar()">Limpar</button>
    <br>

    <table id="tabela">
    <thead>
        <tr>
        <th>Token</th>
        <th>Identificação</th>
        <th>Tamanho</th>
        <th>Posição (linha, coluna)</th>
        </tr>
    </thead>
    <tbody>
    </tbody>
    </table>

    <script>
      // Definindo as palavras reservadas, operadores e terminador
    const palavrasReservadas = ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield', 'range'];
    const operadores = ["=", "+", "==", "!=", "<", ">", "<=", ">="];
    const terminador = [";", ":"];

      // Definindo a expressão regular para identificar tokens
    const regexToken = /[a-zA-Z_][a-zA-Z0-9_]*|[0-9]+|[=+<>!]=?|;|:/g;

// Função para analisar o texto de entrada
function analisar() {
const input = document.getElementById("input").value;
const linhas = input.split("\n");

let tabela = document.getElementById("tabela").getElementsByTagName("tbody")[0];
tabela.innerHTML = "";

for (let i = 0; i < linhas.length; i++) {
    let tokens = linhas[i].match(regexToken);
    let coluna = 0;

    for (let j = 0; j < tokens.length; j++) {
    let token = tokens[j];
    let identificacao;
    let tamanho = token.length;

    let posicaoInicial = linhas[i].indexOf(token, coluna);
    let posicaoFinal = posicaoInicial + tamanho - 1;

    if (palavrasReservadas.includes(token)) {
        identificacao = "Palavra Reservada";
    } else if (operadores.includes(token)) {
        identificacao = "Operador";
    } else if (terminador.includes(token)) {
        identificacao = "Terminador";
        posicaoFinal--;
    } else if (!isNaN(token)) {
        identificacao = "Constante";
    } else {
        identificacao = "Apenas Identificador";
    }

    let linha = i;
    let posicao = "(" + linha + "," + posicaoInicial + ")";

    let row = tabela.insertRow();
    let cellToken = row.insertCell(0);
    let cellIdentificacao = row.insertCell(1);
    let cellTamanho = row.insertCell(2);
    let cellPosicao = row.insertCell(3);

    cellToken.innerHTML = token;
    cellIdentificacao.innerHTML = identificacao;
    cellTamanho.innerHTML = tamanho;
    cellPosicao.innerHTML = posicao;

    coluna = posicaoFinal + 1;
    }
}
}  
    function limpar() {
    document.getElementById("input").value = "";
    document.getElementById("input").focus();
    } 
    </script>
</body>
</html>
