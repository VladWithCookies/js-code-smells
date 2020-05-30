# Shotgun Surgery
## Reason
Shotgun surgery is a change that requires code to be multiple pieces of code to be changed.

## Solutions
```js
// Bad
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.get('/foo', (req, res) => {
  console.log('foo called');
  res.json({ message: 'foo' });
});

app.get('/bar', (req, res) => {
  console.log('bar called');
  res.json({ message: 'bar' });
});

app.get('/baz', (req, res) => {
  console.log('baz called');
  res.json({ message: 'baz' });
});

app.listen(3000, () => console.log('server started'));

// Better
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use((req, res, next) => {
  if (req.path.substring(1)) {
    console.log(`${req.path.substring(1)} called`);
  }
  
  next();
});

app.get('/foo', (req, res) => res.json({ message: 'foo' }));
app.get('/bar', (req, res) => res.json({ message: 'bar' }));
app.get('/baz', (req, res) => res.json({ message: 'baz' }));
app.listen(3000, () => console.log('server started'));
```
