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

1. Create Header and Footer components
2. Implement React-Bootstrap
3. ``src/ components/`` (Header, Footer, Search Box, etc.)
4. Screens: Home, Product, Profile, etc will also be React components
5. However these will go in a separate folder called ``screens/``
6. Naming convention for components is as so: ``Header.js``
7. Typing in ``rafce`` (React Arrow Function Component Export) short-cut works great here
8. Change ``<div>`` to ``<header>header</header>``
9. Also create a ``Footer.js`` Component and change the ``<div>`` to a ``<footer>footer</footer>``
10. Navigate to ``App.js`` then import the Components above (Header, Footer)
11. Because the Components are ``export`` as ``default``, they don't need to be imported in curly brackets (``{}``).
12. ``import Header from './components/Header'`` repeat for footer
.. .. code-block:: js
..    :caption: .App.js
..    :emphasize-lines: 4-8

..    const App = () => {
..     return (
..         <>
..         <Header />
..         <main>
..             <h1>Welcome To ProShop</h1>
..         </main>
..         <Footer />
..         </>
..     )
.. }
13. Test in Browser
14. Navigate to `react-bootstrap.github.io <https://react-bootstrap.github.io/>`_ to get set up with the UI library we are using.
15. This will allow us to use a variety of React-Bootstrap prebuilt components (like ``<Button>``) as well as subcomponents (less things needed to be brought in than material-ui)
16. There is also a material-ui library if you are looking for an alternative
17. Bootswatch.com shows us free themes for bootstrap that are pre-customized
18. Click the arrow beside your theme of choice and download the ``bootstrap.min.css`` 
19. Drag this downloaded file within the ``src/`` folder beside the ``index.css`` file
20. Navigate to ``index.js`` and ``import './boostrap.min.css'`` file
21. Review the application to see if the fonts have changed
22. ``cd`` into your ``frontend/`` and for this dependency run ``npm i react-boostrap``
23. ``Containers`` will move everything into the middle
24. In ``App.js`` ``import { Container } from 'react-boostrap'``
25. Within ``<main>`` wrap a ``<Container>`` so that it holds the ``<h1>`` tag
26. ``import`` {Container, Row, and Col} from ``react-boostrap`` in the ``Footer.js`` file
27. Review the React-Bootstrap documentation for more information on these Components
28. Inside your ``index.css`` file, make ``main { min-height: 80vh; }`` to push the ``<footer>`` down
29. Copy ``<Navbar>`` code from React-Bootstrap into the ``<header>`` tag in ``Header.js``
30. Make sure to ``import`` {Navbar, Nav, Container} ``from 'react-boostrap'``
31. Remove the ``<Form>`` Component code as Traversy gets to that later
32. Get rid of the ``<NavDropdown>`` as well for the same reason
33. Later on we ``import`` from ``react-router-bootstrap'`` for this 
34. So if you review the video, now is ``<Nav.Link>`` but later is ``<LinkContainer>``
35. Label your ``<Navbar.Brand>`` then set ``<Navbar>`` ``bg="dark"`` and ``variant='dark'``
36. Also add ``collapseOnSelect``
37. Add the ``<Container>`` right within the ``<Navbar>`` tags
38. Navigate to `cdnjs.com <https://cdnjs.com/>`_ then search for font-awesome
39. Once you find the ``all.min.css`` link, click the 'copy link' tag
40. Navigate to your ``public/index.html`` file and add the CDN into the ``<head>`` tag
41. This allows us to use icon classes
42. An example of this code in ``Header.js`` includes ``<i className='fas fa-shopping-cart'></i>``
43. Note that we use various Bootstrap classes without this course for styling
44. In the next section, we begin our ``Homescreen`` and bring in some products
45. This will initially be a ``JavaScript file`` with an array of products
46. We will work with this for a little while then start to move on to the ``backend/`` serving products from there, connecting to our database, etc.




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