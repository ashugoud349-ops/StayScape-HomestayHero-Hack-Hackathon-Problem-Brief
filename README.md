# StayScape — HomestayHero Hackathon Solution

A full-stack homestay discovery, booking and host-verification prototype based on the supplied 3-page project brief.

## Included
- Frontend: HTML, CSS and JavaScript (easy to run in VS Code with Live Server)
- Backend: Node.js + Express REST API
- Database: JSON file persistence in `backend/data/db.json` (no database installation required)
- 12 seeded experiential homestays across Indian hill, coastal, heritage and rural destinations

## Requirements
- Node.js 18 or newer
- VS Code (recommended)
- Live Server VS Code extension (optional; you can also use the backend to serve the page)

## Run the full-stack project

1. Extract `StayScape.zip`.
2. Open the extracted `StayScape` folder in VS Code.
3. Open **Terminal → New Terminal**.
4. Run:

   ```bash
   npm install
   npm start
   ```

5. Wait until the terminal says `StayScape API running at http://localhost:4000`.
6. Open a second terminal in VS Code. Install/use the **Live Server** extension, right-click `index.html`, then choose **Open with Live Server**.
7. The website opens in your browser. Keep the backend terminal running while using the site.

The API health check is `http://localhost:4000/api/health`. You can also open `http://localhost:4000/api/stays` to view the sample data.

## Main user journey
1. Search or filter the 12 homestays.
2. Open a stay and choose check-in/check-out dates and guests.
3. Select an optional local experience.
4. Check availability and view the price breakdown.
5. Confirm a simulated booking and view the stay voucher.
6. Open **Host portal** and complete the three-step host verification.
7. Use the **Admin review** button after submitting to approve the demo verification.
8. The approved listing gets the green verified badge when the submitted homestay name matches a seeded listing.

## Pricing and booking logic
- Room price is multiplied by the number of nights.
- Friday/Saturday nights have a 10% demo surcharge.
- Cleaning fee is added once per booking.
- Optional local experience add-on is ₹500.
- Demo local tax is 5% of room + cleaning + add-on.
- The API rejects overlapping confirmed bookings using:
  `newCheckIn < existingCheckOut && newCheckOut > existingCheckIn`.

## REST API
| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/health` | API status |
| GET | `/api/stays` | List/search stays |
| GET | `/api/stays/:id` | Stay details |
| GET | `/api/availability?stayId=...&checkIn=YYYY-MM-DD&checkOut=YYYY-MM-DD` | Availability |
| GET | `/api/bookings` | List bookings |
| POST | `/api/bookings` | Create booking; prevents overlapping dates |
| POST | `/api/verifications` | Submit host verification metadata |
| GET | `/api/verifications` | List verification requests |
| PATCH | `/api/verifications/:id/approve` | Admin approval and badge unlock |

## Important prototype/security notes
- This is a hackathon demonstration, not a production booking platform.
- Do **not** upload real Aadhaar, passport, utility bill or sensitive personal documents. The frontend records only selected demo filenames; it does not upload or retain document contents.
- Admin review is intentionally simulated and is not secure authentication. Add real admin login, authorization, encrypted document storage, audit logs and privacy controls before real use.
- Payments, host phone numbers, directions, and video greetings are demonstration placeholders; no real payment or message is sent.
- Images load from Unsplash, so internet access is needed for the photographs. All core layout and demo logic are local.

## Troubleshooting
- `npm is not recognized`: install Node.js LTS from https://nodejs.org/, restart VS Code, and try again.
- `EADDRINUSE`: port 4000 is already in use; close the other server or set a different `PORT`.
- Website loads but shows no stays: make sure `npm start` is still running in the first terminal.
- API check: open `http://localhost:4000/api/health`.

## Project structure
```text
StayScape/
├── index.html
├── styles.css
├── app.js
├── package.json
├── README.md
└── backend/
    ├── server.js
    └── data/
        └── db.json
```
