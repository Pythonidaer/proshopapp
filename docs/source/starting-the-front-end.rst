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

1. Set up ``HomeScreen.js`` and list out all of our products
2. We will use a JavaScript file with a products array with some dummy data
3. Later on we wil be actually fetching products from our backend and ultimately from a db
4. For now though we should have in our project files an ``images/`` folder and a ``products.js`` file 
5. Copy the ``images/`` folder into the ``public/`` folder (they are the product photos)
6. Bring the ``products.js`` file into the ``src/`` folder
7. Observe that products.js is an array of objects, with key values of string and number
8. One of the important notes about the ``image:`` key is that its value is to the ``image/`` folder 
9. In our ``src/`` folder create a new folder called ``screens/`` > ``HomeScreen.js``
10. ``rafce`` then tab in the file 
11. ``import products from '../products'``
12. What we want to do here is loop through all the products and then output
13. Each one will be its own product component, which we create in a little while
14. Replace the component's ``<div>`` with an empty fragment ``<> </>``
15. Add in a Bootstrap ``<Row>`` and ``import { Row, Col } from 'react-bootstrap'``
16. Inside the ``<Row>`` loop through our products that we imported above
17. i.e. like ``{products.map(product => (<Col sm={12} ><h3>{product.name}</h3></Col>))}``
18. Go to our ``App.js`` then ``import HomeScreen from './screens/HomeScreen'``
19. Within the ``<Container>`` add ``<HomeScreen />`` then review the page again
20. This way we are able to bring the products into the file and loop over them 
21. Go back to the HomeScreen code and replace the ``<h3>``s with ``<Product />``
22. Remember that Components can take in ``props``
23. In this case we will be accessing ``product={product}`` in ``<Product>`` passed from above
24. ``import Product from '../components/Product'``
25. Navigate to ``src/components/`` and create ``Product.js`` then use the ``rafce`` shortcut
26. Add in a ``<Card>`` and make sure this is ``imported`` from ``react-bootstrap``
27. When we implement ``react-router`` we will use the ``<Link>`` tag but for now juse use ``<a>``
28. Within the ``<Card>`` add ``<a href={`/product/${product._id}`}>``
29. Within that ``<a>`` Add in ``<Card.Img src={product.image} variant='top' />``
30. Next, within the ``Product`` functional component, destructure ``({product})`` as a prop
31. You should now see columns of images on the main page 
32. Go back to the ``Product`` and below the link with the image and add ``<Card.Body>``
33. Paste in the ``<a>`` code from above but change ``<Card.Img>`` to ``<Card.Title as='div'>``
34. Within the ``Card.Title`` add ``<strong>{product.name}</strong>``
35. Before the ending of the ``</Card.Body>`` add ``<Card.Text as='div'>`` then a ``<div>``
36. Within this ``<div>`` add ``{product.rating} from {product.numReviews} reviews``
37. Below the ``</Card.Text>`` add another ``<Card.Text as='h3'>`` and add ``${product.price}``
38. In the next video, we will be adding the ``<Rating>`` component



Section 2.7: Rating Component
------------
1. We will create the ``<Rating>`` component to make stars appear along with Font Awesome icons.
2. ``import Rating from './Rating'`` and remove the ``{product.rating} from {product.numReviews} reviews`` <div>
3. Here ``<Rating/>`` will take in 2 props: ``value={product.rating}`` and ``text={`${product.numReviews} reviews`}``
4. Go to the ``components/`` folder and create a ``Rating.js`` file, then use the ``rafce`` syntax 
5. ``Rating`` arrow function component will take the 3 props ``{ value, text, color }`` 
6. Create ``<span>`` within to represent each one (?)
7. Head to `FontAwesome.com <https://fontawesome.com/icons/star-half-stroke?s=regular&f=classic>`_ to choose the stars you want to use 
8. Which star we show is going to depend on the value that's passed in, which is the product rating
9. The conditional code in ``Rating.js`` will always show 5 ``<span>`` tags nested with FontAwesome ``<i>`` icons, however the ``value`` attribute/prop will determine whether the star is filled, half, or empty
10. We also use a span for ``{text && text}`` to short-circuit evaluate 
11. In React we can add inline styles, but we need to use double curly braces ``style={{color}}``
12. For example we could add ``color='red'`` but here we will want to have a default yellow
13. For a default Prop value, in the bottom of ``Rating.js`` we can set ``defaultProps`` object
14. In ``Rating.js`` add ``import PropTypes from 'prop-types'`` to specify the type of each prop we're using (this is optional)
15. This will now type-check our props 
16. Beware the warning ``Warning: Each child in a list should have a unique "key" prop.``
17. What that means is that when we create a list such as we did in ``HomeScreen.js`` the element has to have a ``key`` and that needs to be unique
18. So, back on ``HomeScreen.js``, make each looped ``<Col key={product._id}>`` and that warning should go away 
19. Navigate to ``index.css`` to add ``.rating span { margin: 0.1rem }``
20. At this point you should be able to see both our ratings and our number of reviews 
21. In the next video, Traversy will start to implement the routing
22. We will be able to click a link and go to a separate ``ProductScreen``
23. Search for the React Web Tools from chrome web store 
24. Search for the Redux Dev Tools and install
25. Now in the console, with the React tools we can see the tree of Components, including the Bootstrap components 
26. This will also show you the props that are passed into each Component
27. In the next video, we set up React Router 
28. React Router v6 has been released and has some changes, so see the video below to begin 


