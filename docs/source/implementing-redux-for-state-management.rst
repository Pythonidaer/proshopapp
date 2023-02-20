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

1.
2.
3.

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