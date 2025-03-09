# Weather Station MQTT Dashboard

A real-time weather monitoring system that collects temperature and humidity data via MQTT, stores it in a SQLite database, and displays it through an interactive web dashboard.

![Weather Station Dashboard](https://i.imgur.com/placeholder-image.jpg)

## Features

- **Real-time Data Monitoring**: Displays live temperature and humidity readings from MQTT sensors
- **Historical Data Tracking**: Stores all readings in a SQLite database for historical analysis
- **5-Minute Averages**: Automatically calculates and displays 5-minute average values
- **Interactive Charts**: Visualizes environmental trends with responsive charts
- **Responsive Design**: Works on desktop and mobile devices
- **Database Viewer**: Built-in interface to view raw and averaged data

## Technology Stack

- **Frontend**: HTML, CSS, JavaScript
- **Data Visualization**: Chart.js
- **Real-time Communication**: MQTT over WebSockets
- **HTTP Requests**: Axios
- **Backend**: Node.js with Express
- **Database**: SQLite3
- **Icons**: Font Awesome

## Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- npm (usually comes with Node.js)
- An MQTT broker (this project is configured to use a WebSocket connection to an MQTT broker)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/weather-mqtt-app.git
   cd weather-mqtt-app
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Configure the MQTT connection:

   - Open `public/index.html`
   - Find the line with `mqtt.connect` and update the WebSocket URL to your MQTT broker:
     ```javascript
     const mqttClient = mqtt.connect('ws://your-mqtt-broker-address:port');
     ```
   - Update the MQTT topics if needed:
     ```javascript
     mqttClient.subscribe('/your/temperature/topic');
     mqttClient.subscribe('/your/humidity/topic');
     ```

4. Start the server:

   ```bash
   node server.js
   ```

5. Access the dashboard:
   - Open your browser and navigate to `http://localhost:3000`

## Project Structure

```
weather-mqtt-app/
├── server.js                # Main server file with Express and SQLite setup
├── weather_data.db          # SQLite database (created on first run)
├── public/                  # Static files served by Express
│   ├── index.html           # Main dashboard interface
│   └── [other static files] # Any additional static files
├── package.json             # Project dependencies
└── README.md                # This file
```

## How It Works

1. **Data Collection**: The system connects to an MQTT broker via WebSockets and subscribes to temperature and humidity topics.

2. **Data Storage**: When new data arrives, it's displayed immediately on the dashboard and sent to the server via an API call, which stores it in the SQLite database.

3. **Data Processing**: The server calculates 5-minute averages of temperature and humidity readings and stores them in a separate table.

4. **Data Visualization**: The dashboard fetches the latest readings and historical averages from the server and displays them using Chart.js.

## API Endpoints

- `POST /api/weather/data`: Store new temperature or humidity readings
- `GET /api/weather/current`: Get the most recent temperature and humidity readings
- `GET /api/weather/history`: Get historical 5-minute averages (last hour)
- `GET /db-viewer`: View the database interface
- `GET /db-viewer/raw-data`: View raw data table
- `GET /db-viewer/avg-data`: View averaged data table

## Customization

### Changing the Port

The default port is 3000. To change it, modify the `PORT` variable in `server.js`:

```javascript
const PORT = process.env.PORT || 3000;
```

### Styling the Dashboard

The dashboard styling is contained within the `<style>` section of `public/index.html`. You can modify the CSS variables at the top to change the color scheme:

```css
:root {
	--primary-color: #2563eb;
	--secondary-color: #4f46e5;
	--temp-color: #dc2626;
	--humidity-color: #0284c7;
	/* other variables */
}
```

## Troubleshooting

### MQTT Connection Issues

- Ensure your MQTT broker is running and accessible
- Check that the WebSocket URL is correct
- Verify that the MQTT topics match what your sensors are publishing

### Database Issues

- If you encounter database errors, try deleting the `weather_data.db` file and restarting the server
- Check the server console for specific error messages

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [Chart.js](https://www.chartjs.org/) for the charting library
- [MQTT.js](https://github.com/mqttjs/MQTT.js) for the MQTT client
- [Express](https://expressjs.com/) for the web server
- [SQLite](https://www.sqlite.org/) for the database