Section 2.8: Note on React Router
----------------

1. Review Traversy's video on `React Router v6 <https://www.youtube.com/watch?v=k2Zk5cbiZhg&t=1s/>`_ changes
2. React Router v6 breaks a lot of things from v5 (outdated)
3. As an aside, ``npm i react-router-dom@latest`` updates to the latest version for npm packages
4. One error to resolve is ``Error: A <Route> is only ever to be used as the child of <Routes> element, never rendered directly. Please wrap your <Route> in a <Routes>``
5. The ``<Switch>`` element does not exist anymore - it's been switched to ``<Routes>``
6. Now you have to wrap your ``<Route>``s in ``<Routes>`` (see ``App.js``) for an example 
7. ``import { BrowserRouter as Router, Routes, Route } from 'react-router-dom'``
8. The ``<Route>`` components now have an ``element`` attribute that that takes in JSX 
9. ``exact`` is no longer needed for routes 
10. Also note the error ``Error: [h3] is not a <Route> component. All component children of <Routes> must be a <Route> or <React.Fragment>``
11. When adding a ``<Route>``, make sure to ``import`` the component! (see: ``App.js``)
12. Params are still dealt with similarly as did v5, i.e. ``path='/task/:id'`` 
13. ``<Link to={`/task/${task.id}`>`` syntax remains the same as from v5 
14. Another import of note is the ``userParams`` functionality from ``react-router-dom``
15. The above is how we get params (i.e. id's); these can also be destructured 
16. You can test this object out by ``const params = useParams()``, then ``console.log(params)``
17. The above replaces the destructuring of such object items as ``match``, because these props are not available anymore 
18. "Redirect" has also been replaced with ``Navigate`` in ``react-router-dom``
19. i.e. ``if(error){return <Navigate to='/'> />}``
20. There is also a ``useNavigate`` hook! For more information on hooks, see React documentation 
21. First do ``const navigate = useNavigate()``, then for example ``if(res.status === 404){navigate('/')}``
22. ``navigate(-1)`` will take us to the last page
23. ``useLocation()`` is another hook available in ``react-router-dom`` for location data such as ``pathname``
24. Again, this could be destructured ``const { pathname } = useLocation()``
25. To recap, no more <Switch>, you have to use <Routes>, new attribute with JSX, new hooks
26. For more info on React Router Hooks: `Using Hooks: React Router <https://blog.logrocket.com/using-hooks-react-router/>`_ 



Section 2.9: Implementing React Router
------------

1. In this video, we implement the React Router so that we can have different routes, different URLs that we can go to in our project in our front end
2. First off, make sure you're in the ``frontend/`` folder and we're going to ``npm i react-router-dom react-router-bootstrap``
3. We also want to install the ``react-router-bootstrap`` package, because when we're dealing with links in the navbar or buttons and stuff, we want to use that
4. Go to ``App.js`` to implement the ``<Router>`` (see Section 2.8, Step 7)
5. ``BrowserRouter`` uses the HTML5 History API, i.e. push state and replace state, and also hash router
6. We can alias the above with the following syntax: ``import {BrowserRouter as Router} from react-router-dom``
7. We needed to wrap our entire App with the ``<Router>`` in order to use it (return ())
8. Whenever we want to create a ``<Route>``, we provide a ``path`` and what component we want to load when we go to that path 
9. As an example: ``<Route path='/' element={<HomeScreen />} />``
10. Navigate to the ``screens/`` folder in VSCode and create a new file: ``ProductScreen.js``
11. Generate a component 
12. In ``App.js``, bring that screen in (ProductScreen)
13. Create a route for that, but with the path to be: ``path='/product/:id'``
14. The ``/:id`` is a placeholder, and that's going to be looked at as the ``id`` param
15. Make the ``element`` equivalent to the ``<ProductScreen />`` component
16. Reviewing the ``Project.js`` file, you can see how the ``<Link>`` uses ``project._id``
17. Next we fix the ``<Header>`` links so that we maintain a single-page application 
18. Navigate to ``components/Header.js`` and ``import { LinkContainer } from 'react-router-bootstrap'``
19. Observe that in ``Product.js`` we ``import { Link } from 'react-router-dom'``
20. Replacing ``<a>`` tags with ``<Link>`` tags removes the reloading of the pages and is much faster 
21. ``<LinkContainer>`` from ``react-bootstrap`` allows us to wrap bootstrap components 
22. ``<LinkContainer>`` can be used multiple times within the same component 
23. In the next video, we will implement the ``<ProductScreen>``
24. In the beginning, we will just take from the ``product.js`` file from the array
25. Ultimately, this data will come from the backend (when seeded), but we use this in the beginning just to get our data showing
26. Note: This strategy should be utilized in projects moving forward (i.e. Reactionary)



Section 2.10: Product Details Screen
----------------

1. Now we start on the Product page itself, or ``<ProductScreen/>`` 
2. test 
3. test 
4. test 
5. test 