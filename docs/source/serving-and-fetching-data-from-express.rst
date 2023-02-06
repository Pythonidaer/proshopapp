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

Section 3.13: Fetching Products from React (useEffect)
------------

Section 3.14: Nodemon & Concurrently Setup
----------------

Section 3.15: Environment Variables
------------

Section 3.16: ES Modules in Node.js
----------------
test