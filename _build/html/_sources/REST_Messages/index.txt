.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

REST Message v2
##########################

External Cart Orders
********************

There's three pieces I had to use to allow cart orders from an external source

#.  Creating the staging table
#.  Creating the business rule after insertion into the staging table
#.  Setting up the REST Message

Create the Staging Table
========================

    I created a table and named it Cart Order (u_cart_order).  This will hold four
    fields used for calling the Cart API to create an order, more on that later.

            +--------------+------------+-------------+ 
            | Column Label | Type       | Max length  | 
            +==============+============+=============+ 
            | Req_Id       | String     | 100         | 
            +--------------+------------+-------------+ 
            | Catalog Item | String     | 40          | 
            +--------------+------------+-------------+ 
            | Errors       | String     | 500         | 
            +--------------+------------+-------------+ 
            | Variables    | String     | 3000        | 
            +--------------+------------+-------------+ 


Sending the REST Message
========================

From within another ServiceNow Instance

    This can be run however you would want, but I've only tested
    this using a background script.  I don't see why it would
    fail anywhere else.


.. code-block:: javascript

    var request = new sn_ws.RESTMessageV2();
    request.setEndpoint('https://dev22614.service-now.com/api/now/table/u_cart_order');
    request.setHttpMethod('POST');

    //Eg. UserName="admin", Password="admin" for this code sample.
    var user = 'admin';
    var password = 'admin';

    request.setBasicAuth(user,password);
    request.setRequestHeader("Accept","application/json");
    request.setRequestHeader('Content-Type','application/json');
    request.setRequestBody('{"u_catalog_item":"Blackberry",' +
                                '"u_variables":"original^299-999-9991|' +
                                'replacement^Yes"}');
    var response = request.execute();
    gs.log(response.getBody());

In the requestbody there's two key value's to set up

    * u_catalog_item
        Name of the catalog item should be the value
    * u_variables
        The value should be a pipe **|** separated list of variables, with the
        name of the variable the value separted by a caret **^**

Creating the Business Rule
==========================

    When the REST message is sent, it will populate the Cart Order table that we had
    created above.  What we want to do is create a **BEFORE** business rule to be 
    called on **INSERT** so it can go into the
    `Cart API <http://http://wiki.servicenow.com/index.php?title=Service_Catalog_Script_API/>`_ 
    and make an order depending on what was sent in the REST call.




