Adding The Shopping Cart
=====

.. _adding-the-shopping-cart:

Section 6.32: Qty Select & Add To Cart Button
------------

1. In this video we add the quantity select on the ``ProductScreen.js`` page
2. Traversy wants that select to show the number of items that are in stock
3. So if there are 5 items in stock, then when we hit quantity, you'll only be able to select up to five of them 
4. Quantity is going to be part of our ``component level state``, so add in ``useState`` to react imports
5. Add ``const [qty, setQty] = useState(0)`` this sets the state of quantity to be 0 by default
6. Note: we only want to show the quantity component if the item is in stock, so Traversy uses some ``JSX``
7. See the file for more details: ``{product.countInStock > 0 && (<ListGroup.Item> ...)}``
8. Note that the Qty section uses items such as ``<Form.Control>`` with several ``props``
9. The ``as`` name is the underlying HTML element to use when rendering the FormControl (``as='select'``)
10. The ``value`` is the attribute of the underlying input (``value={qty}``)
11. ``onChange`` is a function that renders the input as plain text, generally used alongside ``readOnly``
12. Set the ``onChange`` function to contain contain an ``event`` where we ``setQty(e.target.value)}``
13. Traversy's following block of JSX code ``[...Array]...`` makes so if the stock is say, five, he makes an array with 0-5 values
14. Then he ``maps`` over the array, and displays an ``<option>``, eac having a ``key`` and ``value``
15. Rather than going from 0-4, Traversy adds ``x + 1`` so that we get, for example, 1-5 for 5
16. Now the ``product`` ``State`` ``countInStock`` value matches that of the ``Qty`` dropdown options (3 = 1-3)
17. When the ``countInStock`` is 0, the text just reads "Out Of Stock" and the "Add to Cart" button is ``disabled``
18. Observe how the "Add to Cart" ``<Button/>`` now has an ``onClick={addToCartHandler}`` added to the component 
19. Add the handler code below our ``userEffect()`` (at least that is what Traversy prefers)
20. ``const addToCartHandler = () => {}`` with the idea to go to the cart page with some parameters
21. Brad wants the ``product`` items and quantity as the query string 
22. This will require ``react-router`` functionality
23. Traversy uses v5 of ``react-router`` but we do not - ``history`` and ``match`` and no longer supported
24. The component now has ``const params = useParams()`` and ``const navigate = useNavigate()`` instead 
25. ``params`` is used in  ``dispatch(listProductDetails(params.id))`` inside the useEffect (and its dependencies)
26. ``navigate`` is used in ``const addToCartHandler = () => { navigate(`/cart/${params.id}?qty=${qty}`)}``
27. Notice how once the ``<Button/>`` is now clicked, the URL becomes ``localhost:3000/cart/a_long_id/qty=2``
28. Next, create ``CartScreen.js`` inside the ``screens/`` folder 
29. Don't forget to get more details by reviewing `the React Router docs <https://reactrouter.com/en/main/hooks/use-navigate/>`_ 
30. Generate the Cart Component 
31. Inside ``App.js``, import the ``CartScreen.js`` and observe the ``<Route>`` for it has a ``path='/cart/:id'``
32. Review the path we followed: Upload button redirect navigation -> create CartScreen component -> add to ``App.js``
33. Now when you visit CartScreen, it shows the word 'Cart', and if you click the top navigation link, it shows the ``CartScreen`` as well 
34. In the next video, Traversy handles the cart ``reducer``, along with an ``action`` that gets details from the database for that specific item in the cart 
35. This will also add it to the cart, which will be saved in local strage 
36. After that, we will build out the screen, which will show all the products in your cart

Section 6.33: Cart Reducer & Add To Cart Action
------------

1. Notice the common workflow is to add the ``constant``, the ``reducer`` or ``action`` then implement that action on the ``screen``
2. Create ``cartConstants.js`` in ``frontend/src/constants/``
3. Then ``export const CART_ADD_ITEM`` and ``const CART_REMOVE_ITEM``
4. Create ``cartReducers.js`` in ``frontend/src/reducers/``
5. Then ``import { CART_ADD_ITEM } from '../constants/cartConstants'``
6. Then ``export const cartReducer = (state = { cartItems: [] }, action) => {}``
7. Within the ``reducer``, proceed to add the ``switch`` syntax
8. Traversy emphasizes how this is going to be tricky because we have to handle if we click "add" and it's already there, if it exists, we have to handle that as well
9. ``const item = action.payload`` then ``const existItem = state.cartItems.find(x => x.product === item.product)``
10. ``if(existItem) { return {...state, cartItems: state.cartItems.map(x => x.product === existItem.product ? item : x)} else {return {...state, cartItems: [...state.cartItems, item] } }``
11. What the above accomplishes is adding either cart items to 0 items or cart items to existing items 
12. Navigate to ``store.js`` then ``import { cartReducer } from './reducers/cartReducers'``
13. Then combine this additional ``reducer`` and confirm on the ``localhost:3000/cart`` page the ``State`` in Redux Dev Tools
14. Go to ``frontend/src/actions`` then create ``cartActions.js``
15. Notice how we bring in ``axios`` because when we add an item to the cart, we want to make a request to ``api/products/:id`` to get the fields to get the data for that particular product to add to the cart
16. Also make sure to import the ``constants`` then create ``exporet const addToCart = (id, qty) => async (dispatch, getState) => {}``
17. Since we are saving our entire cart to localStorage, we can also use getState to get our entire state tree (``productList, productDetails, cart, etc``) aka anything in the store
18. Once we make our request, destructure the data from axios 
19. Once that's called, call ``dispatch({type: CART_ADD_ITEM, payload: {product: data._id, name: data.name, ...)}``
20. Notice how Traversy next sets these items to ``localStorage``
21. ``localStorage.setItem('cartItems', JSON.stringify(getState().cart.cartItems))``
22. In ``store.js``, create a variable ``cartItemsFromStorage`` to get items from ``localStorage`` if they exist or ``[]`` if nothing is there
23. In the next video, Traversy will start to implement the add to cart in the ``CartScreen`` then show all items in the cart as well
24. Note: taking notes for this section was a bit rushed, so when it comes to handling data specifics this may need to be revisted, especially with regards to the Redux flow, general JavaScript manipulation and usage of ``localStorage``

Section 6.34: Add To Cart Functionality
------------

1. 
2.
3.

Section 6.35: Cart Screen
------------

1. 
2.
3.

Section 6.36: Remove Items From Cart
------------

1. 
2.
3.