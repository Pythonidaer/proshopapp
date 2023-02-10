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
3. Navigate to the ``frontend/`` in your commandline console and prepare to add a new dependency ``npm i axios``
4. Axios is an HTTP library - we use it to make requests to our ``backend/``
5. After download run ``npm start`` again
6. Go to ``HomeScreen.js`` and add products as component level state
7. When it comes to state, you have component leven and you have global or application level state
8. Products will ultimately be global state when we get into Redux
9. For now, we just make it part of the component
10. Generally, component level state will be things like a menu component's open and close state
11. Another example would be forms, the separate fields would be part of your component state
12. Things like products, users, your cart, stuff like that is going to be global state through Redux
13. Bring in the ``useState`` hook from React
14. It is used to use state in functional components
15. This is opposed to traditional ``Class`` based components with constructor-defined state 
16. In the functions we don't have a constructor, so we use the useState hook
17. Set a set of brackets to ``useState`` and pass in two things 
18. The two things to pass: what we want to call this piece of state, then what we want to call the function to manipulate or change the state 
19. For example: ``const [products, setProducts] = useState()``
20. Then, whatever we want to set as a default for products we pass in the useState, which is going to be an empty array: ``useState([])``
21. At this point, no errors would show, but our component would be mapping over an empty array 
22. What we want to do now is use the ``useEffect`` hook to make a request to our backend 
23. We want this because what useEffect does is we define it, and it takes in an arrow function, and whatever we put in here is going to run as soon as the component loads
24. So as soon as ``HomeScreen.js`` loads, that ``useEffect(() => {console.log('hi')})`` is going to fire off 
25. That's where we want to make our request because we want these products as soon as the component loads
26. In the useEffect is where we're going to make our axios requests 
27. We are going to use ``async, await`` syntax 
28. ``async, await`` returns a promise
29. To achieve this, we have to create a separate (asynchronous) function within useEffect 
30. ``const fetchProducts = async () => { const res = await axios.get('/api/products') }``
31. The above ``res`` would have a ``data`` object assigned to it (res.data)
32. We can use the data variable directly through destructuring: ``const { data }`` not res
33. Once we fetch that data, we want to set it to the product
34. In other words, we want to change this empty array to the data that we get back from the endpoint
35. We do that by calling ``setProducts`` as that's what we defined above to change the piece of state
36. Outside of ``fetchProducts`` call the function (within ``useEffect``)
37. As a second argument to ``useEffect`` you want to pass in an array of dependencies
38. What this means is anything you want to fire useEffect off when it changes
39. Generally, React will give you warnings if you put stuff in and you don't claim it as a dependency
40. So the syntax right now will be: ``useEffect(() => { ...const fetchProducts... }, [])``
41. Don't forget to ``import axios from 'axis'``
42. Also note that this is temporary, because later on we're going to use Redux and we make all of our requests from what are called ``action creators``
43. Create a proxy by going into the ``frontend/`` ``package.json``
44. Add this line of code: ``"proxy": "http://127.0.0.1:5000/"`` then restart frontned server
45. Now we should be getting the products from our ``backend/``
46. If you open up ``Network`` tab in console then ``Response`` you get to see the data that is coming back 
47. You can also see the ``Headers`` such as ``Status`` and ``content-type``
48. Repeat the process and navigate to ``ProductScreen.js``
49. Bring in both hooks: ``import React, {useState, useEffect} from 'react'``
50. ``const [product, setProduct] = useState({})`` because a single product is an object 
51. Copy the whole useEffect from the last page and take the s off (``setProduct``; ``fetchProduct``)
52. The route is going to be ``/api/products/${params.id}`` to hit whatever the clicked id is
53. Then we want setProduct, then we call fetchProduct, and remember to bring in axios!
54. Check the Chrome Tools ``Network`` tab again to see the id 
55. The ``frontend`` product.js can now be deleted
56. In the next video, we will add ``nodemon`` so we don't have to keep restarting the server
57. We will also use a package called ``concurrently`` so we can run both the ``backend/`` and the ``frontnend/`` at the same time with the same command instead of having to run react in one window and express in another

Section 3.14: Nodemon & Concurrently Setup
----------------

Section 3.15: Environment Variables
------------

Section 3.16: ES Modules in Node.js
----------------
test