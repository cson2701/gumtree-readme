# The weather app

The app was completed in Kotlin and  Jetpack Compose.

#### Search by city name or postcode

1. Type city name or postcode into the searchbar (**TextField**) on the top, which will call an API to `http://api.openweathermap.org/geo/1.0/direct?q={city name},{state code},{country code}&limit={limit}&appid={API key}` if the search term is a city, or `http://api.openweathermap.org/geo/1.0/zip?zip={zip code},{country code}&appid={API key}` if the search term is a city. The API will return a maximum of 5 matches. The results will be populated into a `LazyColumn`.
2. The `TextField` has a **debouce** time of 450ms to prevent too many API calls. 
3. Select one from the results, a new Activity will open with weather details of the selected city. 

#### View weather details

The weather details of the selected city will be displayed. Including the **city name**, **current temperature**, **weather condition** and its **icon**, **highest** and **lowest temperature**. 

#### Recent searched locations

1. Whenever a search result has been selected, it will be saved to the app’s `SharedPreferences`. A maximum of 10 recent searches can be saved. 
2. When there are more than 10 recent searches, the oldest one will be removed. 
3. The recent searches items are inplemented using `FlowRow`.
4. The location won’t be added to recent searches if it already exists, and will be brought to front after selecting. 
5. To **remove** a recent search, tap the **bin** icon, and it will change to a filled state, meaning it is now in removing state, a “✕” will be displayed next to each item. Tap the item to remove it. Tap the filled **bin** icon to return to normal state. 
6. In case there are two or more locations with the same name but from different countries, hold the item to reveal its country. 
7. Recent searches section are hidden when there are no recent searches or the search bar has inputs. 

#### Error handling

1. There is a `cod`, and `message` in the Models of location and weather. when the APIs return an error with a code and a message, such as the entered postcode is invalid or not found, it will be displayed.
2. If there is an error caused by something else, such as when there is no connection, the `customMessage` will be used to display a message.

#### Unit test

Unit tests are made to test against parsing the JSON payloads and make sure the correct results/message are returned. The tese cases include:

- Searching for a city/postcode.
- Searching for a non-existing city/postcode.
- Fetching weather details by latitude and longitude.
- Fetching weather details by wrong latitude or longitude.
- Returning correct message (without crashing) when there is no connection. 

#### Third-party libraries

1. **[OkHttp](https://square.github.io/okhttp/)** to handle HTTP requests. 
2. [**Gson**](https://github.com/google/gson) to parse JSON payloads. 
3. [**Coil**](https://coil-kt.github.io/coil/compose/) to load images.
4. [**Truth**](https://truth.dev/) to make assertions more straightfoward and human readable in unit tests. 
