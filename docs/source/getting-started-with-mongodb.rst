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

1. test
2. test 
3. test

Section 4.19: Adding Colors To The Console (Optional)
------------

Section 4.20: Modeling Our Data
----------------

Section 4.21: Preparing Sample Data
------------

Section 4.22: Data Seeder Script
----------------

Section 4.23: Fetching Products From The Database
----------------

Section 4.24: Getting Started With Postman
------------

Section 4.25: Custom Error Handling
----------------