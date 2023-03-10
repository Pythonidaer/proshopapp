Implementing Redux For State Management
=====

.. _implementing-redux-for-state-management:

Section 5.26: An Overview Of Redux
------------

1. Redux is one of the more difficult technologies to try and explain, especially if you're new to React and the whole concept of ``state``
2. There is a pattern to this though
3. To learn more about Redux, state actions, reducers and more, read more `here <https://redux.js.org/understanding/thinking-in-redux/glossary>`_ 
4. We have two kinds of state: ``component level state`` and we have ``global state`` aka ``application state``
5. ``component level state`` has to do with a specific component (i.e. React - our ``components/`` and ``screens/`` files)
6. An example would be a slide or a drop down menu or something like that
7. Remember, a piece of component state may essentially just be a JavaScript ``object`` with some key-value pairs
8. For instance, you could have a value ``open`` which could be either ``true`` or ``false``
9. Depending on that true or false value, the menu would display as opened or closed
10. This is not what you would have in Redux, which is for ``application state``
11. An example in our project would be ``products``, because we want our products used in multiple components or maybe just things like access, update, add, delete and things like that
12. In the above case, we want the ``products`` available to all of our components (generally speaking)
13. You could put all of your state in the ``App.js`` file and pass pieces of state up and down through ``props``
14. However this gets very messy
15. That may be fine with very small, little applications with just a little bit of ``state``
16. Another example of ``global state`` in our project would be an authenticated user 
17. When we log in, we want to have access to that user's data that will be held in the state: the shopping cart items, orders, etc. and that would all be in the ``global state``
18. The way that ``state`` is changed is through ``reducers`` or ``reducer functions``
19. Basically, these functions accept ``actions``, and they're responsible for manipulating and passing the state down to components
20. ``actions`` are just ``objects`` that represent the intention to change a piece of ``state``
21. We also have ``action creators``, which are ``functions`` that will ``dispatch`` or fire off those ``actions``
22. As an example, we may have an ``action creator`` function called ``getProducts()``
23. In that, we make a *feature request* to the ``backend/`` to get data using ``axios`` or the ``Fetch API``
24. Then we get that data back, then we ``dispatch`` an action to the ``reducer`` and we attach a ``payload``
25. And that ``payload`` will have the fetch ``data``
26. In the ``reducer``, we can assign that ``payload`` data to the ``state`` and we can pass it down to any components that ask for it
27. Think of ``state`` as like a cloud hovering over your application 
28. When we want to click a button and fetch some data from the server and then display it, we have to create an ``action`` or an ``action creator`` to ``dispatch`` a specific ``action`` to the ``reducer`` then the reducer passes it down to the ``component``
29. Redux is not specifically attached to React (you can use it on its own, with other frameworks, etc.)
30. We're actually going to use a package called ``react-redux`` that connects the two together
31. Redux and React are just very popular to together 
32. In the next video, we install Redux and other packages, set up our boilerplate, then state to work with our product ``reducer`` and create some ``actions`` to get the ``data`` from the ``backend/``, because right now we just have that stuff right in the component, and that's not how we want to do it

Section 5.27: Create a Redux Store
----------------

