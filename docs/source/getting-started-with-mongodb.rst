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

1. This next package is optional: `npmjs.com/package/colors <https://www.npmjs.com/package/colors>`_ 
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
5. We will have 3 models for 3 resources in our database
6. These models will be: the Users, the Products and the Orders
7. Create a file and name it ``userModel.js``, then again for ``productModel.js`` and ``orderModel.js``
8. ``import mongoose from 'mongoose'`` then create a ``const userSchema = ...``
9. Set that variable to ``mongoose.Schema()`` then pass in an object
10. This object is where we will define all the fields that we want for a user 
11. Observe common keys: ``name``, ``type``, and whether or not a field is ``required``
12. For this ``User`` model, also observe ``email`` and ``unique`` to avoid email repeats
13. Also observe ``password`` and ``isAdmin``, which could be used for addtl. permissions as well as features
14. Finally, observe here ``default`` so that it is false that a User is an admin initially
15. In Traversy's course, an Admin will have to make another ``User`` an admin
16. Mongoose schemas support ``timestamps`` option, that can provided two fields: ``createdAt`` and ``updatedAt``
17. Read more about these and other features `here <https://mongoosejs.com/docs/timestamps.html/>`_ 
18. Next, create a ``model`` from the now-created ``Schema``
19. Use the code ``const User = mongoose.model('User', userSchema)`` and ``export default User``
20. Repeat the same process for ``const = productSchema`` in ``productModel.js``, however observe a key relational difference
21. Create a ``user: { ... } `` field to later identify which admin (``User``) created which products (alternatively, figure out which user creates which saved post)
22. In ``user``, add ``type: mongoose.Schema.Types.ObjectId``
23. We need to reference a specific model for this object id: ``ref: 'User'``
24. The above adds a relationship between the ``Product`` and the ``User``
25. Observe other key properties here, such as ``image``, ``category``, ``required``, etc.
26. Compare a Product here to, say, a Reddit Post (my idea for the next project)
27. Also note that there is a ``default`` value used with the ``rating`` field
28. Observe that one field, ``reviews``, is an ``array`` of review ``objects``, and that we actually will have a separate ``Schema`` called ``reviewSchema``: ``reviews: [reviewSchema]``
29. Observe the final draft of ``productModel.js``, and make sure to ``export default Product``
30. Observe that tying schemas to models results in only needing to export the model(s)
31. The ``Order`` model is the biggest model as far as the number of fields
32. Notice how the ``orderItems`` field is an array of objects referencing the ``Product`` model
33. Observe that the ``Product`` objects also possess a ``type: mongoose.Schema.Types.ObjectId`` field in order to have a relationship to the order by product id
34. For the ``paymentMethod`` attribute, Brad keeps it general to make it scalable to add other payment gateways besides PayPal (such as Stripe)
35. Observe that the ``paymentResults`` object contains fields for data that will be  received back from the PayPal API (when successful)
36. Observe how ``isPaid`` and ``isDelivered`` are ``Boolean`` types that can later be modified later in the course (how?)
37. ``export default Order`` and review the final file of ``orderModel.js``
38. In the next section, we will prepare data for importing into the database
39. In particular we also want to add some ``Users`` as well
40. After we prepare, our data will go ahead and create a data center script to seed the database with the sample data 
41. Then we can move on and we can start to ``fetch`` data from MongoDB, our products, then get into *user authentication* and go from there


Section 4.21: Preparing Sample Data
------------

1. Now we will prepare some data to be imported into our database to work with
2. To some extend we will use the ``data/products.js`` 
3. Before we set up our data seeder script, we need to get rid of the ``_id``s
4. Because when data is entered into MongoDB, it automatically creates an ``_id`` field
5. Next, create a file in ``data/`` called ``users.js``
6. Create an array of 3 users, with one of them being an admin
7. These ``users`` have to have only the fields that we have in our ``User`` model, or ``mongoose`` isn't going to let us insert it into the database
8. There will be ``name``, ``email``, and ``password`` - the last will have to be hashed
9. We are going to bring in ``bcrypt``, which is used to hash or encrypt passwords
10. Set ``isAdmin`` to ``true``
11. ``isAdmin`` is ``false`` by default, so the non-admin users don't need that field added
12. In the ``propshop`` root, run ``npm i bcryptjs`` (not bcrypt, which is more dependencies)
13. In the ``users.js`` file, ``import bcrypt from 'bcrypt.js'``
14. There are a few different ways to hash passwords 
15. Normally we want to do this asynchonrously, but since this is test data, Traversy uses the hash sync method, which will hash the passwords synchronously
16. Note here that the first param is the plaintext password: ``bcrypt.hashSync('123456', 10)``
17. The second param is the number of rounds, with 10 being a default and secure number 
18. ``export default users``
19. In the next video, we will go ahead and create the ``seeder`` script

