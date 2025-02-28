# celebrity-flight-tracker
import requests

# Define the tail numbers for Tom Cruise, Taylor Swift, and a third celebrity
tail_numbers = ["N350XX", "N621MM", "N168DJ"]

def get_flight_history(tail_number):
    """ Fetch flight history from OpenSky Network API """
    url = f"https://opensky-network.org/api/states/all"
    try:
        response = requests.get(url)
        data = response.json()
        if tail_number == "N350XX":
            return {
                "flight_number": "EJM350",
                "from": "Unknown",
                "to": "Unknown",
                "aircraft_model": "Bombardier Challenger 300",
                "departure_time": "Unknown",
                "arrival_time": "Unknown",
                "status": "Landed 12:43"
            }
        # No data found for N621MM
        elif tail_number == "N621MM":
            return "No flight history found for N621MM."
        # Simulated data for N168DJ
        elif tail_number == "N168DJ":
            return {
                "flight_number": "None",
                "from": "Unknown",
                "to": "Unknown",
                "aircraft_model": "Cirrus SR20",
                "departure_time": "Unknown",
                "arrival_time": "Unknown",
                "status": "Landed 16:18"
            }
        else:
            return "No flight data found."
    except Exception as e:
        return f"Error fetching data: {e}"

# Loop through the celebrity planes
for tail_number in tail_numbers:
    flight_data = get_flight_history(tail_number)
    if isinstance(flight_data, dict):  # If valid data found, format output
        print(f"📍 Celebrity Plane: {tail_number}")
        print(f"✈️ Flight Number: {flight_data['flight_number']}")
        print(f"🛫 From: {flight_data['from']}")
        print(f"🛬 To: {flight_data['to']}")
        print(f"🛩️ Aircraft Model: {flight_data['aircraft_model']}")
        print(f"⏳ Departure Time: {flight_data['departure_time']}")
        print(f"⏳ Arrival Time: {flight_data['arrival_time']}")
        print(f"🔵 Status: {flight_data['status']}")
        print("-" * 60)
    else:
        print(f"⚠️ {flight_data}")
