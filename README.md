# MEAN-stack2
res.status(200).json({ message: 'Item deleted successfully' });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

module.exports = router;



server.js :

const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const cors = require('cors')
const itemRoutes = require('./routes/itemRoutes');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());  // Parse JSON bodies
app.use(cors());
// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/mydatabase', {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.error('MongoDB connection error:', err));

// Use Routes
app.use('/api/items', itemRoutes);

app.listen(port, () => {
  console.log(Server is running on http://localhost:${port});
});
