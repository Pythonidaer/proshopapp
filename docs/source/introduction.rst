Introduction
=====

.. _intro:

Welcome, Project Demo & Resources
---------------------------------

To use ProShopApp, visit the  `Udemy course. <https://www.udemy.com/share/103Cb63@kNDD1NIkFuxNhxVvYAdSwy5PT9fv4_lv6sUm118z5LwRLMPAWjHVWvEjNdZUCwZj/>`_ 

Section 1.1: Course Welcome
---------------------------

This is a sample,
I don't really need to document this section.

I am also learning about how to structure rst files such as these.

rsts stand for `reStructuredText <https://en.wikipedia.org/wiki/ReStructuredText>`_ ``More`` can be read in the `Sphinx Documentation <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#hyperlinks>`_.


MERN stack eCommerce course. One large single project course - an eCommerce platform.
 1. Shopping Cart 
 2. Checkout system 
 3. Will integrate the PayPal API 
 4. Product review 
 5. Rating system 
 6. Customers can view all their orders
 7. Admin 
 8. Admin can manage users, products, orders, etc.
 9. Basics of React required (Components, State, Props, etc.) - Frontend
 10. Node.js and Express - Backend 
 11. Building a simple REST API 
 12. JSON, web tokens, etc.
 13. Jump in and get your hands dirty!

 Quiz.
* What are React Components?
* What is 'State'?
* What are 'Props'?

Section 1.2: ProShop Project Demo 
---------------------------------

* Built from scratch, then deployed to Heroku 
* Redux Dev Tools to see:
    * Actions that are fired off
    * State, Diff, etc.
* Home Page: 
* Navbar: search projects, cart to shopping cart Page, sign in 
* Registration/Sign in Pages: form 
* Carousel: top-rated products: clicking links to product Page
    * Products Page: latest products (from database) - *pagination*
        * Product Page: image, title, description, overall rating, quantity in stock, reviews 
        * Form to write review (1 per project)
* Add to Cart Page 
* Checkout Page: redirects to Sign-In page if not already logged in (uses local storage)
* Shipping Page:
* Payment Page:
* Placeorder Page:
* Order Page: > button for PayPal API
* Profile Page: > allows you to update Name, Email, Password and view Orders
* Admin Page:
    * Unique admin privileges/Additional options to:
        * Edit or delete users > edit form, buttons, redirects
        * Make users admins
        * Edit or delete products
        * Create products 
        * Edit or delete orders
* Search feature: regex
* Database seeder to seed db with products and users

Section 1.3: Resources & Environment
------------------------------------

.. _a Traversy's GitHub: https://github.com/bradtraversy/proshop_mern
.. _a Basir's YouTube: https://www.youtube.com/channel/UC2xRE4hUCQ3xO3ymEtMh1Hw
.. _a Coding with Basir: https://codingwithbasir.com/
.. _a React Docs: https://reactjs.org/
.. _a Redux Docs: https://redux.js.org/
.. _a MongoDB Docs: https://www.mongodb.com/
.. _a Node.js Docs: https://nodejs.org/en/
.. _a Heroku: https://www.heroku.com/
.. _a Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
.. _a Redux Devtools: https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en
.. _a React Bootstrap: https://react-bootstrap.github.io/
.. _a Bootswatch: https://bootswatch.com/
.. _a JWT.io: https://jwt.io/

VSCode Extensions 
########
ES7 React/Redux/GraphQL/React-native snippets (shortcuts for Component generation) - *rafce*
Bracket Pair Colorizer (organizes syntax colorfully)
Auto Rename Tag (HTML and JSX) - changes beginning and end tags
JavaScript (ES6) code snippets 
Prettier - Code formatter - to remove semi-colons (or keep them if you prefer) same with single quotes

VSCode Settings
########
Prettier:
* JSX Single Quote (checked) 
* Semicolons (unchecked) 
* Single Quote (checked) 
* Tab width (2)

Settings.json shows this information and more 