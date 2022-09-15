<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Guess Game</title>
    <link href="https://fonts.googleapis.com/css2?family=Carter+One&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        header {
            width: 100%;
            line-height: 15vh;
            background-color: #20bf6b;
        }

        h1 {
            text-align: center;
            color: white;
            font-size: 1.8rem;
            letter-spacing: 15px;
            text-transform: uppercase;
            font-family: 'Carter One', cursive;
            text-shadow: 0 1px 0 #efefef,
                0 2px 0 #efefef,
                0 3px 0 #efefef,
                0 4px 0 #efefef,
                0 30px 50px rgba(0, 0, 0, .1);
        }

        section {
            height: 85vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #7bed9f;
        }

        .gameArea {
            width: 50%;
            height: 400px;
            padding: 20px 0;
            background-color: #2ed573;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        h3 {
            text-align: center;
            font-size: 1.5rem;
        }

        input {
            width: 40%;
            padding: 15px 0;
            text-align: center;
            border-radius: 25px;
            outline: none;
            border: none;
            background-color: #dff9fb;
            color: black;
            margin: 2rem 0;
            font-size: 1.1rem;
        }

        button {
            font-size: 1rem;
            cursor: pointer;
            outline: none;
            border: #2f3542;
            margin-top: 10px;
            color: #eb4d4b;
            border-radius: 25px;
        }

        button.btn {
            font-weight: 600;
            padding: 1rem 2rem;
            background-color: white;
            text-transform: uppercase;
            transition-property: all;
            transition-duration: 0.5s;
            transition-timing-function: cubic-bezier(0.65, -0.25, 0.25, 1.95);
        }

        button.btn:hover,
        button.btn:focus,
        button.btn:active {
            letter-spacing: 0.125rem;
            word-spacing: 0.2rem;
        }

        .hidden {
            display: none;
        }
    </style>

</head>

<body>
    <div class="container">
        <header>
            <h1>Guess The Word Game</h1>
        </header>
        <section>
            <div class="gameArea">
                <h3 class="msg"></h3>
                <input type="text" class="hidden">
                <button class="btn">Click here to Start</button>
            </div>
        </section>
    </div>
    <script>
        const msg = document.querySelector(".msg");
        const guess = document.querySelector("input");
        const btn = document.querySelector(".btn");
        let play = false;
        let sWords = ['java', 'python', 'javascript', 'html', 'css', 'nodejs', 'reactjs', 'angular', 'android', 'sql', 'mysql']
        let newWords = "";
        let randWords = "";


        const createNewWords = () => {
            let ranNum = Math.floor(Math.random() * sWords.length); // creating i value
            // console.log(ranNum);
            let newTempSwords = sWords[ranNum];   //sWords[i]
            // console.log(newTempSwords.split(''));
            return newTempSwords;
        }

        const scrambleWords = (arr) => {
            for (let i = arr.length - 1; i >= 0; i--) {
                let temp = arr[i];
                // console.log(temp);
                let j = Math.floor(Math.random() * (i + 1))
                // console.log(i);
                // console.log(j);
                arr[i] = arr[j];
                arr[j] = temp;
            }
            return arr;
        }

        btn.addEventListener('click', function () {
            if (!play) {
                play = true;
                btn.innerHTML = "Guess";
                guess.classList.toggle('hidden');
                newWords = createNewWords();
                randWords = scrambleWords(newWords.split("")).join("");
                // console.log(randWords.join(""));
                msg.innerHTML = `Guess the Given Word : ${randWords}`;
            }
            else {
                let tempWord = guess.value;
                if (tempWord === newWords) {
                    // console.log('correct');
                    play = false;
                    msg.innerHTML = `Awesome It's Correct. It is ${newWords}`;
                    btn.innerHTML = "Start Again";
                    guess.classList.toggle('hidden');
                    guess.value = "";


                } else {
                    // console.log('incorrect');
                    msg.innerHTML = `Sorry Boss... It's not Correct. Plz Try Again ${randWords}`
                }
            }

        })
    </script>
</body>

</html>
