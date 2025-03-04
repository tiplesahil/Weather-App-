# Weather-App-
import React, { useState } from "react";

export default function WeatherApp() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState(null);
  const API_KEY = "YOUR_API_KEY";

  const fetchWeather = async () => {
    if (!city) return;
    try {
      const response = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${API_KEY}`
      );
      const data = await response.json();
      setWeather(data);
    } catch (error) {
      console.error("Error fetching weather data", error);
    }
  };

  return (
    <div className="min-h-screen flex flex-col items-center justify-center bg-gray-900 text-white p-6">
      <h1 className="text-3xl font-bold mb-6">Weather App</h1>
      <div className="flex gap-4 mb-6">
        <input
          type="text"
          placeholder="Enter city"
          className="p-2 rounded text-black"
          value={city}
          onChange={(e) => setCity(e.target.value)}
        />
        <button
          onClick={fetchWeather}
          className="bg-blue-500 px-4 py-2 rounded text-white hover:bg-blue-600"
        >
          Get Weather
        </button>
      </div>
      {weather && weather.main ? (
        <div className="bg-gray-800 p-6 rounded-lg text-center">
          <h2 className="text-2xl font-semibold">{weather.name}</h2>
          <p className="text-lg">{weather.weather[0].description}</p>
          <p className="text-xl font-bold">{weather.main.temp}°C</p>
          <p>Humidity: {weather.main.humidity}%</p>
        </div>
      ) : (
        <p className="text-gray-400">Enter a city to get the weather</p>
      )}
    </div>
  );
}