Section 4.22: Data Seeder Script
----------------

1. Now that we have our ``models/``, and sample data for ``products`` and ``users``, we can create a database seeder to easily import some sample data (users and products)
2. In ``backend/`` folder, create a new file called ``seeder.js`` 
3. This isn't part of our application, it's just a separate script so that we can run to import data
4. ``import mongoose, dotenv, colors, users, products, User, Product, Order`` and ``connectDB`` from their respective locations
5. We're not actually creating any orders with the seeder, but Traversy does want the ability to ``destroy`` all users, products and orders (so we do need the model to remove data)
6. Review the file and enter ``dotenv.config()`` followed by ``connectDB()``
7. We are creating two functions: one is going to impport dat aand one is going to destroy data 
8. This is going to be asynchronous because we're dealing with the database or dealing with ``mongoose``
9. So, everything returns a ``Promise``
10. Create ``const importData = async () => {}`` and in the code block add a ``try catch`` section 
11. In the ``try``, add ``await Order.deleteMany()`` and repeat the same for ``Product`` and ``User``
12. What this will do is clear all those because we don't want to import anything with stuff already in the database (this will completely wipe it out)
13. Next we can add ``await User.insertMany(users)`` so we can import the ``users`` data 
14. Next create a variable called ``const createdUsers = `` and store the above inside of it to create an array of the created ``users``
15. Capture the admin by adding the line ``const adminUser = createdUsers[0]._id`` as it is the first array element
16. Next add the line ``const sampleProducts = products.map((product) => { return { ...product, user: adminUser }})
`` 
17. In the above: for each ``product``, return an object with all of the stuff that's in it already 
18. We achieve this by using the spread operator, which spreads across all of the data that's already ther
19. In addition to that, we add the ``user`` field, the ``adminUser`` that we pulled in step 15
20. So far, nothing is in the database, but we have everything stored inside of ``sampleProducts``
21. In the next line add ``await Product.insertMany(sampleProducts)`` to add all the ``product`` data, which is also now going to include the ``admin`` user
22. Finally, add a line ``console.log('Data Imported!'.green.inverse)`` then ``process.exit()``
23. Within the ``catch``, add the parameter ``error`` followed by ``console.error(`${error}.red.inverse`)`` and ``process.exit(1)`` to log the error to the console and exit the process with a failure (1)
24. Create another function ``const destroyData = async () => { ... } `` containing another ``try catch`` block
25. As opposed to the above where we clear the database before importing data, here we just delete the data 
26. Review the ``seeder.js`` file and observe that the ``deleteMany()`` calls remain, just not the ``insertMany()``
27. Repeat the same error content in the ``catch`` portion
28. Run ``node backend/seeder`` to do the import 
29. Run ``node backend/seeder -d`` to do destroy the data
30. To achieve this, lastly add the code ``if (process.argv[2] === '-d') { destroyData()} else { importData() }``
31. This uses ``Node.js`` to check for whether the second ``argument variable`` after ``node`` is ``-d`` or not
32. Instead of leaving the call to the console, Traversy creates an npm ``script``
33. Head to the main ``package.json`` and under ``scripts`` add ``"data:import"`` and ``"data:destroy"`` 
34. The two above scripts will contain the seeder and seeder -d calls
35. From the main ``proshop`` root, run ``npm run data:import`` and observe if the console says ``Date Imported!``
36. Navigate to ``MongoDB Compass`` on your desktop, click the top nav ``View`` option, then select ``Reload Data``
37. We should now be able to see all of our ``products`` and ``user`` data
38. Each of the ``products`` should have the same ``user`` field, because we added the ``admin`` to each ``product``
39. You can verify this by navigating to the ``users`` collection and taking a look at the ``admin _id`` value
40. Notice that the password is hashed 
41. Next, from the console again run ``npm run data:destroy``, check the console, and ``View > Reload Data`` once more
42. Watch out for this, as this will delete live data so if you ever have real stuff it will get wiped from the db 
43. We basically just wanted to get data in there in the beginning, we can even delete it if we want to
44. In the next section, we start to ``fetch`` data from the database in our ``backend/`` 
45. That way, in our ``fronend/`` we can make our ``request`` to the roots and get data from the database as opposed to right now, where we're just getting from ``products.js`` which is currently probably broken since we removed the ``_id`` value (notice how MongoDB re-added it)


