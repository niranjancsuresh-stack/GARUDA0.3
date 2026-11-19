# G.A.R.U.D.A.

**Ground-link Automated Receiver & Unified Data Analyzer**

Plug in, test, calibrate, take data.

Created by Niranjan CS.

## How it works

1. Open `index.html`. A welcome window shows the logo, the name and two options.
2. Pick **CubeSat Testing Lab** or **CubeSat Telemetry**.
3. Fill in your details, then the page opens:
   - Testing Lab asks: team name, team ID, lab name, CubeSat name.
   - Telemetry asks: team name, team ID, your name (person on duty), CubeSat name.

Your details are saved on your computer and added to every download (CSV, JSON, Excel, logs) together with the date and time.

## CubeSat Testing Lab

Small tab buttons run across the top:

| Tab | What it does |
| --- | --- |
| **Sensor Check** | A live checklist: battery charge, signal, temperature, humidity, accelerometer, gyroscope, magnetometer, heading, altimeter, GPS and reaction wheel. Each one turns green when it is sending good data, and shows every reading. Raw data and the latest serial lines are shown next to it. |
| **Altimeter** | Step by step: set ground level, lift it up, bring it back down. |
| **IMU Calibration** | Like calibrating a drone: all six faces, hold still, move up and down, slide, spin clockwise and counter-clockwise around every axis, then a magnetometer figure-8. Every step shows a picture and waits for you to press OK. |
| **Sound & LED** | Beeps the buzzer and lights the LED, and you say what you heard and saw. |
| **Reaction Wheel** | A safety checklist you must tick, then the wheel spins gently and stops. |
| **Report** | All results in one place. Save as JSON, Excel or CSV. |
| **Full guided check** | Runs everything above in one go. |

### What your CubeSat firmware needs

Telemetry: one JSON (or CSV) line per packet, with these keys: `temp, hum, ax, ay, az, gx, gy, gz, mx, my, mz, hdg, alt, lat, lon, batt, wheel, rssi, snr, gps_fix`.

Commands the lab sends over the USB cable (one line each), and the reply it expects:

| Command | Reply |
| --- | --- |
| `CMD BUZZER_ON` / `CMD BUZZER_OFF` | `{"ack":"BUZZER_ON","ok":true}` |
| `CMD LED_ON` / `CMD LED_OFF` | `{"ack":"LED_ON","ok":true}` |
| `CMD WHEEL_START 30` / `CMD WHEEL_STOP` | `{"ack":"WHEEL_START","ok":true}` |

If a command gets no reply, the lab tells you and carries on. Lines starting with `#` are shown as notes.

## Files

| File | What it does |
| --- | --- |
| `index.html` | The welcome window. |
| `testing-lab.html` | CubeSat Testing Lab. |
| `telemetry.html` | CubeSat Telemetry (live packets, graphs, 3D view, map, export). |
| `assets/garuda.js` | Saves your details and adds them to every export. |
| `assets/garuda.css` | Shared day and night look. |
| `assets/logo-*.webp` | Logos. Swap these files to change the logo. |

## Put it on GitHub Pages

1. Create a new repository on GitHub (for example `garuda`).
2. Upload everything in this folder.
3. Go to **Settings → Pages**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
4. Open the link GitHub gives you. The USB connection (Web Serial) needs **Chrome or Edge** on a computer, and works on `https://` links like GitHub Pages.

## Notes

- The pages load Tailwind CSS, Chart.js, SheetJS (Excel) and the Saira font from the internet.
- Names and the day/night choice are stored in your browser only. Nothing is sent anywhere.
- Angles in the spin checks are estimated by adding up the gyroscope readings, so they are rough but good for a guided check.
