<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Aprovação - UNINASSAU</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #003366; /* Fundo azul escuro */
            color: #ffffff;
        }

        .container {
            text-align: center;
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            width: 300px;
            color: #333;
        }

        h1 {
            font-size: 28px;
            color: #0056a6;
            margin: 0 0 20px;
        }

        h2 {
            font-size: 20px;
            color: #333;
            margin: 0 0 20px;
        }

        label {
            font-size: 16px;
            color: #555;
        }

        input[type="number"] {
            width: 100%;
            padding: 8px;
            margin: 8px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }

        button {
            width: 100%;
            padding: 10px;
            background-color: #0056a6;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
        }

        button:hover {
            background-color: #004080;
        }

        #resultado {
            font-size: 16px;
            margin-top: 20px;
            color: #333;
        }

        #notaNecessaria {
            font-size: 14px;
            color: #777;
            margin-top: 10px;
        }

        footer {
            position: fixed;
            bottom: 10px;
            right: 10px;
            font-size: 14px;
            color: #ffffff;
            text-align: right;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>UNINASSAU</h1>
        <h2>Calculadora de Aprovação</h2>
        <form>
            <label for="av1">Nota AV1:</label>
            <input type="number" id="av1" min="0" max="10" step="0.1" placeholder="Digite a nota da AV1"><br>

            <label for="av2">Nota AV2:</label>
            <input type="number" id="av2" min="0" max="10" step="0.1" placeholder="Digite a nota da AV2"><br>

            <label for="final">Nota Final:</label>
            <input type="number" id="final" min="0" max="10" step="0.1" placeholder="Nota da Final (se aplicável)" disabled><br>

            <button type="button" onclick="calcular()">Calcular</button>
        </form>

        <h3 id="resultado"></h3>
        <p id="notaNecessaria"></p>
    </div>

    <footer>
        Desenvolvida por Prof. Antonio Carlos<br>
        UNINASSAU - Garanhuns
    </footer>

    <script>
        function calcular() {
            let av1 = parseFloat(document.getElementById("av1").value) || 0;
            let av2 = parseFloat(document.getElementById("av2").value) || 0;
            let final = parseFloat(document.getElementById("final").value) || 0;
            let media = (av1 + av2) / 2;
            let resultado = document.getElementById("resultado");
            let notaNecessaria = document.getElementById("notaNecessaria");

            resultado.innerHTML = "";
            notaNecessaria.innerHTML = "";

            if (av1 > 0 && av2 > 0) {
                if (media >= 7) {
                    resultado.innerHTML = "Aluno aprovado! Média: " + media.toFixed(2);
                } else if (media < 4) {
                    resultado.innerHTML = "Aluno reprovado sem direito de fazer a final, pois a média é menor que 4. Média: " + media.toFixed(2);
                } else {
                    resultado.innerHTML = "Aluno na final! Média: " + media.toFixed(2);
                    let notaParaFinal = (5 * 2 - media).toFixed(2); 
                    notaNecessaria.innerHTML = "Nota mínima necessária na prova final: " + notaParaFinal;
                    document.getElementById("final").disabled = false;
                }
            } else if (av1 > 0 || av2 > 0) {
                let notaFaltante = av1 > 0 ? 7 - av1 : 7 - av2;
                resultado.innerHTML = "Nota necessária na AV" + (av1 > 0 ? "2" : "1") + ": " + notaFaltante.toFixed(2);
            } else {
                resultado.innerHTML = "Por favor, insira pelo menos uma nota.";
            }

            if (final > 0 && media < 7 && media >= 4) {
                let mediaFinal = (media + final) / 2;
                notaNecessaria.innerHTML = ""; 
                if (mediaFinal >= 5) {
                    resultado.innerHTML = "Aluno aprovado na final! Média Final: " + mediaFinal.toFixed(2);
                } else {
                    resultado.innerHTML = "Aluno reprovado na final. Média Final: " + mediaFinal.toFixed(2);
                }
            }
        }
    </script>
</body>
</html>
