|Tag| |License| |Build| |Coverage| |Quality|

.. raw:: html

  <div align="center">
   <h2><code>storehouse has been deprecated⚠️</code></h2>
  </div>

MongoDB has been chosen as a default document-oriented database, so if your NApp needs this type of storage check out `this documentation <https://kytos-ng.github.io/napps/mongodb.html>`_. If you're looking for additional code samples you can also check out `flow_manager <https://github.com/kytos-ng/flow_manager>`_, `topology <https://github.com/kytos-ng/topology>`_ and `mef_eline <https://github.com/kytos-ng/mef_eline>`_.

.. raw:: html

  <div align="center">
    <h1><code>kytos/storehouse</code></h1>

    <strong>NApp that provides backends for persistent data storage</strong>

    <h3><a href="https://kytos-ng.github.io/api/storehouse.html">OpenAPI Docs</a></h3>
  </div>

Overview
========
This NApp is responsible for data persistence, saving and retrieving
information. It can be acessed by external agents through the REST API or by
other NApps, using the event-based methods.

Each box of data can be saved in a different namespace, with support for nested
namespaces.

The NApp is designed to support many options of back-end persistence solutions.
Currently it features filesystem operations, but alternatives such as SQL or
NoSQL databases will be implemented.

Installing
==========

To install this NApp, first, make sure to have the same venv activated as you have ``kytos`` installed on:

.. code:: shell

   $ git clone https://github.com/kytos-ng/storehouse.git
   $ cd storehouse
   $ python setup.py develop

Events
======

Subscribed
----------

The NApp listens to events requesting operations. Every event must have a
callback function to be executed right after the internal method returns. The
signature of the callback function is described with each event.

kytos.storehouse.create
~~~~~~~~~~~~~~~~~~~~~~~

Event requesting to save data to a box in a namespace.

Content:

.. code-block:: python3

   {
       data: <any data to be saved>,
       namespace: <namespace name>,
       callback: <callback function> # To be executed after the method returns.
   }

Callback function:

.. code-block:: python3

   def callback_function_name(box, error=False):
       # box: copy of the Box instance stored with data and metadata.
       # error: False when the operation is successful, True otherwise.

kytos.storehouse.retrieve
~~~~~~~~~~~~~~~~~~~~~~~~~

Event requesting to load data from a box in a namespace.

Content:

.. code-block:: python3

   {
       box_id: <ID of the Box to retrieve data from>,
       namespace: <namespace name>,
       callback: <callback function> # To be executed after the method returns.
   }

Callback function:

.. code-block:: python3

   def callback_function_name(box, error=False):
       # box: the retrieved Box instance.
       # error: False when the operation is successful, True otherwise.

kytos.storehouse.update
~~~~~~~~~~~~~~~~~~~~~~~

Event requesting to update data to a box in a namespace.

Content:

.. code-block:: python3

   {
       box_id: <ID of the Box to retrieve data from>,
       data: <any data to be saved>,
       namespace: <namespace name>,
       callback: <callback function> # To be executed after the method returns.
   }

Callback function:

.. code-block:: python3

   def callback_function_name(event, box, error=False):
       # event: copy of the original event data
       # box: copy of the Box instance stored with data and metadata.
       # error: False when the operation is successful, True otherwise.
       
kytos.storehouse.list
~~~~~~~~~~~~~~~~~~~~~

Event requesting to list all boxes in a namespace.

Content:

.. code-block:: python3

   {
       namespace: <namespace name>,
       callback: <callback function> # To be executed after the method returns.
   }

Callback function:

.. code-block:: python3

   def callback_function_name(box_list, error=False):
       # box_list: the retrieved list of Box.box_id.
       # error: False when the operation is successful, True otherwise.

kytos.storehouse.delete
~~~~~~~~~~~~~~~~~~~~~~~

Event requesting to remove a box from a namespace.

Content:

.. code-block:: python3

   {
       box_id: <ID of the Box to be deleted>,
       namespace: <namespace name>,
       callback: <callback function> # To be executed after the method returns.
   }

Callback function:

.. code-block:: python3

   def callback_function_name(result, error=False):
       # result: True if the box was deleted, False otherwise .
       # error: False when the operation is successful, True otherwise.


.. |License| image:: https://img.shields.io/github/license/kytos-ng/kytos.svg
   :target: https://github.com/kytos-ng/storehouse/blob/master/LICENSE
.. |Build| image:: https://scrutinizer-ci.com/g/kytos-ng/storehouse/badges/build.png?b=master
  :alt: Build status
  :target: https://scrutinizer-ci.com/g/kytos-ng/storehouse/?branch=master
.. |Coverage| image:: https://scrutinizer-ci.com/g/kytos-ng/storehouse/badges/coverage.png?b=master
  :alt: Code coverage
  :target: https://scrutinizer-ci.com/g/kytos-ng/storehouse/?branch=master
.. |Quality| image:: https://scrutinizer-ci.com/g/kytos-ng/storehouse/badges/quality-score.png?b=master
  :alt: Code-quality score
  :target: https://scrutinizer-ci.com/g/kytos-ng/storehouse/?branch=master
.. |Tag| image:: https://img.shields.io/github/tag/kytos-ng/storehouse.svg
   :target: https://github.com/kytos-ng/storehouse/tags