1. Navigate to the chrome web store and insall the ``Redux Dev tools`` in your browser
2. This gives us an overall picture of our ``Redux store``, state and state changes from component to component 
3. It's pretty much mandatory
4. In the commandland, navigate to ``frontend/`` (you don't want to have it on your backend)
5. Type in ``npm i redux react-redux redux-thunk redux-devtools-extension`` which allows us to use React with Redux 
6. The thunk package allows us to make asynchronous requests inside of our ``action creators``, because we're going to have to talk to our server from those ``action creators``
7. Thunk is a piece of ``middleware``
8. The last package (extension) is because ``Redux Dev Tools`` don't work by default; they require a piece of code added to set it up
9. After installing, the first step is to create your ``Redux store`` files
10. In ``frontend/src/``, create a file called ``store.js``
11. This will be where we connect all of our ``reducers`` and any middleware, stuff like that
12. In ``store.js``, ``import { createStore, combineReducers } from 'redux'`` to create the store 
13. The second import allows you to have a bunch of ``reducers`` (each handling a certain piece of functionality) 
14. For example, if we're fetching products from the backend, we have a ``reducer`` for productList, and it'll have a request part, a success part if it's a successful response, then it'll have a fail in case of an error
15. We also want to add to the redux import ``{ applyMiddleware }`` so that we can apply any middleware such as ``thunk``
16. Then ``import thunk from 'redux-thunk'`` followed by ``import { composeWithDevTools } from 'redux-devtools-extension'``
17. Next, create a store: ``const store = createStore()`` and note that this is now legacy code from Redux core
18. Above that line, add ``const reducer = combineReducers({})`` then add that reducer variable as a parameter to the createStore() function below it 
19. We passed an empty object in ``reducer``, because we don't have any ``reducers`` just yet
20. When we do, we'll bring them inside the ``reducer`` variable and combine the reducers 
21. The next then we do is add the initial ``state`` (``const initialState = {}``) to the createStore as a second parameter
22. If we want something to be loaded when the Redux store loads, we can put it inside the ``initialState``
23. To learn more about the Redux Devtools Extension, read more `here <https://github.com/zalmoxisus/redux-devtools-extension#usage>`_ 
24. Next, add ``composeWithDevTools(applyMiddleware(...middleware))`` as the third parameter to ``createStore``
25. Above that line, add ``const middleware = [thunk]`` so that it spreads whatever is inside the middleware
26. ``export default store`` so we can then implement this into our application through a ``provider``
27. A ``provider`` in this case will come from React Redux
28. Navigate to our entrypoint for React, aka ``index.js``, and ``import { Provider } from 'react-redux'``
29. Next make sure to ``import store from ''./store'`` because store is passed into the provider
30. Note, the ``ReactDOM.render()`` should now contain ``<Provider store={store}> <App /> </Provider>,``
31. ``npm run dev`` from the root
32. Once the main page refreshes, you should now be able to see the Redux Dev Tools working
33. We will now be able to see all of our ``state`` from the Dev Tools once we have something in there (reducers, actions, a full store, etc.)
34. Now that our ``store`` is connected, in the next section we will begin ``fetching`` data through a ``redux action`` then passing the data down through ``state`` through a ``reducer``, instead of just fetching the data right from the ``component`` like we currently are

Section 5.28: Product List Reducer & Action
------------

1. Now we get into the whole flow of creating a ``constant``, creating ``reducer`` and ``action`` then bringing that into our components
2. In ``frontend/src/`` create a folder called ``reducers/``
3. Each resource of our application will have a ``reducer`` file such as products: ``productReducers.js``
4. The above filename is plural because it's going to have a bunch of different reducer functions in there, all related to products
5. The first one we will create is ``productListReducer``, which is going to handle the state for the product lists, which we see on the Home Page
6. A reducer takes in two things: the ``initial state`` (such as an empty object), then it takes an ``action``
7. Start off with this code: ``export const productListReducer = () => {}``
8. When we create an ``action``, we're going to ``dispatch`` or we ``create`` an ``action reducer``, we are going to dispatch an action to this reducer
9. This object will have a ``type``, and we will evalate that type to do a certain thing depending on what ``type`` that is
10. It might also contain a ``payload``; this one will as it's going to add in products and set that to an empty array
11. In the initial ``state``, add in ``state = { products: [] }``
12. We use a switch syntax to evaluate the type that's in the action object 
13. Add in the code block this syntax: ``switch (action.type) { ... }`` - there will be 3 different ``types`` that we look for
14. One is the products list ``request``, where it's when we actually make the request 
15. One is going to be the product list ``success``, which is if we get a successful response and we get the data 
16. One is going to be it if fails then we send an ``error`` through the ``state``
17. Add in this first ``case 'PRODUCT_LIST_REQUEST': return { loading: true, products: [] } ``
18. In all of our cases, we just want to return this piece of this part of the ``state``
19. We set ``loading`` to true in the request case, because when we make the request, we want the component to know that it's currently ``fetching``, so it's currently loading
20. The returned ``products`` empty array is because the request hasn't been fulfilled yet, so we don't have data populating it from the database 
21. Next, add the ``case 'PRODUCT_LIST_SUCCESS':, and return { loading: false, products: action.payload }`` because it's done loading once the request has completed successfully
22. As you can see above, ``products`` will be filled with that ``action`` object; they'll be a ``payload`` attached to it, so we're going to fill products in the ``state`` with that ``payload`` data
23. ``action.payload`` will make more sense once we create the actual ``action function``
24. Next, if we try to fetch data and we get an error like a ``404``, then the product list will fail 
25. Therefore, add this ``case 'PRODUCT_LIST_FAIL': return { loading: false, error: action.payload }`` because we will also send the error through the action payload if that happens
26. The default will be ``default: return state``, with the state being the initial ``state = { products: [] }``
27. In order to use this ``reducer``, we need to actually add it to our store
28. That would be ``import { productListReducer } from './reducers/productReducers'``
29. Add this to the ``combineReducers`` param object: ``productList: productListReducer``
30. This is important as that is what's going to appear in the state ``productList``
31. Now if you return to the browser Redux tools, ``productList`` appears with a ``products: []`` inside the State tab
32. Before we get into ``actions``, Traversy tells us about ``constants``
33. Constants just means our ``case values`` for the ``reducer switch syntax`` will be in ``consts`` that doesn't change, even though it ultimately will have the same string values
34. Not everbody uses ``constants``, but this new ``src`` folder ``constants/`` will give us a central place for all of our cases, all of our ``constants``
35. In ``constants/`` create ``productConstants.js`` and ``export const`` for each ``case type`` in ``productReducers.js``
36. For instance, ``export const PRODUCT_LIST_REQUEST = 'PRODUCT_LIST_REQUEST'`` and for SUCCESS and FAIL also
37. Back in ``productReducers.js``, import the above three consts ``... from '../constants/productConstants'``
38. Then replace the ``strings`` with the ``constants``
39. Next, in the ``src/`` folder create an ``actions/`` folder, then create ``productActions.js`` inside of it
40. You will notice how we ``create the constant --> the reducer --> the action --> fire it off in the component``
41. We want to bring in the ``constants`` into our action file as well
42. After importing, make sure at the bottom to ``export const listProducts = () => {}``
43. What this action will do is pretty much what we did in our ``useEffect`` in the ``HomeScreen`` component
44. So, we fetched from API products and we got that data back, then we just map through them down instead of fetching them directly
45. We are going to do this through this action and we're going to ``dispatch actions`` to the ``reducer``
46. Think of the functions on these ``productAction.js`` files as ``action creators``, and the actual ``actions`` (i.e., the ``constants``) that we dispatch back to the ``reducer`` like ``PRODUCT_LIST_REQUEST``
47. So, think of those reducer case types as ``actions``, where each type we are looking for is a potential action
48. In short, ``action reducers`` are functions, and the constants are actual ``actions`` (``reducers are functions``)
49. This is where Redux Thunk comes in (we want to make an asynchronous request)
50. ``redux-thunk`` allows us to basically add a function within a function 
51. This is how we can dispatch these actions: ``export const listProducts = () => async (dispatch) => { ... }``
52. Inside the action creator, add a ``try {} catch {}`` block and first try to ``dispatch()`` the request
53. Within the ``try`` add this: ``dispatch({ type: PRODUCT_LIST_REQUEST })`` to set ``loading`` to true (see the reducer aligning with this ``constant/action`` case type)
54. In the ``productActions.js``, ``import axios from 'axios'`` then destructure data: ``const { data } = await `` ...
55. After the ``await`` above, finish the variable with this: ``axios.get('/api/products')`` to give us the data
56. Then, under that part of the ``try`` block, ``dispatch({ type: PRODUCT_LIST_SUCCESS })``
57. In the ``try`` is the REQUEST and SUCCESS, because if it FAILS, then it'll fire down in the ``catch (error) { ... }``
58. When it works, we want to send the ``payload`` as the ``data``, so in the SUCCESS dispatch object also add ``payload: data``
59. This aligns with the ``productReducers.js`` case where SUCCESS constant returns ``{ loading: false, products: action.payload }``
60. Observe how in the reducer receives the action conditionally dispatched based on what constant it was provided 
61. If something goes wrong, then we want to ``dispatch({ type: PRODUCT_LIST_FAIL })`` in the ``catch {}`` block 
62. Here, also add to the dispatch ``payload: error.response && error.response.data.message``
63. Here we want to get whatever the error message is like (test in Postman if you want: ``{{URL}}/api/products/1``)
64. This way we can that put into the payload, which means we can get our ``backend/`` errors and have them in our ``frontend/`` state
65. The ``error.response`` is just a generic message, but if we have a custom message it will be ``data.message``
66. That will give us the message we set up in postman (see ``errorMiddleware.js`` for more info)
67. Update the dispatch payload for FAIL to read this completely: ``error.response && error.response.data.message ? error.response.data.message : error.message``
68. This creates a ternary that checks for if both exist to use the custom, otherwise to use the default error message 
69. This payload will be very common in all of our requests, since we just want to fill it with the error message
70. In our ``HomeScreen``, we want to fire this action off, so that is what we are going to do in the next video


Section 5.29: Bringing Redux State Into HomeScreen - useDispatch & useSelector
----------------

1. In the last video, we created ``constants`` for the ``productList`` ``reducer``, which handles the listing of products in the ``state``, then also listed the ``listProducts`` ``action``
2. Now, the ``listProducts action`` needs to be *fired off* in the ``HomeScreen``
3. Traversy starts by clearing out the ``useEffect(() => {}, [])``
4. Note that we no longer need to set products as our local state anymore or our component level state
5. We don't even need useState in HomeScreen
6. To ``dispatch`` our ``listProducts`` action, we have to bring that in from ``react-redux``
7. ``import { useDispatch, useSelector } from 'react-redux'`` 
8. useDispatch will be used to dispatch or call in ``action``
9. useSelector is used to select parts of the ``state``
10. To dispatch we first need to define a variable called ``dispatch`` and just set that to ``useDispatch``
11.  ``import { listProducts } from ''../actions/productActions'``
12. Again we want to fire this off in the useEffect because it does the same thing as before, it makes the request to the ``backend/`` to get ``products``
13. Add in the useEffect: ``dispatch(listProducts())``
14. Since we're using dispatch in the useEffect, also add ``dispatch`` as a dependency in the [] of the ``useEffect``
15. Just that alone should call listProducts and fill up our state
16. Make ``const products = []`` below that
17. Refresh ``localhost:3000`` and observe the ``Diff`` in ``state`` from the Redux Dev tools
18. Observe both actions fired off: ``PRODUCT_LIST_REQUEST`` then ``PRODUCT_LIST_SUCCESS``
19. This occurs because we ``dispatched`` ``listProducts`` from our ``HomeScreen.js`` (inside the ``useEffect``)
20. In our ``listProduct`` action (on ``productActions.js``), the action is fired and happened to be successful 
21. Because it was successful, it passed the data into the ``payload``
22. In our ``reducer`` (in ``productReducers.js``), that ``payload`` is getting put into ``products`` on a successful response
23. If we look inside ``products`` in the ``Diff``, we can see that it's filled with product data
24. Observe also that the products appear in the ``State`` of the Redux Dev Tools
25. To actually display those, we have to select it from ``state``, which is where ``useSelector`` omes in
26. ``const productList = useSelector(state => state.productList)``
27. We want to call the above whatever we call it in the ``store.js``
28. ``useSelector`` takes in an arrow function then what part of the state that we want (so for this, productList)
29. Now we can ``destructure`` what we want from product list 
30. ``const { loading, error, products } = productList``
31. This is all parts of that ``state`` that could be sent down (review what's returned in ``productReducers.js``)
32. Next up, remove the empty ``const products = []`` then prepare for checking to see if state is loading or in error
33. ``{loading ? <h2>Loading...</h2> : error ? <h3>{error}</h3> : ...}``
34. In the ``...`` above, insert the entire ``<Row>`` code into the JSX
35. At this point, we should now be getting our ``products``, even the ``Loading...`` momentarily when it is true
36. In our ``route`` in ``productRoutes.js``, you can change ``router.get('/', ...)`` to test out errors 
37. Under ``products``, add ``res.status(401)`` then ``throw new Error('Not Authorized')``
38. Now, when we refresh the page we only see ``Not Authorized`` as we added in Step 33. (in the ``JSX`` block)
39. Undo the changes in the routes page
40. To recap, using the ``useSelector`` allows us to get those pieces of state (our products) that we get from Redux 
41. This data now appears inside of our ``HomeScreen`` component because of the ``useSelector`` code
42. Traversy says there's two parts: firing off the ``action`` to actually get the product, send it through the ``reducer`` down into the ``state``
43. Then there's the ``useSelector()`` to actually grab it from the ``state`` then pull out what we want from it and display it in our output
44. In the next videos, we will create a ``<Loader>`` spinner, then a ``<Message>`` component for nice alerts

Section 5.30: Message & Loader Components
------------

1. Now we will replace ``loading ? (<h2 ...>)`` and ``: error ? (<h3 ...>)`` with components
2. In ``components/``, create ``Loader.js`` and ``Message.js``
3. Use the ``rafce`` + tab shortcut to generate a React component for each 
4. For ``Loader.js``, also ``import { Spinner } from 'react-bootstrap'``
5. In the ``return``, swap out the <div> with ``<Spinner animation='border'> ... </Spinner>``
6. To see everything that's available, header over to `the React-Boostrap documentation on Spinners <https://react-bootstrap.github.io/components/spinners/>`_ 
7. Assign the ``<Spinner>`` a ``role`` and a ``style``
8. Within the Spinner, add a ``<span>`` (see file for className information)
9. For ``Message.js``, ``import { Alert } from 'react-bootstrap``'
10. This component will receive two ``props``: ``{ variant, children }``, the latter being the text we want inside
11. To see everything that's available, header over to `the React-Boostrap documentation on Alerts <https://react-bootstrap.github.io/components/alerts/>`_ 
12. Add a ``defaultProps`` to the ``Message`` component, so that its ``variant`` defaults to a light blue ``Alert``
13. Navigate to ``HomeScreen.js`` and import both components
14. Replace the ``loading`` and ``error`` headings with components (see file for more specific detail)
15. To test the error (``<Message>``), navigate to ``productRoutes.js`` and in ``router.get('/', ...)`` ``throw new Error('Some error')`` before responding with the json
16. If you look inside the ``state Diff`` Redux tool, we get an ``error`` because our ``productList`` is failing (you can see the ``PRODUCT_LIST_FAIL`` at the top)
17. Notice how when you undo the route error and refresh the page, the ``productList`` state no longer shows an ``error`` because ``PRODUCT_LIST_SUCCESS`` shows 
18. In other words, the ``action.payload`` is different because a separate ``constant/action`` was fired off
19. In the next page, we will work on the product details page
20. Rather than fetch from the component, we want to have a ``productDetailsReducer`` with a listProduct/getProductDetails actions, and get this from the global Redux state

Section 5.31: Product Details Reducer & Action
----------------

1. To repeat what we did on the ``HomeScreen`` on the ``ProductScreen.js``, we want to ``fetch`` data from the ``state``
2. Create a ``productDetailsReducer``, an ``action``, get the ``data`` within the component with ``useSelector`` then fire it off with ``useDispatch`` 
3. Note that this is kind of the flow for the rest of the course
4. Whenever you want to add a new piece of *functionality*, make a new request or whatever, this is the structure that Travery suggests
5. Start off with the ``constants/`` ``productConstants.js``(``PRODUCT_DETAILS_...``)
6. Next, go to the ``productReducer.js`` and copy paste the productListReducer and rename it to ``productDetailsReducer``
7. Change the state to be ``{ product: { reviews: [] } }`` as the initial state
8. Observe how the ``constants`` are actually just ``types`` of ``actions``
9. For ``PRODUCT_DETAILS_REQUEST``, use a spread operator to add whatever else is in the current ``state``
10. For ``PRODUCT_DETAILS_SUCCESS``, set the ``action.payload`` to the ``product``
11. Remember that whenever we create a new ``reducer`` we have to add it to our ``store.js``
12. Inside ``const reducer``, add the value ``productDetails: productDetailsReducer`` and make sure to import this also
13. Traversy likes breaking things up into separate reducers, because it makes it easier for him to ``debug``
14. Also, because it causes less issues with like wrong pieces of state being displayed and whatnot
15. After we add our ``reducer`` to our ``store``, we want to create our ``action``
16. We know we want to make a ``request`` to our ``backend/`` and make a ``request`` to ``/api/products/:id``
17. In ``productActions.js``, observe the ``listProductDetails`` ``action`` and observe how it takes an ``id`` arg
18. Notice how the ``error`` stays the same, or rather the entire ``catch`` block and ``dispatch`` for FAIL 
19. Observe how in the ``try`` block we once again destructure and ``await`` the data we get from the route request 
20. This is because the request returns a ``Promise``
21. The ``id`` is passed into the route from the ``action`` parameter
22. After finishing the ``action``, move into ``ProductScreen.js`` and remove the ``axios`` import 
23. You can also remove the destructured ``useState({})`` since we're no longer calling it 
24. Clear out the ``useEffect`` and ``import { useDispatch, useSelector } from 'react-redux'``
25. Inside the ``ProductScreen``, note that the video shows ``match`` but ``react-router version 6`` no longer uses this 
26. Add ``const dispatch = useDispatch()`` as we want to ``dispatch`` the ``action`` that we just created
27. Add ``dispatch()`` into the ``useEffect()``
28. To learn more about useEffect, visit `the React documentation on effect hooks <https://reactjs.org/docs/hooks-effect.html/>`_ 
29. ``import { listProductDetails } from '../actions/productActions'``
30. ``dispatch(listProductDetails(params.id))``
31. Note some of the ``v6`` imports here: ``import { Link, useParams, useNavigate } from 'react-router-dom'``
32. Rather than use match, within the component add ``const params = useParams()`` to extract the params.id
33. Notice how this lines up with the ``action`` and is how we get the parameter for that through ``react-router-dom``
34. Make sure to add in ``dispatch`` and ``params`` as your arrayed dependencies
35. Temporarily add ``const products = {}`` and observe how the screen doesn't yet show the data but doesn't error 
36. Next observe in the ``Diff`` how the object data appears, along with the REQUEST and SUCCESS actions
37. Under ``dispatch``, add ``const productDetails`` and assign it to ``useSelector(state => state.productDetails)``
38. Below that, destructure `const { loading, error, product } = productDetails`
39. In the ``return``, below ``</Link>``, add an expression similar to the last component ``{loading ? <Loader /> : error ? <Message variant='danger'>{error}</Message> : ()}`` and paste the ``<Row>`` inside that final empty parenthesis
40. Reload the page and you should see the products, the loader, *coming from the server and coming through Redux down through our state*
41. As you can see, every ``action`` that is called is shown in the Redux toolkit
42. In the next section, we will add the ``cart`` reducer and actions because we're going to have to do something to the cart 
43. We're going to make a request to get the data for that item from the database and have it in our cart 
44. We're also going to be using ``localStorage`` so that we can save whatever is in our cart in the browser