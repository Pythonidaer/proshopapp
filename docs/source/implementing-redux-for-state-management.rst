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

1.
2.
3.

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