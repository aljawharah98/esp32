# esp32
#include <WiFi.h>
#include <HTTPClient.h>
const char* ssid = "your_SSID";
const char* password = "your_PASSWORD";

void setup() {
  Serial.begin(115200);

  
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("Connected to WiFi");
  HTTPClient http;

  http.begin("http://jsonplaceholder.typicode.com/todos/1"); 
  int httpCode = http.GET(); 

  if (httpCode > 0) {
    String payload = http.getString();
    Serial.println("Response:");
    Serial.println(payload);
  } else {
    
    Serial.printf("Error code: %d\n", httpCode);
  }

  http.end(); 

void loop() {
  }
