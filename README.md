# Weather App

> A simple Android weather application built with Kotlin, utilizing the OpenWeatherMap API to provide real-time weather data.

## Table of Contents

- [About](#about)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [Contact](#contact)

## About

Weather App is an Android application developed in Kotlin that fetches and displays weather information for different cities using the OpenWeatherMap API. The app allows users to search for a city's weather and provides details such as temperature, humidity, wind speed, sunrise and sunset times, and weather conditions.

## Features

- Fetch and display current weather data for any city.
- Search functionality to find weather data for specific cities.
- Real-time updates of weather conditions.
- Dynamic background and animations based on weather conditions.
- Displays detailed weather metrics including temperature, humidity, wind speed, sunrise, and sunset times.

## Installation

To run this project locally, follow these steps:

1. **Clone the repository:**
    ```bash
    git clone https://github.com/akeelshafi/weather-app.git

    ```
2. **Open the project in Android Studio:**
    - Start Android Studio and select "Open an existing project".
    - Navigate to the cloned repository folder and open it.

3. **Install dependencies:**
    - The project uses Retrofit and Gson for network calls and data parsing, which are included in the `build.gradle` file.
    - Ensure you have an active internet connection to download the required libraries.

4. **Set up the OpenWeatherMap API key:**
    - Obtain an API key from [OpenWeatherMap](https://openweathermap.org/api).
    - Replace `YOUR_API_KEY` in the `fetchWeatherData` method with your actual API key.

## Usage

1. **Launch the application:**
    - Run the application on an emulator or physical device from Android Studio.

2. **Search for a city's weather:**
    - Use the search bar to input the name of a city and get real-time weather data.

## MainActivity Code Snippet
Here’s a brief overview of the `MainActivity` code:
```kotlin
class MainActivity : AppCompatActivity() {
    private val binding: ActivityMainBinding by lazy {
        ActivityMainBinding.inflate(layoutInflater)
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(binding.root)

        fetchWeatherData("sopore")
        searchCity()
    }

    private fun searchCity() {
        val searchView = binding.searchView
        searchView.setOnQueryTextListener(object : SearchView.OnQueryTextListener {
            override fun onQueryTextSubmit(query: String?): Boolean {
                if (query != null) {
                    fetchWeatherData(query)
                }
                return true
            }

            override fun onQueryTextChange(newText: String?): Boolean {
                return true
            }
        })
    }

    private fun fetchWeatherData(cityName: String) {
        val retrofit = Retrofit.Builder()
            .addConverterFactory(GsonConverterFactory.create())
            .baseUrl("https://api.openweathermap.org/data/2.5/")
            .build().create(ApiInterface::class.java)

        val response = retrofit.getWeatherDate(cityName, "YOUR_API_KEY", "metric")
        response.enqueue(object : Callback<WeatherApp> {
            override fun onResponse(call: Call<WeatherApp>, response: Response<WeatherApp>) {
                val responseBody = response.body()
                if (response.isSuccessful && responseBody != null) {
                    updateUI(responseBody, cityName)
                }
            }

            override fun onFailure(call: Call<WeatherApp>, t: Throwable) {
                // Handle failure
            }
        })
    }

    private fun updateUI(responseBody: WeatherApp, cityName: String) {
        // Update UI elements with weather data
    }
}
```
## Contributing

Contributions are welcome! To contribute to this project, follow these steps:

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a pull request.

## Contact

- **Developer**: Akeel shafi
- **Email**: akeelshafi20@gmail.com
- **Project Link**:https://github.com/akeelshafi/WeatherApp


