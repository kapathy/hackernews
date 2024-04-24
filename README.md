# Hacker News Top Stories

A simple web application built with Vue.js that fetches and displays ten random top stories from Hacker News, sorted by story score in ascending order.

## Features

- Fetches ten random top stories from Hacker News.
- Displays story details including title, URL, timestamp, score, author ID, and author karma score.
- Utilizes the Hacker News API endpoints for fetching story and author information.

## Technologies Used

- Vue.js
- JavaScript
- Hacker News API

## Installation

1. **Clone the repository:**
  ```bash
   git clone https://github.com/kapathy/hackernews.git
  ```

2. **Navigate to the project directory:**
  ```bash
   cd hackernews
  ```

3. **Install dependencies:**
  ```bash
   npm install
  ```

## Usage

1. **Start the development server:**
  ```bash
   npm run dev
  ```

2. **Open your web browser and go to `http://localhost:5173/` to view the application.**

## API Endpoints Used

- **Top stories:** `https://hacker-news.firebaseio.com/v0/topstories.json`
- **Story info:** `https://hacker-news.firebaseio.com/v0/item/[id].json`
- **Author info:** `https://hacker-news.firebaseio.com/v0/user/[id].json`

## How It Works

1. Fetch ten random story IDs from the top stories endpoint.
2. For each story ID, fetch the story details using the story info endpoint.
3. Fetch the author details using the author info endpoint.
5. Display the fetched data, sorted by story score in ascending order.