# Quiz-App
name- shyam bhavee
Email - shyam7322041088@gmail.com
# Quiz -Application
Learning how to build a website with js, HTML and CSS
# HTML code
<!DOCTYPE html>
<html>
    <head>
        <title>Quize App - Easy Tutorials</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <div class="app">
            <h1>Simple Quize</h1>
            <div class="Quize">
                <h2 id="question">Question goes here</h2>
                <div id="answer-buttons">
                    <button class="btn">Answer 1</button>
                    <button class="btn">Answer 2</button>
                    <button class="btn">Answer 3</button>
                    <button class="btn">Answer 4</button>
                </div>
                <button id="next-btn">Next</button>
            </div>

        </div>
        <script src="script.js"></script>
    </body>
</html>

# css- file

* {
    margin: 0;
    padding: 0;
    font-family: 'poppins',sans-serif;
    box-sizing: border-box;
}
body{
    background-color: #001e4d;
}
.app{
    background-color: #fff;
    width: 90%;
    max-width: 600px;
    margin: 100px auto 0;
    border-radius: 10px;
    padding: 30px;
}
.app h1{
    font-size: 25px;
    color: #001e4d;
    font-weight: 600;
    border-bottom: 1px solid#333;
    padding-bottom: 30px;

}
.quiz{
    padding: 20px 0;
}
.quiz h2{
    font-size: 18px;
    color: #001e4d;
    font-weight: 600;
}
.btn{
    background: #fff;
    color: #222;
    font-weight: 500;
    width: 100%;
    border: 1px solid #222;
    padding: 10px;
    margin: 10px 0;
    text-align: left;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
}
.btn:hover:not([disabled]){
    background: #222;
    color: #fff;

}
.btn:disabled{
    cursor: no-drop;
}
#next-btn{
    background: #001e4d;
    color: #fff;
    font-weight: 500;
    width: 150px;
    border: 0;
    padding: 10px;
    margin: 20px auto 0;
    border-radius: 4px;
    cursor: pointer;
    display: none;
}
.correct{
    background: #9aeabc;
}
.incorrect{
    background: #ff9393;
}

# js - file

const questions = [
    {
        question: "Who is the father of Computers?",
        answers: [
            { text: "James Gosling",correct: false},
            { text: "Charles Babbage",correct: true},
            { text: "Dennis Ritchie",correct: false},
            { text: "Bjarne Stroustrup",correct: false},

        ]
    },
    {
        question: "What is the full form of CPU?",
        answers: [
            { text: "Computer Processing Unit",correct: false},
            { text: "Central Processing Unit",correct: true},
            { text: "Computer Principle Unit",correct: false},
            { text: "Control Processing Unit",correct: false},

        ]
    },
    {
        question: "Which of the following language does the computer understand?",
        answers: [
            { text: "Computer understands only C Language",correct: false},
            { text: " Computer understands only Assembly Language",correct: false},
            { text: "Computer understands only Binary Language",correct: true},
            { text: "Computer understands only BASIC",correct: false},

        ]
    },
    {
        question: "Which of the following computer language is written in binary codes only?",
        answers: [
            { text: "pascal",correct: false},
            { text: "machine language",correct: true},
            { text: "c",correct: false},
            { text: "c#",correct: false},
        

        ]
    },
    {
        question: " Which of the following is the brain of the computer?",
        answers: [
            { text: "Central Processing Unit",correct: true},
            { text: "Memory",correct: false},
            { text: "Arithmetic and Logic unit",correct: false},
            { text: "Control unit",correct: false},

        ]
    },
    {
        question: " Which of the following is the smallest unit of data in a computer?",
        answers: [
            { text: "Bit",correct: true},
            { text: "nibbal",correct: false},
            { text: "KB",correct: false},
            { text: "byte",correct: false},

        ]
    },
    {
        question: " Which of the following is not a type of computer code?",
        answers: [
            { text: "EDIC",correct: true},
            { text: "ASCII",correct: false},
            { text: " BCD",correct: false},
            { text: "EBCDIC",correct: false},

        ]
    },
    {
        question: " Which of the following are physical devices of a computer?",
        answers: [
            { text: "Hardware",correct: true},
            { text: "Software",correct: false},
            { text: "System Software",correct: false},
            { text: "Package",correct: false},

        ]
    },
    {
        question: " Which of the following can access the server?",
        answers: [
            { text: " Web Client",correct: true},
            { text: " User",correct: false},
            { text: "Web Browser",correct: false},
            { text: "Web Server",correct: false},

        ]
    },
    {

    question: "Which of the following is the first neural network computer?",
        answers: [
            { text: "AM",correct: false},
            { text: "AN",correct: false},
            { text: " SNARC",correct: true},
            { text: "RFD",correct: false},

        ]
    },
    {
        question: "A computer system includes",
        answers: [
            { text: "Hardware",correct: false},
            { text: "Software",correct: false},
            { text: "Peripheral devices",correct: false},
            { text: "All of these",correct: true},

        ]
    }
];

const questionElement = document.getElementById("question");
const answerButton = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz(){
    currentQuestionIndex = 0;
    score = 0;
    nextButton.innerHTML = "Next";
    showQuestion();


}

function showQuestion(){
    resetState();
    let currentQuestion = questions[currentQuestionIndex];
    let questionNo = currentQuestionIndex + 1;
    questionElement.innerHTML = questionNo + ". " + currentQuestion.question;

    currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.text;
        button.classList.add("btn");
        answerButton.appendChild(button);
        if(answer.correct){
            button.dataset.correct = answer.correct;
        }
        button.addEventListener("click", selectAnswer);
        
    });
}

function resetState(){
    nextButton.style.display  = "none";
    while(answerButton.firstChild){
        answerButton.removeChild(answerButton.firstChild)
        
    }
}

function selectAnswer(e){
    const selectedBtn = e.target;
    const isCorrect = selectedBtn.dataset.correct === "true";
    if(isCorrect){
        selectedBtn.classList.add("correct");
        score++;

    }else{
        selectedBtn.classList.add("incorrect");

    }
    Array.from(answerButton.children).forEach(button => {
        if(button.dataset.correct === "true"){
            button.classList.add("correct");

        }
        button.disabled = true;
    });
    nextButton.style.display = "block";
} 

function showScore(){
    resetState();
    questionElement.innerHTML = `you scored ${score} out of ${question.length}!`;
    nextButton.innerHTML = "play Again";
    nextButton.style.display = "block";
}

function handleNextButton(){
    currentQuestionIndex++;
    if(currentQuestionIndex < questions.length){
        showQuestion();
    }else{
        showScore();
    }
}

nextButton.addEventListener("click", ()=>{
    if(currentQuestionIndex < questions.length){
        handleNextButton();

    }else{
        startQuiz();
    }
})

startQuiz();

