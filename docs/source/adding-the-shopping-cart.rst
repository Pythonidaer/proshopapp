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
16.
17.
18.
19.
20.

Section 6.33: Cart Reducer & Add To Cart Action
------------

1. 
2.
3.

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