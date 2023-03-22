# Applications-of-Threading-in-real-life
                                          Digital Watch App:
   
   - Problem: 
A digital watch application needs to provide the user with some information such as the time, date, and weather but the weather information is fetched from an external API and can take several seconds to load, causing the UI to lag.  
    - Solution: 
Multi-threading can be used to fetch the weather information in the background without blocking the UI. So, that the user can navigate and use the interface while other features are running in the background without causing any delay or lag. Here's an example of how this can be done in Java:


public class WatchApp {
    public static void main(String[] args) {
        // Start the UI thread
        new Thread(() -> {
            while (true) {
                // Update the UI with the current time and date
                updateTime();
                updateDate();
                
                try {
                    // Sleep for one second before updating again
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
        
        // Start the weather thread
        new Thread(() -> {
            while (true) {
                // Fetch the weather information from the API
                WeatherInfo weather = fetchWeather();
                
                // Update the UI with the weather information
                updateWeather(weather);
                
                try {
                    // Sleep for 5 minutes before fetching again
                    Thread.sleep(300000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }
    
    private static void updateTime() {
        // Update the time display on the UI
    }
    
    private static void updateDate() {
        // Update the date display on the UI
    }
    
    private static WeatherInfo fetchWeather() {
        // Fetch the weather information from the API
    }
    
    private static void updateWeather(WeatherInfo weather) {
        // Update the weather display on the UI
    }
}


  - Explanation:
This app uses two threads: one for updating the time and date on the UI, and another for fetching the weather information in the background.
The UI thread updates the time and date every second, while the weather thread fetches the weather information every 5 minutes and updates the UI.

                                            Smart TV App: 

A Smart TV application works as follows: process user inputs and stream video content simultaneously.
- Problem: 
The video decoder can block the UI thread. As a consequence, the app might  become unresponsive.
- Solution:
To solve the problem we can use Multi-threading. It will process user inputs and stream video content on separate threads.
Here's an example of how this can be done in Android:


public class TvApp extends Activity {
    private VideoPlayer videoPlayer;
    private InputProcessor input processor;
    
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        // Create the video player and input processor
        videoPlayer = new VideoPlayer();
        inputProcessor = new InputProcessor();
        
        // Start the video thread
        new Thread(() -> {
            while (true) {
                // Decode and play the next video frame
                videoPlayer.playNextFrame();
            }
        }).start();
        
        // Start the input thread
        new Thread(() -> {
            while (true) {
                // Process the next user input
                inputProcessor.processInput();
            }
        }).start();
    }
    
    private class VideoPlayer {
        public void playNextFrame() {
            // Decode and play the next video frame
        }
    }
    
    private class InputProcessor {
        public void processInput() {
            // Process the next user input
        }
    }
}

   - Explanation:

This code is an example of how multi-threading can be used in a TV app to concurrently perform different tasks. The app creates two threads: one for video playback and one for processing user input.
The VideoPlayer thread runs continuously in a loop, decoding and playing the next video frame. The InputProcessor thread also runs continuously in a loop, processing the next user input. By using multi-threading, both tasks can be performed concurrently without blocking each other, which allows for a better user experience.
