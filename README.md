import requests

def get_weather():
    city = input("Enter City Name: ")
    
    api_key ="fae74e03d4752d27dc7676f0d237988e" 
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

    try:
        response = requests.get(url)
        data = response.json()

    
        if response.status_code == 200:
            temp = data['main']['temp']
            desc = data['weather'][0]['description']
            print(f"\n✅ Weather in {city}: {temp}°C, {desc}")
        
        elif response.status_code == 401:
            print("❌ Error 401: Your API Key is not active yet. Wait 30-60 mins!")
        elif response.status_code == 404:
            print("❌ Error 404: City not found. Check spelling!")
        else:
            print(f"❌ Error {response.status_code}: {data.get('message')}")

    except Exception as e:
        print(f"❌ Connection Error: {e}")

get_weather()
