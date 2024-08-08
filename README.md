<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ABM Interactive Business Simulation</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <div id="introPage" class="intro-page">
            <h1>Welcome to the ABM Interactive Business Simulation</h1>
            <p>This quiz will test your business decision-making skills in various situational contexts. Are you ready?</p>
            <button onclick="startQuiz()">Start Quiz</button>
        </div>

        <div id="quizPage" class="quiz-page hidden">
            <div class="question-container">
                <h2 id="question">Question will appear here</h2>
                <div id="options">
                    <!-- Options will be dynamically loaded here -->
                </div>
            </div>
            <button id="nextBtn" class="hidden" onclick="nextQuestion()">Next</button>
        </div>

        <div id="resultPage" class="result-page hidden">
            <h1>Congratulations!</h1>
            <p id="score"></p>
            <p>Thank you for participating in the simulation.</p>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: 'Arial', sans-serif;
    background: linear-gradient(to right, #74ebd5, #ACB6E5);
    color: #333;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
}

.container {
    width: 80%;
    max-width: 600px;
    padding: 20px;
    background-color: white;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
}

.hidden {
    display: none;
}

.intro-page h1, .result-page h1 {
    color: #555;
    margin-bottom: 20px;
}

.question-container {
    margin-bottom: 20px;
}

#options {
    display: flex;
    flex-direction: column;
}

button {
    background-color: #74ebd5;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 20px;
    font-size: 16px;
}

button:hover {
    background-color: #ACB6E5;
}
const questions = [
    {
        question: "You’re in charge of inventory management. You notice that a particular item isn't selling well. What should you do?",
        options: ["Order more of the item", "Reduce the price", "Discontinue the item", "Promote the item with ads"],
        correct: 1
    },
    // Add 29 more questions here
    // Example format:
    // {
    //     question: "Another situational question?",
    //     options: ["Option 1", "Option 2", "Option 3", "Option 4"],
    //     correct: 2
    // },
];

let currentQuestion = 0;
let score = 0;

function startQuiz() {
    document.getElementById('introPage').classList.add('hidden');
    document.getElementById('quizPage').classList.remove('hidden');
    showQuestion();
}

function showQuestion() {
    const questionObj = questions[currentQuestion];
    document.getElementById('question').textContent = questionObj.question;

    const optionsDiv = document.getElementById('options');
    optionsDiv.innerHTML = '';

    questionObj.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.textContent = option;
        button.onclick = () => checkAnswer(index);
        optionsDiv.appendChild(button);
    });
}

function checkAnswer(selectedIndex) {
    const correctIndex = questions[currentQuestion].correct;
    if (selectedIndex === correctIndex) {
        score++;
    }

    document.getElementById('nextBtn').classList.remove('hidden');
}

function nextQuestion() {
    currentQuestion++;
    if (currentQuestion < questions.length) {
        showQuestion();
        document.getElementById('nextBtn').classList.add('hidden');
    } else {
        showResults();
    }
}

function showResults() {
    document.getElementById('quizPage').classList.add('hidden');
    document.getElementById('resultPage').classList.remove('hidden');
    document.getElementById('score').textContent = `You scored ${score} out of ${questions.length}.`;
}
