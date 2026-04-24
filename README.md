# weather
from tkinter import *
import requests

API_KEY = "f3a6de436bab1dd1c2dc45fe2bee0638"

def get_weather():
    city = city_entry.get()

    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric"

    response = requests.get(url)
    data = response.json()

    if data["cod"] != 200:
        result_label.config(text="City not found!")
        return

    temp = data["main"]["temp"]
    humidity = data["main"]["humidity"]
    weather = data["weather"][0]["description"]
    wind = data["wind"]["speed"]

    result = f"""
City: {city}

Temperature: {temp}°C
Humidity: {humidity}%
Weather: {weather}
Wind Speed: {wind} m/s
"""

    result_label.config(text=result)

root = Tk()
root.title("Weather App")
root.geometry("400x400")

Label(root, text="Weather App", font=("Arial", 18)).pack(pady=10)

city_entry = Entry(root, font=("Arial", 14))
city_entry.pack(pady=10)

Button(root, text="Get Weather", command=get_weather).pack(pady=10)

result_label = Label(root, text="", font=("Arial", 12), justify=LEFT)
result_label.pack(pady=20)

root.mainloop()
