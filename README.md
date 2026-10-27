# 🧺Chilantianguis
Chilantianguis is a free map of Mexico City's tianguis, public markets, local shops, and small businesses. Discover products, opening hours, and discounts, or let merchants list their stalls and receive simple orders. Built as an MVP for Chilangatón 2026, it helps connect local businesses with their communities.


## 📦 Technologies
- `Python`
- `Flask`
- `SQLite`
- `HTML + Jinja2`
- `Leaflet + OpenStreetMap`
- `Pillow`


## 🦄 Features

Here's what you can do with Chilantianguis:

- **Explore the Map**: Open the map of Mexico City and see every tianguis, market, shop and small business as a pin. No account needed.

- **Search and Filter**: Find places by name, type, borough, category, day, or active sales. View addresses, hours, stalls, products, and prices.

- **Find Sales**: Discover discounts and their start and end dates. Merchants can register with a phone number and simulated verification code, then manage their business, products, stock, and offers.

- **Create a Merchant Account**: Sign up with a phone number and a simulated verification code - (simulated in this demo).
 
- **Manage Your Business**: Register your stall, add products and photos, update stock, and schedule discounts.

- **Place an Order**: Shop with a cart and confirm orders without real payments. Stock updates automatically.
 
- **Follow Orders**: Track orders from preparation to delivery. Cancellations restore stock.
  
- **Contact by WhatsApp**: Share your phone number with customers only if enabled.
  
- **Buy Together at Wholesale**: Join other merchants in group purchases for better supplier prices. Commitments are simulated.

- **Request a New Tianguis**: Associations of vendors can fill out a form to ask for their tianguis to be added to the map.

## 👨‍🍳 The Process

I started by thinking about who would use the platform: people looking for places to shop, and small merchants who need visibility. With that clear, I designed the database, which is basically the list of everything the site needs to remember: users, places, opening hours, stalls, products, categories, sales, orders and wholesale groups. I added rules to it, so for example a price can never be zero and a discount can never end before it starts.

Next, I built the website with Flask. I created the pages for the home screen, the explorer, the place details and the merchant panel, and connected them to the database.

Then I worked on the map. I used Leaflet and OpenStreetMap to draw it, and wrote a small service inside the app that returns the places matching the filters the visitor chooses. Every time a filter changes, the map updates without reloading the page.

To have real content to show, I wrote scripts that load 64 example places (16 tianguis, 16 public markets, 16 neighborhood shops and 16 small businesses, spread across the 16 boroughs of Mexico City). I also prepared an importer that can bring in the official open data of Mexico City.

After that, I added the merchant side: sign-up with a phone number and a simulated verification code, a panel to register stalls and products, photo uploads and scheduled discounts. Then I built the shopping cart, the order flow and the wholesale groups.

Finally, I focused on safety and honesty: protection against forged form submissions, safely stored passwords, checked images, private phone numbers by default and clear labels wherever the data is an example.

## 📚 What I Learned

During this project, I picked up new skills and a better understanding of how a complete web application fits together.

### 🗄️ Designing a Database:
- **Planning Ahead**: I learned to organize information into connected tables and to add rules so wrong data (like negative stock) can't get in.
- **Safe Updates**: I learned how to add new features to an existing database without erasing the data that was already there.

### 🛒 Avoiding Mistakes with Stock:
- **Transactions**: I learned that if two people buy the last item at the same time, the system must let only one succeed. I used database transactions to make sure the stock is never sold twice.

### 🗺️ Working with Maps:
- **Coordinates and Open Data**: I learned how to place businesses on a map using latitude and longitude, and how to read the GeoJSON files that the city government publishes.

### 🕒 Time Zones:
- **Local Time Matters**: Sales start and end at specific hours, so I learned to handle Mexico City time correctly to show only the discounts that are really active.

### 🔐 Security and Privacy:
- **Protecting Users**: I learned about CSRF protection, password hashing, validating uploaded images and not exposing personal data (like phone numbers) without permission.

### 🤝 Thinking Like a User:
- **Being Honest in the Design**: I learned to clearly mark what is real and what is simulated (payments, text messages, example data), so nobody is misled.

### 📈 Overall Growth:
Each part of this project helped me understand more about building a full application, from the database to the screen the user sees. It was more than just making a website. It was about solving real problems for small local businesses, learning new tools and writing code that is safe and organized.

## 💭 How can it be improved?
- Send real verification text messages instead of the simulated code.
- Add real online payments.
- Add a review screen where administrators can approve or reject tianguis requests.
- Verify merchant profiles and moderate their content.
- Add login attempt limits and HTTPS before publishing it on the internet.
- Import more real businesses using the INEGI DENUE database.
- Add automated tests to catch errors early.
- Add a dark mode and more languages.
- List every dependency (such as Pillow) in ```requirements.txt``` for an easier installation.

## 🚦 Running the Project

To run the project on your own computer (Windows with PowerShell), follow these steps:

1. Install Python (version 3.9 or newer) and Git.
2. Clone the repository and open the project folder:
```
  git clone https://github.com/<your-username>/Chilantianguis.git
  cd Chilantianguis7
```
   
3. Create a virtual environment and install the required libraries:
```
   py -m venv .venv
   .\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

4. Create your settings file (open ```.env``` afterwards and change ```SECRET_KEY``` to any long random text):
```
   Copy-Item .env.example .env
```
5. Create the database and load the 64 example places:
```
   .\.venv\Scripts\python.exe -m flask --app app init-db
   .\.venv\Scripts\python.exe scripts\cargar_64_comercios.py
```

6. Start the application:
```
   .\.venv\Scripts\python.exe -m flask --app app run --debug
```

7. Open [(http://127.0.0.1:5000) in your web browser.

To try the merchant side: click "Tengo un puesto", type any 10-digit cell phone number and use the verification code ```111111```. This code is a simulation made for the demo, and no real text message is sent. The map needs an internet connection to load.

## 🍿 Video
