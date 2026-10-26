# Inventory Management App

An Android inventory tracking app built in Java for CS 360 (Mobile Architecture and Programming). The app lets warehouse staff log in, track items in a live grid, add and remove items, adjust quantities, and receive a text alert when an item runs out of stock.

## About the Project

The goal of this app was to give small businesses and warehouse teams a simple, reliable way to see what is in stock and to catch when something runs out before it becomes a problem. The core user need was straightforward: know what is on hand and get warned before a shelf goes empty, without needing a heavy enterprise system to do it. To meet that need, the app required a secure login, a persistent database to hold user accounts and inventory, a grid to display every item, controls to add, remove, and change items, and a notification that fires when an item reaches zero.

## UI Design

The app is built around three screens: a login and registration screen, the main inventory grid, and an add-item screen. Each screen was designed with the user in mind by keeping the layout simple and the most-used actions easy to reach. The login screen doubles as account creation so a first-time user does not need a separate signup flow. The grid shows each item with its name, quantity, plus and minus buttons, and a delete button, so the most common tasks are one tap away. Adding an item happens on its own screen to keep the grid uncluttered. These designs were successful because they follow standard Android and Material Design patterns, which means the app behaves the way users already expect and stays easy to learn.

## Coding Approach

I approached the coding in layers rather than all at once. I built the UI first, then connected it to the data. I created a single DatabaseHelper class to handle all of the SQLite work, which kept the database logic in one place and out of the screens. Each screen and the adapter call that helper to read or write data, so every action in the UI maps to a specific database operation. I used clear naming conventions and inline comments throughout so the code is readable to anyone who opens it. This separation of the UI from the data layer is a technique I can reuse in future projects, since it makes code easier to test, debug, and extend.

## Testing

I tested the app continuously in the Android Emulator as I built it, rather than waiting until the end. I confirmed each feature as it was added: creating an account and logging in, adding and deleting items, changing quantities, and closing and reopening the app to make sure the database kept the data. I also tested both outcomes of the SMS permission prompt, granting and denying, to make sure the app kept working either way. Testing often is important because it catches problems while they are still small and easy to trace, and it revealed exactly where data needed to reload so newly added items would appear in the grid.

## Challenges and Innovation

The part that took the most problem-solving was making the inventory grid, the quantity controls, and the database stay in sync. When a user changes a quantity or deletes a row, the screen and the stored data both have to update together. I solved this by having the adapter write each change to the database immediately and by reloading the grid when the screen returns to the front, so what the user sees always matches what is stored. Connecting the low-stock alert was another challenge, which I handled with a callback from the adapter to the activity so the SMS only sends when an item actually reaches zero and only if permission was granted.

## Strongest Component

The component I am most proud of is the database layer. Getting the SQLite database to handle user accounts and full create, read, update, and delete operations on the inventory, while staying persistent across app restarts, is what turned a set of static screens into a working app. It best demonstrates my ability to connect a user interface to real, lasting data, which is a skill that carries directly into the database and data analytics work I want to do.
