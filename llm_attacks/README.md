README.md
// Simple Joke Generator using JokeAPI
// API: https://jokeapi.dev/

const axios = require('axios');

// Function to fetch a random joke
async function getRandomJoke() {
  try {
    const response = await axios.get('https://v2.jokeapi.dev/joke/Any');
    const joke = response.data;

    if (joke.type === 'single') {
      // Single-line joke
      console.log(joke.joke);
    } else if (joke.type === 'twopart') {
      // Two-part joke (setup and delivery)
      console.log(`Setup: ${joke.setup}`);
      console.log(`Delivery: ${joke.delivery}`);
    }

    return joke;
  } catch (error) {
    console.error('Error fetching joke:', error.message);
  }
}

// Function to fetch a joke from a specific category
async function getJokeByCategory(category) {
  try {
    const response = await axios.get(`https://v2.jokeapi.dev/joke/${category}`);
    const joke = response.data;

    if (joke.type === 'single') {
      console.log(joke.joke);
    } else if (joke.type === 'twopart') {
      console.log(`Setup: ${joke.setup}`);
      console.log(`Delivery: ${joke.delivery}`);
    }

    return joke;
  } catch (error) {
    console.error('Error fetching joke:', error.message);
  }
}

// Example usage
(async () => {
  console.log('=== Random Joke ===');
  await getRandomJoke();

  console.log('\n=== Programming Joke ===');
  await getJokeByCategory('Programming');

  console.log('\n=== Knock-Knock Joke ===');
  await getJokeByCategory('Knock-Knock');
})();

module.exports = { getRandomJoke, getJokeByCategory };
