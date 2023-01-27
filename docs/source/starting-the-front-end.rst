Starting The Front End
=====

.. _starting-the-front-end:


Section 2.4: React Setup & Git Initialize
------------

1. Generate a boilerplate of a react application, including the library
2. Create new folder for project
3. Open with VSCode
``npx create-react-app frontend``
    This is the client, the front end, the UI part of our application
    The backend folder will be Node, Express, database, etc.
4. ``cd`` into the frontend folder, then run ``npm start`` to run our frontend dev-server
    On localhost:3000 by default
5. You'll notice the package.json has all the dependencies that we use
    (i.e. - react-dom is the library used for react to work with the document)
    (i.e. - react-scripts includes the dev server that we're running and stuff)
    NPM scripts such as ``npm run build``, which build out all of our static assets
    We can also run tests 
6. Navigate to ``index.html`` and observe that React is a single page application framework
    It is used to create single page applications
    The browser initially reads this single ``index.html``
7. Navigate to the src folder and into ``index.js``, which is the entry point
    It brings in React and React-DOM
    React-DOM has a method called Render, which takes our main app component from ``App.js``
    The Render places this component into an ``id`` via vanilla JavaScript that ``index.html`` picks up
8. **Please Note: ** every custom component that we create will be put into ``App.js``
9. Navigate back to the ``index.html`` and remove the comments
    Change the ``<title>`` tag in the ``<head>`` tag 
    Later in the course, we use react-helmet, which allows us to have custom page titles
    Change the ``<meta>`` description to something that makes more sense
    Update the ``favicon.ico`` file so that you no longer default to the React logo
    Delete the following unnecessary files: ``App.css``, ``App.test.js``, ``logo.svg``, and ``setupTest.js``
10. Navigate into App.js (where you can import images, svg, css, etc.) to remove above ``imports``
    In this tutorial we will be using function based components with hooks
    Notice that we will be using ``jsx``, which is similar to HTML but ``className`` is used as an attribute because ``class`` is reserved
    **Please Note: ** You can have JavaScript expressions within the curly braces of ``jsx``.
    (i.e. variable, conditional, ternary)
11. Remove everything within the ``App`` component besides the ``<div className="App"/>``
    Note that when you ``return`` output inside of a component, everything has to be wrapped in a single element (it doesn't have to be a ``<div>``)
12. Note that a *fragment* is an empty element
13. Delete everything inside of the ``index.css``
14. Change the ``function`` App syntax to ``const App = () => { return ( ... ) }``
    Using Git for version control is recommended for this course 
    Note that we will later on be deploying from GitHub to Heroku anyway
15. Consider ``ls -a`` then ``rm -rf .git`` to delete this git repository
    We want it in the root of the project and not the frontend folder
16. Move the ``.gitignore`` file into the root
    What this file does is allows you to describe any files/folders you don't want pushed to your repo (i.e. ``node_modules``)
    Add ``node_modules/`` because we'll have one in our root for all of our server dependencies
    We will also have one in our frontend (make sure to exclude both of these)
17. Ignore ``.env``, as the file will be all of our environment variables; our global variables
    We definitely don't want to contain sensitive information like API keys, MongoDB URI, etc.
18. ``cd ..`` out of the frontend folder 
    Enter ``git init`` in the console to initialize our repository (note we deleted one earlier)
    ``git add .`` > ``git status`` to see our staging ``git commit -m 'comment'``
    Make commits along the way
19. ``cd`` back into the frontend folder then run ``npm start``.
20. In the next video, we create ``<Header/>``, which also will have a navbar, and ``<Footer/>``, as well as some other things



Section 2.5: React-Bootstrap Setup, Header & Footer Components
------------

test

Section 2.6: HomeScreen Product Listing
----------------

Section 2.7: Rating Component
------------

Section 2.8: Note on React Router
----------------

Section 2.9: Implementing React Router
------------

Section 2.10: Product Details Screen
----------------

test