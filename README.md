# Counter-App-Carrito-de-Compras-
<html>
<head>
    <title>Counter App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f5f5f5;
        }
        .counter-container {
            text-align: center;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .counter-value {
            font-size: 48px;
            margin: 20px 0;
            color: #333;
        }
        button {
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        .decrement {
            background-color: #f44336;
        }
        .decrement:hover {
            background-color: #d32f2f;
        }
        .reset {
            background-color: #2196F3;
        }
        .reset:hover {
            background-color: #0b7dda;
        }
    </style>
</head>
<body>
    <div class="counter-container">
        <h1>Counter App</h1>
        <div class="counter-value" id="count">0</div>
        <div class="buttons">
            <button class="decrement" onclick="decrement()">- Decrement</button>
            <button class="reset" onclick="reset()">Reset</button>
            <button class="increment" onclick="increment()">+ Increment</button>
        </div>
    </div>

    <script>
        let count = 0;
        const countElement = document.getElementById('count');

        function updateCount() {
            countElement.textContent = count;
        }

        function increment() {
            count++;
            updateCount();
        }

        function decrement() {
            count--;
            updateCount();
        }

        function reset() {
            count = 0;
            updateCount();
        }
    </script>
</body>
</html>
