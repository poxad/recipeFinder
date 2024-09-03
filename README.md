# recipeFinder

![recipeFinder](https://github.com/user-attachments/assets/936ea18a-8753-44ad-bedb-f2c77152a6cb)

**recipeFinder** is a simple and intuitive recipe website built using Vue.js, the Spoonacular API, and React. It allows users to find food recipes by searching with food names or ingredients. The app also includes an about page that provides information about the app and a contact page for users to reach out.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Pages](#pages)
- [API Reference](#api-reference)
- [License](#license)

## Features

- **Search by Food Name:** Find recipes by entering a food name.
- **Search by Ingredients:** Find recipes based on the ingredients you have.
- **Responsive Design:** Works on both desktop and mobile devices.
- **Easy Navigation:** Simple and intuitive navigation across different pages.

## Installation

To get a local copy up and running, follow these steps:

1. **Clone the repository:**
   ```sh
   git clone https://github.com/yourusername/recipeFinder.git
   ```

2. **Install NPM packages:**
   ```sh
   npm install
   ```

3. **Deploy:**
   ```sh
   npm run serve
   ```

## Usage

Once the application is running, you can access it in your browser by navigating to `http://localhost:8080`.

- Use the search bar on the home page to find recipes by food name.
- Navigate to the "Search by Ingredients" page to find recipes based on available ingredients.
- Learn more about the app in the "About" page.
- Contact the team through the "Contact" page.

## Pages

- **Home Page (Find by Food Name):** Enter the name of the food, and the app will display a list of recipes using the Spoonacular API.
  
- **Search by Ingredients:** Enter one or more ingredients, and the app will find recipes that can be made using them.
  
- **About Page:** Provides information about the app.
  
- **Contact Page:** Allows users to reach out with questions or feedback.

## API Reference

This app uses the [Spoonacular API](https://spoonacular.com/food-api) to fetch recipe data. You'll need to sign up for an API key to use it in development.

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.
