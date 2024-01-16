# RESAT_Challenge
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RESAT 프론트엔드 개발 챌린지 2일차 미션</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }

        legend {
            text-align: center;
            font-size: 3em;
            font-weight: bold;
        }

        input[type=text] {
            border-radius:30%;
            background-color: antiquewhite;
        }

        #index{
            border-radius:10%;
            border-width: 1cap;
        }
        #timer {
            background-color: bisque;    
            border-radius:10%;
            border-width: 1cap;
        }
        
        #timerDisplay {
            font-size: 3em;
            margin-bottom: 10px;              
            text-align: center;
        }
        
        #inputTime {
            display: flex;
            justify-content: center;
            margin: 20px;
            text-align: center;
        }        
        
        #btnStart, #btnStop, #btnReset {
            background-color: bisque;
            border-radius:30%;
            font-size: 1em;
            font-weight: bold;
            margin: 60px;
            width : 100px;
            height: 100px;
        }
    </style>
</head>

<body>
    <fieldset id="index">
        <legend>카운트다운 타이머</legend>
        <div id="inputTime">
            <label for="hours"></label>
            <input type="text" id="hours" placeholder="시" style="text-align: center;"/>
            <p>:</p>    
            <label for="minutes"></label>
            <input type="text" id="minutes" placeholder="분" style="text-align: center;"/>
            <p>:</p>      
            <label for="seconds"></label>
            <input type="text" id="seconds" placeholder="초" style="text-align: center;"/>
        </div>
        <fieldset id = "timer">
                <div id = "timerDisplay">00:00:00</div>
        </fieldset>
        <div>
            <button id="btnStart" onclick="startTimer()">START</button>
            <button id="btnStop" onclick="stopTimer()">STOP</button>
            <button id="btnReset" onclick="resetTimer()">RESET</button> 
        </div>
    </fieldset>

    <script>
        let timer;
        let sumTime;

        function startTimer(){
            document.getElementById('inputTime').style.display = 'none';
            const inputHours = parseInt(document.getElementById('hours').value, 10) || 0;
            const inputMinutes = parseInt(document.getElementById('minutes').value, 10) || 0;
            const inputSeconds = parseInt(document.getElementById('seconds').value, 10) || 0;

            sumTime = inputHours * 3600 + inputMinutes * 60 + inputSeconds;

            if(sumTime <= 0){
                alert('시간을 다시 입력해 주세요.');
                resetTimer();
                return;
            }
            
            updateTimer();
            timer = setInterval(operateTimer, 1000);
        }

        function stopTimer(){
            clearInterval(timer);
        }

        function resetTimer(){
            clearInterval(timer);
            document.getElementById('timerDisplay').textContent = '00:00:00';
            document.getElementById('inputTime').style.display = 'flex';
            document.getElementById('hours').value = '';
            document.getElementById('minutes').value = '';
            document.getElementById('seconds').value = '';
        }

        function operateTimer(){
            if(sumTime > 0){
                sumTime--;
                updateTimer();
            } else {
                clearInterval(timer);
                resetTimer();
            }
        }

        function updateTimer(){
            const hours = Math.floor(sumTime / 3600);
            const minutes = Math.floor((sumTime % 3600) / 60);
            const seconds = sumTime % 60;
            const setTime = setZero(hours) + ':' + setZero(minutes) + ':' + setZero(seconds);
            document.getElementById('timerDisplay').textContent = setTime;
        }

        function setZero(time){
            return time < 10 ? '0' + time : time;
        }
    </script>
</body>
</html>
