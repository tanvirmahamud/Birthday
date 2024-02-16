<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Countdown Timer</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f2f2f2;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    transition: background-color 1s ease-in-out;
  }
  #countdown {
    font-size: 2rem;
    color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #countdown div {
    margin: 0 10px;
    padding: 10px;
    background-color: #61a5c2; /* Blue */
    color: #fff;
    border-radius: 5px;
    min-width: 80px;
  }
  #countdown div:nth-child(2n) {
    background-color: #da4453; /* Red */
  }
  #countdown div:nth-child(3n) {
    background-color: #5cb85c; /* Green */
  }
  #countdown div:nth-child(4n) {
    background-color: #f6bb42; /* Yellow */
  }
  #countdown div span {
    display: block;
    font-size: 0.8rem;
    margin-top: 5px;
  }
  .message-button {
    font-size: 2rem;
    color: #333;
    margin-top: 20px;
    cursor: pointer;
    background-color: #FF69B4;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    transition: background-color 0.3s ease-in-out;
  }
  
  .message-button:hover {
    background-color: #ff4081;
  }
  
  #message {
    display: none;
  }
</style>
</head>
<body>
<div>
  <h1>Countdown Timer</h1>
  <div id="countdown"></div>
  <button id="message" class="message-button" onclick="showPersonalMessage()">Happy Birthday Fatiha!</button>
</div>

<script>
  // Function to calculate time remaining until today at 12:00 AM in Bangladesh time
  function getTimeRemaining() {
    const now = new Date();
    const utcOffset = now.getTimezoneOffset() * 60000; // Timezone offset in milliseconds
    const bdOffset = 360 * 60000; // Bangladesh timezone offset in milliseconds (UTC+6)
    const targetTime = new Date(now.getTime() + bdOffset - utcOffset); // Target time in Bangladesh timezone
    targetTime.setHours(0, 0, 0, 0); // Set to 12:00 AM

    const timeRemaining = targetTime - now;

    const seconds = Math.floor((timeRemaining / 1000) % 60);
    const minutes = Math.floor((timeRemaining / 1000 / 60) % 60);
    const hours = Math.floor((timeRemaining / (1000 * 60 * 60)) % 24);
    const days = Math.floor(timeRemaining / (1000 * 60 * 60 * 24));

    return {
      total: timeRemaining,
      days,
      hours,
      minutes,
      seconds
    };
  }

  // Function to display the countdown
  function initializeClock() {
    const countdown = document.getElementById('countdown');
    const messageButton = document.getElementById('message');

    function updateClock() {
      const t = getTimeRemaining();

      if (t.total <= 0) {
        clearInterval(timeinterval);
        countdown.style.display = 'none';
        messageButton.style.display = 'block';
        document.body.style.backgroundColor = '#FF69B4'; // Change background color to Pink
      } else {
        countdown.style.display = 'flex';
        messageButton.style.display = 'none';
        document.body.style.backgroundColor = '#f2f2f2'; // Reset background color
        countdown.innerHTML = `
          <div>${t.days}<span>days</span></div>
          <div>${t.hours}<span>hours</span></div>
          <div>${t.minutes}<span>minutes</span></div>
          <div>${t.seconds}<span>seconds</span></div>
        `;
      }
    }

    updateClock(); // run function once at first to avoid delay

    // update the clock every second
    const timeinterval = setInterval(updateClock, 1000);
  }

  function showPersonalMessage() {
    const personalMessage = "Happy Birthday, Fatiha! 🎉🎂 May your day be filled with love, laughter, and all the things that bring you joy. Wishing you a year ahead filled with blessings, success, and unforgettable moments. Enjoy your special day to the fullest!";
    alert(personalMessage);
  }

  initializeClock();
</script>
</body>
</html>