Section 4.23: Fetching Products From The Database
----------------

1. In this section we begin to fetch our ``products`` from the ``database``
2. Currently, we just have two ``routes`` directly from our ``server.js`` file that get ``products`` from the ``products.js`` file
3. In the ``backend/`` folder, create a ``routes/`` folder and create a ``productRoutes.js`` file
4. ``import express from 'express'``
5. Create a variable ``const router = express.Router()``
6. ``export default router``
7. Paste the ``routes`` from ``server.js`` into the ``productRoutes`` file, but change ``app`` to ``router``
8. Since we will point to this file, remove the ``'/api/products'`` syntax (``'/api/products/:id'`` becomes ``'/:id'``)
9. In ``server.js``, ``import productRoutes from './routes/productRoutes.js'`` (ES6 modules used, so add the .js)
10. Mount the imported route with the syntax: ``app.use('/api'/products', productRoutes)``
11. Go back to the ``productRoutes.js`` file and ``import Product from '../models/productModel'``
12. Where we get all our ``products``, add ``const products = Product.find({})`` and pass in an empty object, which just gives us everything (and returns a ``Promise``)
13. Remember, whenever we use a ``mongoose`` method it returns a ``Promise``, so we use ``await`` and ``async``
14. Therefore, change the syntax to: ``router.get('/', async (req, res) => { const products = await ... })``
15. To avoid adding a ``try, catch`` block to every route grouping, import the ``express-async-handler`` library 
16. Read more about how this simple middleware handles exceptions inside of async express routes `here <https://www.npmjs.com/package/express-async-handler>`_ 
17. In the main root folder, ``npm i express-async-handler`` then ``import asyncHandler from 'express-async-handler'``
18. Next, wrap the async like so: ``router.get('/', asyncHandler(async (req, res) => { ... }))``
19. Next, for the specific ``/:id`` route, add in the block ``const product = await Product.findById(req.params.id)``
20. The above will give us whatever the ``/id`` is that is in the URL
21. Next, add ``if(product){res.json(product)}`` and ``else{res.status(404).json({message: 'Product not found' })}``
22. Repeat the steps from step 18. to wrap the ``/:id`` route in ``asyncHandler`` as well 
23. COMMENTS: add a header for each ``route`` that says what it is, as well as the ACCESS level (i.e. admin, private/public)
24. Use this syntax: ``// @desc Fetch all products // @route GET /api/products // @access Fetch all products``
25. Please note, Traversy has been taking us one step at a time to help people get a clearer picture of what's going on 
26.
27. What Traversy means by ``@access`` is that for some ``routes``, we'll need a ``token``
28. For example, you'll need to be logged in to perform certain tasks - you'll need to send a token to specific routes, and those will be private routes
29. PUBLIC routes means that anyone can hit it 
30. Repeat the comments for the second route, then head over to Postman to test routes on the ``backend/``
31. From the console, run ``npm run server`` to for now just test the URL in the browser
32. What you should see for, say, ``localhost:5000/api/products`` is all the Product data from the database
33. Likewise, adding ``/id`` of one of the ``product ids`` in the browser URL should return one product's data
34. Try adding a separate number to the end of the ``id`` in the URL to replicate the ``Not found`` error in the browser (a 404), and you can verify by checking the ``Headers`` inside of the ``Network`` tab
35. In the next section, we are going to start using Postman and also start setting up ``GLOBAL`` variables

Section 4.24: Getting Started With Postman
------------

1. test
2. test 
3. test
4.
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19.
20.
21.
22.
23.
24.

Section 4.25: Custom Error Handling
----------------

1. test
2. test 
3. test
4.
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19.
20.
21.
22.
23.
24.