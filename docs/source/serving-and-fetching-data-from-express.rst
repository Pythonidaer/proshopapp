Serving & Fetching Data From Express
=====

.. _serving-and-fetching-data-from-express:

Section 3.11: Front End / Back End Workflow & Explanation
------------

1. First we go over the whole process of the frontend and the backend
2. The frontend is the React application that we review in the browser 
3. Right now the products are stored in a json file on the frontend
4. To create a full-stack application, we need a backend
5. Our backend will be created with Node.js, which is the JavaScript runtime
6. This allows us to run JavaScript on our server 
7. And also Express.js, which is a backend framework that allows us to create routes 
8. The backend is where we communicate with our database (in this case will be MongoDB)
9. To communicate with our db, we'll be using what's called an object data mapper
10. In the coding bootcamp, these were known as ORMs and in this case we're using Mongoose
11. Mongoose has methods like ``find`` and ``findById`` to make it easier to interact with the db
12. In our ``backend/``, we will be creating controllers, models, etc.
13. To get data from the ``backend/``, we need to make an HTTP request
14. The main 4 requests are GET, POST, PUT and DELETE
15. If we want to fetch the products from our ``backend/``, we would make a request from the ``frontend/``
16. For example, from the React app to something like ``/api/products``, which is a route we will create with Express.js
17. When we hit that route, we would send back the products' ``json`` data
18. Our ``backend/`` isn't going to serve HTML templates or anything like that
19. It's only going to serve ``json`` to our ``frontend/`` to pickup/read/do whatever we want
20. In our case, we're going to display our Products page, single Product Details page, etc.
21. Ultimately, these products and anything else that we have in our app is going to be stored in our MongoDB database 
22. For now, we're just going to move that products ``json`` folder from the frontend to the backend, just so we can start to work with a server
23. We can save data to our server, update, delete, etc. wit hthe different http methods 
24. GET is used for fetching/getting data 
25. POST is used for adding data
26. The above two could be the same endpoint, but there are different methods so it doesn't matter
27. To update something, typically you would use a PUT request
28. For PUTs, you'd have like ``/api/products/25`` (25 being an id) because you'd need to know which product that you're updating 
29. Same with DELETE: ``/api/products/25``
30. This keeps everything RESTful
31. REST API stands for REpresentational State Transfer (a software architectural style that defines a set of constraints to be used for Web APIs and web services)
32. Sometimes the apis will change if you were to have actions like authentication
33. In the next video, we're going to start to set up a very, very basic express server 
34. This way, we can actually fetch our products from the ``backend/`` rather than just by loading a JavaScript file in the ``frontend/``

Section 3.12: Serving Products - Back End Routes
----------------

1. Before we get into the database, let's serve products from the ``backend/``
2. React will fetch it from our ``frontend/``
3. Make sure to run ``npm init`` not inside the ``backend/`` folder but in the root for the server 
4. Add a description, and make the ``entry point`` be ``server.js``, author and license MIT 
5. The above will result in a ``package.json`` being created
6. ``npm i express`` in the root will install Express.js as a dependency
7. In ``backend/`` create a file called ``server.js`` that will be our entry point for our back end 
8. Also create a folder called ``data/`` and copy from the ``frontend/src/`` folder the ``products.js`` (that way nothing breaks)
9. Next, we want to create some routes to serve the products from the backend
10. In ``server.js``, add ``const express = require('express')``
11. The above syntax is common JS, which is traditionally what Node.js has used on the frontend
12. Instead we will be using the ``import`` syntax, which is the ES modules
13. Add ``const app = express()`` and ``app.listen(5000, console.log('listening on port 5000'))``
14. Later on this will be in an environment variable and we'll have separate files for routes and models and controllers (i.e. ``.env, backend/models || routes || controllers``) etc.
15. For now, we just want to serve the ``.json`` products
16. Run ``node backend/server`` to see "listening on port 5000"
17. To avoid the tediousness of having to do the above, go into the root ``package.json`` and add a key-value pair to the ``scripts`` section 
18. In the ``scripts`` object, add ``"start": "node backend/server"`` to run our server from the commandland
19. The above now logs the same as step 16
20. Go back to ``server.js`` and add ``app.get('/', (req, res) => { res.send('API is running...')})``
21. If you go to localhost:5000 in the browser, you will see there too that the API is running
22. Next we create an api route 
23. Copy the above code and for the first ``.get()`` param, add ``'/api/products'``
24. Temporarily go to the ``backend/data/products.js`` file and change the ``export default`` syntax to common JS ``module.exports = products``
25. Navigate back to the ``server.js`` file and add ``const products = require('./data/products') ``
26. Within the new ``app.get('/api/'products', ...)`` code, add ``res.json(products)`` in the body 
27. ``res.json()`` will convert our JavaScript to the JSON type 
28. Now, if you go to ``localhost:5000/api/products``, you'll notice it gives us the products array 
29. Add one more route for now: ``app.get('/api/products/:id', (req, res) => { const product = products.find((p) => p._id === req.params.id) res.json(product)})``
30. This will allow us to access routes for specific products based off their id 
31. For example: ``localhost:5000/api/products/2``
32. In the next video, we will return to the frontend React portion and make a request to the backend to get those products, as opposed to just having a file in the ``frontend/src/`` area


Section 3.13: Fetching Products from React (useEffect)
------------

1. Instead of loading a ``products.js`` file from the ``frontend/``, we want to fetch it from the ``backend/data/`` routes in the back
2. The ``'api/products'`` will return us this data
3. Navigate to the ``frontend/`` in your commandline console and prepare to add a new dependency 
4. test

Section 3.14: Nodemon & Concurrently Setup
----------------

Section 3.15: Environment Variables
------------

Section 3.16: ES Modules in Node.js
----------------
test