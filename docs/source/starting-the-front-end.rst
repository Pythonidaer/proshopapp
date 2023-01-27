Starting The Front End
=====

.. _starting-the-front-end:


Section 2.4: React Setup & Git Initialize
------------

1. Generate a boilerplate of a react application, including the library
2. Create new folder for project
3. Open with VSCode ``npx create-react-app frontend``
4. This is the client, the front end, the UI part of our application
5. The backend folder will be Node, Express, database, etc.
6. ``cd`` into the frontend folder, then run ``npm start`` to run our frontend dev-server
7. On localhost:3000 by default
8. You'll notice the package.json has all the dependencies that we use
9. (i.e. - react-dom is the library used for react to work with the document)
10. (i.e. - react-scripts includes the dev server that we're running and stuff)
11. NPM scripts such as ``npm run build``, which build out all of our static assets
12. We can also run tests 
13. Navigate to ``index.html`` and observe that React is a single page application framework
14. It is used to create single page applications
15. The browser initially reads this single ``index.html``
16. Navigate to the src folder and into ``index.js``, which is the entry point
17. It brings in React and React-DOM
18. React-DOM has a method called Render, which takes our main app component from ``App.js``
19. The Render places this component into an ``id`` via vanilla JavaScript that ``index.html`` picks up
20. **Please Note: ** every custom component that we create will be put into ``App.js``
21. Navigate back to the ``index.html`` and remove the comments
22. Change the ``<title>`` tag in the ``<head>`` tag 
23. Later in the course, we use react-helmet, which allows us to have custom page titles
24. Change the ``<meta>`` description to something that makes more sense
25. Update the ``favicon.ico`` file so that you no longer default to the React logo
26. Delete the following unnecessary files: ``App.css``, ``App.test.js``, ``logo.svg``, and ``setupTest.js``
27. Navigate into App.js (where you can import images, svg, css, etc.) to remove above ``imports``
28. In this tutorial we will be using function based components with hooks
29. Notice that we will be using ``jsx``, which is similar to HTML but ``className`` is used as an attribute because ``class`` is reserved
30. **Please Note: ** You can have JavaScript expressions within the curly braces of ``jsx``.
31. (i.e. variable, conditional, ternary)
32. Remove everything within the ``App`` component besides the ``<div className="App"/>``
33. Note that when you ``return`` output inside of a component, everything has to be wrapped in a single element (it doesn't have to be a ``<div>``)
34. Note that a *fragment* is an empty element
35. Delete everything inside of the ``index.css``
36. Change the ``function`` App syntax to ``const App = () => { return ( ... ) }``
37. Using Git for version control is recommended for this course 
38. Note that we will later on be deploying from GitHub to Heroku anyway
39. Consider ``ls -a`` then ``rm -rf .git`` to delete this git repository
40. We want it in the root of the project and not the frontend folder
41. Move the ``.gitignore`` file into the root
42. What this file does is allows you to describe any files/folders you don't want pushed to your repo (i.e. ``node_modules``)
43. Add ``node_modules/`` because we'll have one in our root for all of our server dependencies
44. We will also have one in our frontend (make sure to exclude both of these)
45. Ignore ``.env``, as the file will be all of our environment variables; our global variables
46. We definitely don't want to contain sensitive information like API keys, MongoDB URI, etc.
47. ``cd ..`` out of the frontend folder 
48. Enter ``git init`` in the console to initialize our repository (note we deleted one earlier)
49. ``git add .`` > ``git status`` to see our staging ``git commit -m 'comment'``
50. Make commits along the way
51. ``cd`` back into the frontend folder then run ``npm start``.
52. In the next video, we create ``<Header/>``, which also will have a navbar, and ``<Footer/>``, as well as some other things



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