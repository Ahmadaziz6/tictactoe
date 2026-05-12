#tictactoe        font-size: 40px;
        color: white;
        cursor: pointer;

        display: flex;
        align-items: center;
        justify-content: center;
    }

    .cell:hover {
        background: #444;
    }

    #status {
        margin-top: 20px;
        font-size: 20px;
    }

    button {
        margin-top: 20px;
        padding: 10px 20px;
        font-size: 16px;
        cursor: pointer;
    }
</style>
</head>

<body>

<h1>Tic Tac Toe</h1>

<div class="board" id="board">
    <div class="cell" onclick="main(0)"></div>
    <div class="cell" onclick="main(1)"></div>
    <div class="cell" onclick="main(2)"></div>
    <div class="cell" onclick="main(3)"></div>
    <div class="cell" onclick="main(4)"></div>
    <div class="cell" onclick="main(5)"></div>
    <div class="cell" onclick="main(6)"></div>
    <div class="cell" onclick="main(7)"></div>
    <div class="cell" onclick="main(8)"></div>
</div>

<div id="status">Giliran: X</div>

<button onclick="resetGame()">Reset</button>

<script>
    let board = ["", "", "", "", "", "", "", "", ""];
    let currentPlayer = "X";
    let gameOver = false;

    const winPattern = [
        [0,1,2],
        [3,4,5],
        [6,7,8],
        [0,3,6],
        [1,4,7],
        [2,5,8],
        [0,4,8],
        [2,4,6]
    ];

    function main(index) {
        if (board[index] !== "" || gameOver)
            return;

        board[index] = currentPlayer;

        const cells = document.querySelectorAll(".cell");
        cells[index].innerText = currentPlayer;

        if (cekMenang()) {
            document.getElementById("status").innerText =
                "Pemain " + currentPlayer + " menang!";
            gameOver = true;
            return;
        }

        if (!board.includes("")) {
            document.getElementById("status").innerText =
                "Permainan seri!";
            gameOver = true;
            return;
        }

        currentPlayer = currentPlayer === "X" ? "O" : "X";

        document.getElementById("status").innerText =
            "Giliran: " + currentPlayer;
    }

    function cekMenang() {
        return winPattern.some(pattern => {
            return pattern.every(index => {
                return board[index] === currentPlayer;
            });
        });
    }

    function resetGame() {
        board = ["", "", "", "", "", "", "", "", ""];
        currentPlayer = "X";
        gameOver = false;

        document.querySelectorAll(".cell").forEach(cell => {
            cell.innerText = "";
        });

        document.getElementById("status").innerText =
            "Giliran: X";
    }
</script>

</body>
</html>
