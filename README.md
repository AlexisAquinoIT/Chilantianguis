# Chilantianguis
Chilantianguis is a free map of Mexico City's tianguis, public markets, local shops, and small businesses. Discover products, opening hours, and discounts, or let merchants list their stalls and receive simple orders. Built as an MVP for Chilangatón 2026, it helps connect local businesses with their communities.

📦 Technologies
Python: the programming language that runs the "brain" of the website.
Flask: a lightweight Python tool for building websites. It receives what the visitor asks for and sends back the right page.
SQLite: a small database stored in a single file. It keeps all places, stalls, products, discounts and orders.
HTML + Jinja2: HTML builds the pages you see, and Jinja2 fills them in automatically with the data from the database.
Tailwind CSS and CSS: control the colors, layout and the Mexican-market look of the site, so it also works on phones.
JavaScript: makes the map and the filters react instantly, without reloading the page.
Leaflet + OpenStreetMap: draw the interactive map and place a pin on every business.
Pillow: checks and shrinks the photos that merchants upload.

🦄 Features

Here's what you can do with Chilantianguis:

Explore the Map: Open the map of Mexico City and see every tianguis, market, shop and small business as a pin. No account needed.
Search and Filter: Look for a place or product by name and narrow results by type of place, borough (alcaldía), product category, day of the week or active sales.
See Place Details: Open any place to check its address, opening hours, the stalls inside and the products with their prices.
Find Sales: Discover products with a discount and see exactly when each sale starts and ends.
Create a Merchant Account: Sellers sign up with their cell phone number and a verification code (simulated in this demo).
Manage Your Business: From a personal panel, merchants can register a stall, shop or small business, pin its location on the map, add products with photos, update stock and schedule discounts.
Place an Order: Shoppers can fill a cart and confirm an order with just their name. They get an order code, and no real payment is made. Stock is reduced automatically.
Follow Orders: Merchants see incoming orders and mark them as preparing, ready, delivered or cancelled. A cancelled order puts the products back in stock.
Contact by WhatsApp (Optional): A merchant's phone number is only shown if they choose to turn this option on.
Buy Together at Wholesale: Merchants can create group purchases, so several small sellers join forces to reach a quantity and get a better supplier price (commitments are simulated, no money moves).
Request a New Tianguis: Associations of vendors can fill out a form to ask for their tianguis to be added to the map.

👨‍🍳 The Process

I started by thinking about who would use the platform: people looking for places to shop, and small merchants who need visibility. With that clear, I designed the database, which is basically the list of everything the site needs to remember: users, places, opening hours, stalls, products, categories, sales, orders and wholesale groups. I added rules to it, so for example a price can never be zero and a discount can never end before it starts.

Next, I built the website with Flask. I created the pages for the home screen, the explorer, the place details and the merchant panel, and connected them to the database.

Then I worked on the map. I used Leaflet and OpenStreetMap to draw it, and wrote a small service inside the app that returns the places matching the filters the visitor chooses. Every time a filter changes, the map updates without reloading the page.

To have real content to show, I wrote scripts that load 64 example places (16 tianguis, 16 public markets, 16 neighborhood shops and 16 small businesses, spread across the 16 boroughs of Mexico City). I also prepared an importer that can bring in the official open data of Mexico City.

After that, I added the merchant side: sign-up with a phone number and a simulated verification code, a panel to register stalls and products, photo uploads and scheduled discounts. Then I built the shopping cart, the order flow and the wholesale groups.

Finally, I focused on safety and honesty: protection against forged form submissions, safely stored passwords, checked images, private phone numbers by default and clear labels wherever the data is an example.

📚 What I Learned

During this project, I picked up new skills and a better understanding of how a complete web application fits together.

🗄️ Designing a Database:
Planning Ahead: I learned to organize information into connected tables and to add rules so wrong data (like negative stock) can't get in.
Safe Updates: I learned how to add new features to an existing database without erasing the data that was already there.
🛒 Avoiding Mistakes with Stock:
Transactions: I learned that if two people buy the last item at the same time, the system must let only one succeed. I used database transactions to make sure the stock is never sold twice.
🗺️ Working with Maps:
Coordinates and Open Data: I learned how to place businesses on a map using latitude and longitude, and how to read the GeoJSON files that the city government publishes.
🕒 Time Zones:
Local Time Matters: Sales start and end at specific hours, so I learned to handle Mexico City time correctly to show only the discounts that are really active.
🔐 Security and Privacy:
Protecting Users: I learned about CSRF protection, password hashing, validating uploaded images and not exposing personal data (like phone numbers) without permission.
🤝 Thinking Like a User:
Being Honest in the Design: I learned to clearly mark what is real and what is simulated (payments, text messages, example data), so nobody is misled.
📈 Overall Growth:

Each part of this project helped me understand more about building a full application, from the database to the screen the user sees. It was more than just making a website. It was about solving real problems for small local businesses, learning new tools and writing code that is safe and organized.

💭 How can it be improved?
Send real verification text messages instead of the simulated code.
Add real online payments.
Add a review screen where administrators can approve or reject tianguis requests.
Verify merchant profiles and moderate their content.
Add login attempt limits and HTTPS before publishing it on the internet.
Import more real businesses using the INEGI DENUE database.
Add automated tests to catch errors early.
Add a dark mode and more languages.
List every dependency (such as Pillow) in requirements.txt for an easier installation.
🚦 Running the Project

To run the project on your own computer (Windows with PowerShell), follow these steps:

Install Python (version 3.9 or newer) and Git.
Clone the repository and open the project folder:
powershell
   git clone https://github.com/<your-username>/Chilantianguis.git
   cd Chilantianguis
Create a virtual environment and install the required libraries:
powershell
   py -m venv .venv
   .\.venv\Scripts\python.exe -m pip install -r requirements.txt
Create your settings file (open .env afterwards and change SECRET_KEY to any long random text):
powershell
   Copy-Item .env.example .env
Create the database and load the 64 example places:
powershell
   .\.venv\Scripts\python.exe -m flask --app app init-db
   .\.venv\Scripts\python.exe scripts\cargar_64_comercios.py
Start the application:
powershell
   .\.venv\Scripts\python.exe -m flask --app app run --debug
Open http://127.0.0.1:5000 in your web browser.

To try the merchant side: click "Tengo un puesto", type any 10-digit cell phone number and use the verification code 111111. This code is a simulation made for the demo, and no real text message is sent. The map needs an internet connection to load.

🍿 Video
