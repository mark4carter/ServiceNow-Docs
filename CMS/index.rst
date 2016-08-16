.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Content Management System
#########################


Continue Shopping Redirection
*****************************

After a rebranding effort, everything seemed to work fine except a continue shopping button.
The error didn't creep up until later in the month.  This value is not found in a UI Macro
as first expected.  The value is actually a field in a record under Service Catalog -> Maintain Catalogs.

In this particular task, I had to inside one more step deeper into the Service Catalog record and choose
the specific site.

.. image:: img/sc_list.jpg
      :width: 100%

Then within I changed the fields CMS 'Continue Shopping' page

.. image:: img/shop_field.jpg
      :width: 75%

Ref: https://community.servicenow.com/community/service-management/service-catalog/blog/2015/05/01/how-to-get-continue-shopping-buttons-to-work-in-your-service-catalog