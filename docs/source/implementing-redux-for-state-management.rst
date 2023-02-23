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

1.
2.
3.

Section 5.30: Message & Loader Components
------------

1.
2.
3.

Section 5.31: Product Details Reducer & Action
----------------

1.
2.
3.