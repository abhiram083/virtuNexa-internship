 A simple event countdown page that shows the time remaining until the event starts.


Structure:
      -User Interface: Design a simple and user-friendly web interface where users can input a number and calculate its factorial using both iterative and recursive methods.
      -Input Validation: Implement checks to ensure the user enters a valid positive integer.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Countdown and Factorial Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
            background-color: #f4f4f9;
        }
        .container {
            width: 60%;
            margin: 0 auto;
        }
        .countdown {
            font-size: 3em;
            margin: 20px 0;
        }
        .factorial-section {
            margin-top: 30px;
        }
        input[type="number"] {
            padding: 10px;
            font-size: 1.2em;
            margin: 10px;
            width: 200px;
        }
        button {
            padding: 10px 15px;
            font-size: 1.2em;
            cursor: pointer;
        }
        .result {
            font-size: 1.5em;
            margin-top: 20px;
        }
        .error {
            color: red;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Event Countdown</h1>
        <div id="countdown" class="countdown">Loading...</div>

        <hr>

        <div class="factorial-section">
            <h2>Factorial Calculator</h2>
            <label for="numberInput">Enter a positive integer:</label>
            <input type="number" id="numberInput" min="0">
            <button onclick="calculateFactorial()">Calculate Factorial</button>

            <div class="result">
                <p id="factorialResult"></p>
                <p id="recursiveResult"></p>
            </div>
            <p id="errorMessage" class="error"></p>
        </div>
    </div>

    <script>
        // Event Countdown Timer
        const eventDate = new Date("2025-01-15T00:00:00Z"); // Set event date
        function updateCountdown() {
            const now = new Date();
            const timeDifference = eventDate - now;

            if (timeDifference <= 0) {
                document.getElementById('countdown').innerHTML = "The event has started!";
                clearInterval(countdownInterval);
            } else {
                const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
                const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);
                document.getElementById('countdown').innerHTML = `${days}d ${hours}h ${minutes}m ${seconds}s`;
            }
        }

        const countdownInterval = setInterval(updateCountdown, 1000);
        updateCountdown();

        // Factorial Calculator
        function calculateFactorial() {
            const numberInput = document.getElementById('numberInput').value;
            const errorMessage = document.getElementById('errorMessage');
            const factorialResult = document.getElementById('factorialResult');
            const recursiveResult = document.getElementById('recursiveResult');

            // Reset error message
            errorMessage.textContent = "";
            factorialResult.textContent = "";
            recursiveResult.textContent = "";

            // Validate the input
            const number = parseInt(numberInput);
            if (isNaN(number) || number < 0) {
                errorMessage.textContent = "Please enter a valid positive integer.";
                return;
            }

            // Calculate factorial using iterative method
            const iterFactorial = iterativeFactorial(number);
            factorialResult.textContent = `Iterative Factorial: ${iterFactorial}`;

            // Calculate factorial using recursive method
            const recFactorial = recursiveFactorial(number);
            recursiveResult.textContent = `Recursive Factorial: ${recFactorial}`;
        }

        // Iterative method for factorial
        function iterativeFactorial(n) {
            let result = 1;
            for (let i = 1; i <= n; i++) {
                result *= i;
            }
            return result;
        }

        // Recursive method for factorial
        function recursiveFactorial(n) {
            if (n === 0 || n === 1) {
                return 1;
            }
            return n * recursiveFactorial(n - 1);
        }
    </script>

</body>
</html>
