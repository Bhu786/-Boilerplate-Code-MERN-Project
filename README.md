# -Boilerplate-Code-MERN-Project


```javascript
// Import necessary modules
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const path = require('path');
const dotenv = require('dotenv');

// Initialize dotenv for environment variables
dotenv.config();

// Create an Express application
const app = express();

// Middlewares
app.use(express.json()); // To parse JSON request bodies
app.use(express.urlencoded({ extended: true })); // To parse URL-encoded request bodies
app.use(cors()); // To handle Cross-Origin Resource Sharing

// Connect to MongoDB
const mongoURI = process.env.MONGO_URI; // MongoDB URI from environment variable
mongoose.connect(mongoURI, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
})
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.log('MongoDB connection error: ', err));

// Example route for testing
app.get('/', (req, res) => {
  res.send('Welcome to the MERN backend!');
});

// Add your other routes here (Example: routes for image upload, user authentication, etc.)
// const imageRoutes = require('./routes/imageRoutes');
// app.use('/api/images', imageRoutes);

// Serve static files in production
if (process.env.NODE_ENV === 'production') {
  // Set static folder
  app.use(express.static('client/build'));

  // Serve index.html for any non-API routes in production
  app.get('*', (req, res) => {
    res.sendFile(path.resolve(__dirname, 'client', 'build', 'index.html'));
  });
}

// Start the server
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```






