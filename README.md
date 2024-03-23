<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Quiz Game</title>
  <style>
    /* Your CSS styles here */
    body {
      font-family: Arial, sans-serif;
      text-align: center;
    }
    .quiz-container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background-color: #f9f9f9;
    }
    .options {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    button {
      margin-top: 10px;
      padding: 8px 20px;
      border: none;
      border-radius: 4px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body background="C:\Users\PUNTA\Pictures\Saved Pictures\quizbackground2.jpg">
<div class="quiz-container">
    <h1>Quiz </h1>
    <p id="question"></p>
    <div id="options" class="options"></div>
    <button id="prevBtn">Previous</button>
    <button id="submitBtn">Submit</button>
    <button id="nextBtn">Next</button>
    <p id="result" style="display: none;"></p>
    <p id="score" style="display: none;"></p>
    <p id="timer"></p>
  </div>
  <div id="thankYouScreen" style="display: none;">
     <h2>Thank You for Participating!</h2>
     <p id="remarks"></p>
     <p>Your Score: <span id="finalScore"></span> out of <span id="totalQuestions"></span></p>
</div>
  <script>
    // JavaScript code here
    const questions = [
      {
        question: "(1)  If England is written as 1234526 and france is written  as 78592, how if Greece coded ?",
        options: ["A) 381171", "B) 381191", "C) 234424", "D) 335343"],
        answer: "B) 381191"
      },
      {
        question: "(2)  In a row of boys facing North, A is sixteenth from the left end and C is sixteenth from the right end. B, who is fourth to the right of A, is fifth to the left of C in the row. How many boys are there in the row?",
        options: ["A) 37", "B) 36", "C) 40", "D) 42"],
        answer: "C) 40"
      },
      {
        question: "(3)  There is a certain relationship between the numbers on the either side of : : . Select a number from 3: 15: : 7: ? ",
        options: ["A) 35", "B) 36", "C) 61", "D) 42"],
        answer: "A) 35"
      },
      {
        question: "(4)  Pointing to a photograph, a women says, 'this man's son's sister is my mother in law.' How is the women's husband related to the man in the  photograph?",
        options: ["A) Grandson", "B) Son", "C) Son in law", "D) Nephew"],
        answer: "A) Grandson"
      },
      {
        question: "(5)  How many 5's are there in the given number of sequence which are immediately preceded by 7 and immediately followed by 6 ",
        options: ["A) One", "B) Two", "C) Three", "D) Four"],
        answer: "A) One"
      },
      {
        question: "(6)  Ritu and Priti starts from a fixed point. Ritu moves 5km westward and turns left and then covers 6km. Priti moves 7 km northward, turns left and walks 5km. The distance between Ritu and Priti now is",
        options: ["A) 10km", "B) 13km", "C) 8km", "D) 6km"],
        answer: "A) 13km"
      },
      {
        question: "(7) If the first half of the English alphabet is reversed and then next portion of English alphabet is reversed so as 'A' takes the position of 'M' and 'N' takes the position of 'Z' then which letter will be 6th to the left of 17th letter to the right of 7th letter from the left? ",
        options: ["A) U", "B) V", "C) B", "D) D"],
        answer: "B) V"
      },
      {
        question: "(8) A, B. C, D, E. F, G and H are sitting around a circle facing the centre. B is second to the right of D, who is third to the right of F. C is second to the left of A, who is second to the left of F. G is third to the right of E. Who is on the immediate right of A? ",
        options: ["A) B", "B) E", "C) F", "D) None of These"],
        answer: "B) E"
      },
      {
        question: "(9)  Kunal walks 10 kilometres towards North. From there, he walks 6 kilometres towards South. Then, he walks 3 kilometres towards East. How far and in which direction is he with reference to his starting point?",
        options: ["A) 5Km West", "B) 5km Northeast", "C) 7 km East", "D) None of These"],
        answer: "B) 5km Northeast"
      },
      {
        question: "(10)  If 'lead' is called 'stick', 'stick' is called 'nib', 'nib' is called 'needle' 'needle' is called 'rope' and 'rope' is called 'thread', what will be fitted in a pen to write with it?",
        options: ["A) stick", "B) lead", "C) needle", "D) nib"],
        answer: "C) needle"
      },
      {
        question: "(11)  Which of the following words cannot be  formed by using the letters of the given word: CONCCRETE",
        options: ["A) TREAT", "B) CONCERN", "C) TRAIN", "D) CENTER"],
        answer: "C) TRAIN"
      },
      {
        question: "(12)  Complete  the sequence - Clothes: Tailor: : Book: ? ",
        options: ["A) Dic", "B) CONCERN", "C) TRAIN", "D) CENTER"],
        answer: "C) TRAIN"
      },
      {
        question: "(13)  Complete  the sequence - Mill: Cloth: : Factory: ? ",
        options: ["A) Fiber", "B) Cement", "C) Textile", "D) Oil"],
        answer: "B) Cement"
      },
     {
        question: "(14)  Complete  the sequence - Degree: Temperature: : Joule: ? ",
        options: ["A) Force", "B) Work", "C) Newton", "D) Power"],
        answer: "B) Work"
      },
     {
        question: "(15)  2  4  8  16  _",
        options: ["A) 20", "B) 24", "C) 32", "D) 64"],
        answer: "C) 32"
      },
     {
        question: "(16)  2  6  12  20  _",
        options: ["A) 30", "B) 24", "C) 32", "D) 64"],
        answer: "A) 30"
      },
     {
        question: "(17)  149  4196  91625   _",
        options: ["A) 253649", "B) 276272", "C) 735633", "D) 162536"],
        answer: "D) 162536"
      },
     {
        question: "(18)  The HCF and LCM of two numbers are 84 and 21, respectively. If the ratio of the two numbers is 1:4, then the larger of the two numbers is:",
        options: ["A) 80", "B) 43", "C) 81", "D) 64"],
        answer: "C) 81"
      },
     {
        question: "(19)  What is difference is the place and face value of 3 in 456783",
        options: ["A) 0", "B) 1", "C) 2", "D) 3"],
        answer: "A) 0"
      },
     {
        question: "(20)  The sum of 3 + 3 * 3(4+3) is:",
        options: ["A) 38", "B) 43", "C) 81", "D) 66"],
        answer: "D) 66"
      },
     {
        question: "(21) How many prime numbers are there between 10 and 20 ?  ",
        options: ["A) 7", "B) 4", "C) 3", "D) 5"],
        answer: "B) 4"
      },
     {
        question: "(22)  Which of the following properties is incorrect qith respect to the property of whole numbers ?",
        options: ["A) Addition and subtraction are cummutative", "B) Division by 0 is not defined", "C) Multiplication is distributive over addition", "D) They are closed under addition and multiplication"],
        answer: "A) Addition and subtraction are cummultative"
      },
     {
        question: "(23) A bag contains 25-paise and 50-paise coins whose total value is Rs. 30. If the number of 25-paise coins is four times that of 50-paise coins, then find the number of each type of coins? ",
        options: ["A) 40 and 30", "B) 20 and 40", "C) 80 and 20", "D) 60 and 20"],
        answer: "C) 80 and 20"
      },
     {
        question: "(24) Fill in the blanks:  1 million=________ hundred thousand  ",
        options: ["A) One", "B) Ten", "C) Hundred", "D) Twenty"],
        answer: "A) One"
      },
     {
        question: "(25) Virat can type 28 words per minute. At this rate, how many words can Virat type iin 5.5 minutes ?  ",
        options: ["A) 154", "B) 157", "C) 159", "D) 162"],
        answer: "A) 154"
      },
     {
        question: "(26) Convert 5km into metre   ",
        options: ["A) 500m", "B) 5000m", "C) 50m", "D) 5m"],
        answer: "B) 5000m"
      },
     {
        question: "(27) The numbers which are multiples of 2 are:  ",
        options: ["A) odd", "B) even", "C) composite", "D) prime"],
        answer: "B) even"
      },
     {
        question: "(28) Where do we place the positive numbers on a vertical number line with respect to 0 ?  ",
        options: ["A) above", "B) left side", "C) right side", "D) below"],
        answer: "A) above"
      },
     {
        question: "(29) The easurement of an angle is 180. Which one of the following types of angle is this ?  ",
        options: ["A) Rigth angle", "B) Straigth angle", "C) Reflex angle", "D) None of these"],
        answer: "B) Straigth angle"
      },
     {
        question: "(30) A table cover measures 2.45m by 1.25m. Find its perimeter ?  ",
        options: ["A) 6.80m", "B) 7.40m", "C) 8.70m", "D) 7.70m"],
        answer: "B) 7.40m"
      },
     {
        question: "(31) Who among the following wrote sanskrit grammer ?  ",
        options: ["A) Kalidas", "B) Charak", "C) Panini", "D) Aryabhatt"],
        answer: "C) Panini"
      },
     {
        question: "(32) Which among the following headstreams meets ganga at the last  ?  ",
        options: ["A) Alakanda", "B) Pindar", "C) Mandakini", "D) Bhagirathi"],
        answer: "D) Bhagirathi"
      },
     {
        question: "(33) Patanjali is well known  for the compilation of ?  ",
        options: ["A) Yoga sutra", "B) Panchatantra", "C) Brahma sutra", "D) Ayurveda"],
        answer: "A) Yoga sutra"
      },
     {
        question: "(34) The country highest in barley production is  ?  ",
        options: ["A) China", "B) Russia", "C) India", "D) France"],
        answer: "B) Russia"
      },
     {
        question: "(35) Tsunami are caused by  ",
        options: ["A) Hurricans", "B) Earthquakes", "C) Undersea landslides", "D) None of these"],
        answer: "A) Hurricans"
      },
     {
        question: "(36) Which is  the hottest planet in our solar system ?  ",
        options: ["A) Mercury", "B) Venus", "C) Mars", "D) Jupiter"],
        answer: "B) Venus"
      },
     {
        question: "(37) Where was the electricity supply first introduced ?  ",
        options: ["A) Mumbai", "B) Dehradun", "C) Darjeeling", "D) Chennai"],
        answer: "C) Darjeeling"
      },
     {
        question: "(38) When was the battle of Plaseey fought ?  ",
        options: ["A) 1757", "B) 1758", "C) 1753", "D) 1755"],
        answer: "A) 1757"
      },
     {
        question: "(39) Which mughal emperor was famous as Zinda Pir ?  ",
        options: ["A) Shahjahan", "B) Akbar", "C) Aurangzeb", "D) Babar"],
        answer: "C) Aurangzeb"
      },
     {
        question: "(40) Who founded mauryan dynasty ?  ",
        options: ["A) Bindusara", "B) Chandragupta Maurya", "C) Ashoka", "D) Suryagupta Maurya"],
        answer: "B) Chandragupta Maurya"
      },
     {
        question: "(41) The area of a trapezium is 480 cm2, the distance between two parallel sides is 15 cm and one of the parallel side is 20 cm. The other parallel side is:  ?  ",
        options: ["A) 20cm", "B) 44cm", "C) 50cm", "D) 54"],
        answer: "B) 44"
      },
     {
        question: "(42)  The area of a rhombus is 240 cm  and one of the diagonals is 16 cm. Find the other diagonal.",
        options: ["A) 16cm", "B)  20cm", "C) 30cm", "D)  36m"],
        answer: "C) 30"
      },
     {
        question: "(43) The age of the father is three times the age of the son. If the age of the son is 15 years old, then the age of the father is:",
        options: ["A) 50 years", "B)  55 years", "C) 40 years", "D)  45 years"],
        answer: "D) 45 years"
      },
     {
        question: "(44) The difference between two whole numbers is 66. The ratio of the two numbers is 2: 5. The two numbers are",
        options: ["A) 60 and 6 ", "B)  100 and 33 ", "C)  110 and 44", "D)  45 and 3"],
        answer: "C)  110 and 44"
      },
     {
        question: "(45) Three consecutive integers add up 51. The integers are:",
        options: ["A) 16,17,18 ", "B)  15,16,17", "C) 17,18,19", "D)  18,19,20"],
        answer: "A)  16,17,18"
      },
     {
        question: "(46)  The solution for 3m = 5m – (8/5) is:",
        options: ["A) 8/5", "B) 4/5", "C) 5/4", "D) 5/7"],
        answer: "B)  4/5"
      },
     {
        question: "(47) If the weight of 12 sheets of thick paper is 40 grams, how many sheets of the same paper would weigh 2500 grams?",
        options: ["A) 750", "B) 800", "C) 532", "D) 400"],
        answer: "A)  750"
      },
     {
        question: "(48) 6 pipes are required to fill a tank in 1 hour 20 minutes. If we use 5 such types of pipes, how much time it will take to fill the tank?",
        options: ["A) 120 min", "B) 96 min", "C) 80 min", "D) 85 min"],
        answer: "B)  96 min"
      },
     {
        question: "(49) In a trapezium, the parallel sides measure 40 cm and 20 cm. Calculate the area of the trapezium if its non-parallel sides are equal having the lengths of 26 cm.",
        options: ["A) 750", "B) 800", "C) 720", "D) 400"],
        answer: "C)  720"
      },
     {
        question: "(50)  A cuboidal box of dimensions 1 m × 2 m × 1.5 m is to be painted except its bottom. Calculate how much area of the box has to be painted.",
        options: ["A) 11", "B) 15", "C) 19", "D) 21"],
        answer: "A)  11"
      },

    ];

 
  
    
    let currentQuestion = 0;
    let score = 0;
    let startTime = 0;
    const timePerQuestion = 3600;
    let timerInterval;

    const questionElement = document.getElementById("question");
    const optionsElement = document.getElementById("options");
    const resultElement = document.getElementById("result");
    const scoreElement = document.getElementById("score");
    const timerElement = document.getElementById("timer");
    const prevButton = document.getElementById("prevBtn");
    const nextButton = document.getElementById("nextBtn");
    const submitButton = document.getElementById("submitBtn");
    const thankYouScreen = document.getElementById("thankYouScreen");

    function startQuiz() {
      startTime = Date.now(); // Start time for the entire quiz
      startTimer(); // Start the timer for the first question
      loadQuestion(); // Load the first question
    }

    function startTimer() {
      timerInterval = setInterval(updateTimer, 1000);
    }

    function updateTimer() {
      const current = questions[currentQuestion];
      const elapsed = Math.floor((Date.now() - startTime) / 1000);
      const remaining = timePerQuestion - elapsed;

      if (remaining >= 0) {
        const minutes = Math.floor(remaining / 60);
        const seconds = remaining % 60;
        timerElement.textContent = `Time Left: ${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
      } else {
        clearInterval(timerInterval);
        showResult();
      }
    }

    function loadQuestion() {
      const current = questions[currentQuestion];
      questionElement.textContent = current.question;

      optionsElement.innerHTML = "";
      current.options.forEach(option => {
        const button = document.createElement("button");
        button.textContent = option;
        button.addEventListener("click", () => checkAnswer(option));
        optionsElement.appendChild(button);
      });

      updateButtons();
      resultElement.style.display = "none";
      scoreElement.style.display = "none";
    }

    function moveToQuestion(index) {
      if (index !== currentQuestion) {
        clearInterval(timerInterval);
      }
      currentQuestion = index;
      loadQuestion();
      startTimer();
    }

    function checkAnswer(selectedOption) {
      const current = questions[currentQuestion];
      const selectedAnswer = selectedOption.trim();
      const correctAnswer = current.answer.trim();

      if (selectedAnswer === correctAnswer) {
        score += 1;
      }

      if (currentQuestion === questions.length - 1) {
        showScore();
      } else {
        moveToQuestion(currentQuestion + 1);
      }
    }

    function showResult() {
      resultElement.style.display = "block";
      resultElement.textContent = `Result: ${score} out of ${questions.length}`;
      scoreElement.style.display = "block";
      scoreElement.textContent = `Your Score: ${score}`;
      timerElement.textContent = "Time's up!";
      updateButtons();
    }

    function updateButtons() {
      prevButton.disabled = currentQuestion === 0;
      nextButton.disabled = currentQuestion === questions.length - 1;
    }

    function showScore() {
      const totalQuestions = questions.length;
      const remarks = getRemarks(score, totalQuestions);

      thankYouScreen.style.display = "block";
      document.getElementById("finalScore").textContent = score;
      document.getElementById("totalQuestions").textContent = totalQuestions;
      document.getElementById("remarks").textContent = remarks;

      // Hide quiz container after showing the score
      document.querySelector(".quiz-container").style.display = "none";
    }

    function getRemarks(score, totalQuestions) {
      const percentage = (score / totalQuestions) * 100;

      if (percentage >= 80) {
        return "Excellent! You did great!";
      } else if (percentage >= 60) {
        return "Good job! Keep it up!";
      } else {
        return "You can do better. Try again!";
      }
    }

    window.onload = startQuiz;

    prevButton.addEventListener("click", () => moveToQuestion(currentQuestion - 1));
    nextButton.addEventListener("click", () => moveToQuestion(currentQuestion + 1));
    submitButton.addEventListener("click", () => showScore());
  </script>
</body>
</html>
