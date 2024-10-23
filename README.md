# Open-Weather-API-kEY
# Index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Weather App</h1>
        <input type="text" id="cityInput" placeholder="Enter city name...">
        <button id="getWeatherBtn">Get Weather</button>
        <div id="weatherInfo"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>

# css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}

.container {
    width: 300px;
    margin: 50px auto;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

h1 {
    color: #333;
}

input[type="text"] {
    width: calc(100% - 22px);
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    width: 100%;
    padding: 10px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background: #0056b3;
}

#weatherInfo {
    margin-top: 20px;
    display: none;
}

.weather {
    background: #e9ecef;
    border-radius: 4px;
    padding: 10px;
    color: #333;
}

# js
const apiKey = 'YOUR_API_KEY'; // Replace with your OpenWeatherMap API key
const getWeatherBtn = document.getElementById('getWeatherBtn');
const cityInput = document.getElementById('cityInput');
const weatherInfo = document.getElementById('weatherInfo');

getWeatherBtn.addEventListener('click', getWeather);

async function getWeather() {
    const cityName = cityInput.value.trim();
    if (cityName === '') {
        alert('Please enter a city name!');
        return;
    }

    const url = `https://api.openweathermap.org/data/2.5/weather?q=${cityName}&appid=${apiKey}&units=metric`;

    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error('City not found');
        }
        const data = await response.json();
        displayWeather(data);
    } catch (error) {
        alert(error.message);
    }
}

function displayWeather(data) {
    const { name, main, weather } = data;
    const weatherDescription = weather[0].description;
    const temperature = main.temp;

    weatherInfo.innerHTML = `
        <div class="weather">
            <h2>${name}</h2>
            <p>Temperature: ${temperature} °C</p>
            <p>Condition: ${weatherDescription}</p>
        </div>
    `;
    weatherInfo.style.display = 'block';
}
