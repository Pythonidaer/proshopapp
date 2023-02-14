Getting Started With MongoDB
=====

.. _getting-started-with-mongodb:

Section 4.17: MongoDB Atlas & Compass Setup
------------

1. We will now start working with a NoSQL database flavor called MongoDB
2. With NoSQL databases you have collections of documents (JSON objects basically)
3. A document example includes an object of key-value pairs
4. When you create a new document, it assigns what's called an ``object _id`` and puts an underscore id field, so those fields are created automatically in MongoDB
5. We are going to have a few "collections" (for Users, Orders and for Products)
6. Head to `www.mongodb.com <https://www.mongodb.com/>`_ and create an account
7. You can use MongoDB Atlas, which is a cloud version
8. This meakes it easy to deploy; we don't have to install because we keep the same database
9. Everything would be the same except the database URI string that you use to connect
10. As soon as you log in you might see a "Create a Cluster" or "Build a Cluster"
11. Build a Cluster, keep the defaults, then make your preferred language 'JavaScript'
12. Choose the free tier, then choose the AWS cloud provider (Default)
13. Name the Cluster whatever you like; takes about 2-3 minutes to finish setting up
14. Optionally you can download MongoDB Compass (a GUI desktop app to connect to the database and your data)
15. On MongoDB Cloud, navigate to 'Database Access' and create a new DB user
16. Create a password, then allow the user to r/w to any db then add that user
17. Under Network Access add IP address,
18. If this is a Production application that you're deploying, you would want to add your current IP address
19. For our project, we select "Allow access from anywhere" then click Confirm
20. Go back to Clusters 
21. Then click on Collections (this is where you would see your data if we had any)
22. Click on "Add My Own Data" then name your Database (the app name, ideally)
23. Put an initial collection (i.e. "products")
24. You should now see the ``proshop`` database with ``products`` collection
25. The collections will be created automatically when we run our application, once we set it up to create a collection
26. Go back to the 'Clusters' view and click 'Connect' and click on 'MongoDB Compass'
27. Select 'I have MongoDB Compass' then copy the string
28. Copy and paste the URL to MongoDB Compass 
29. Replace ``test`` with your ``database_name``
30. Replace ``<password>`` with your password
31. From here, you should be able to find your database and collection on the GUI
32. Go back to the Atlas, 'Connect to Application' then copy the Application URL string, then paste that in your MONGO_URI ``.env`` file 
33. Make sure to change the database and password here as well 
34. By now, you should be all set with MongoDB Atlas
35. Next video, we're going to connect to our database, create a database config file, and we're going to use Mongoose to do that, which is an object data map, or it's basically a layer that allows us to interact with our database really easily to create items, create data, find data, all that stuff

Section 4.18: Connecting To The Database
----------------

1. Next we're going to be connecting to our database through our application
2. We're going to use a tool called Mongoose, which is object modeling for Node.js 
3. This basically allows us to create a model and a schema for different resources in our database: like products, users, and so on
4. Check out  `mongoosejs.com <https://mongoosejs.com/>`_ documentation
5. We can even create Mongoose ``middleware`` that runs when you do certain things like save a document
6. Next we are going to install and connect
7. For this, make sure you are in your root (don't install this on the ``frontend/``)
8. Enter ``npm i mongoose`` and note that there are different ways to structure this 
9. What Travery does here in the ``backend/`` is create a folder called ``config/``
10. Inside ``config/`` create a file called ``db.js`` and this will be our db/connection file
11. ``import mongoose from 'mongoose'`` in ``db.js`` 
12. Then ``const connectDB = async () => { ... }``
13. This will be asynchronous, because when we deal with MongoDB, when we call ``.connect`` or ``.find()`` or ``.create()`` or whatever, it's always going to ``return`` a ``Promise``
14. Then insert a ``try { ... } catch (error) { ... }`` code block inside of the function 
15. In the ``try``, add ``const conn = await mongoose.connect(process.env.MONGO_URI)``
16. Then, ``console.log(`MongoDB Connected: ${conn.connection.host}`)``
17. In the ``error`` add ``console.error(`Error: ${error.message}`)``
18. Next, add ``process.exit(1)`` because the 1 means we will exit with failure
19. Finally, add ``export default connectDB`` to export the function 
20. Navigate to the ``server.js`` file and ``import connectDB from './config/db.js'``
21. Note that we have to add ``.js`` when we're importing files because we're on the ``backend/`` using ES6 modules with Node, and that is one of the current rules
22. Below ``dotenv.config()``, add ``connectDB()``
23. The next time you run your application, you should connect to the server
24. From the root, enter ``npm run server`` in commandline
25. Check the console to confirm that you have successfully connected
26. In the next video, we will install a package called ``colors`` so that we can add colors to our console and make these messages pop a bit more 

Section 4.19: Adding Colors To The Console (Optional)
------------

1. This next package is optional: `npmjs.com/package/colors <https://www.npmjs.com/package/colors`_ 
2. This will allow us to just have colors in the console 
3. We can underline, bold text, inverse styles
4. Enter ``npm i colors`` from the root then ``npm run server`` once more
5. ``import colors from 'colors'`` in ``server.js``
6. Update ``db.js`` log to ``(`MongoDB Connected: ${conn.connection.host}`.cyan.underline)``
7. You can also update error log to ``(`Error: ${error.message}`.red.underline.bold)``
8. What we will do in the next video is start to create some ``data models``
9. With NoSQL, you don't do that stuff on a database level as you would with, say, MySQL or Postgres
10. With Postgres you would use something like PG admin or a migration and you would set up your fields with the data types
11. With MongoDB, we do that at the application level

Section 4.20: Modeling Our Data
----------------

1. Here we are going to create all 3 models
2. After we create the models, we are going to create a seeder script 
3. The seeder script is so we can ``import`` some dummy data to work with 
4. In the ``backend/`` folder create a folder called ``models/``
5.
6.
7.
8.
9.
10.

Section 4.21: Preparing Sample Data
------------

1. test
2. test 
3. test

Section 4.22: Data Seeder Script
----------------

1. test
2. test 
3. test

Section 4.23: Fetching Products From The Database
----------------

1. test
2. test 
3. test

Section 4.24: Getting Started With Postman
------------

1. test
2. test 
3. test

Section 4.25: Custom Error Handling
----------------

1. test
2. test 
3. test