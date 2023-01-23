Usage
=====

.. _installation:

Installation
------------

To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']


.. backup
.. Welcome to ProShopApp's documentation!
.. ===================================

.. **ProShopApp** is a *MERN* tutorial project. I followed this 
.. Udemy course created by Brad Traversy to learn 
.. more about React and other technologies.
.. The main website can be found  `here. <https://proshopapp2023.herokuapp.com/>`_

.. Check out the :doc:`usage` section for further information, including
.. how to :ref:`installation` the project.

.. .. note::

..    This project is under active development.

.. Contents
.. --------

.. .. toctree::

..    introduction
..    usage
..    api

.. ProShopApp has its documentation hosted on Read the Docs.
