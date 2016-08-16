
Reference Qualifiers
====================================================

Creating a Dynamic Qualifier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

I decided to create a catalog item to request a parking space.  One feature
I wanted was to only show parking spots depending on which type of spot
you want to reserve (ie. VIP, Motorcycle, Normal).

To accomplish that requirement, I decided to go with a dynamic qualifier that
changes depending on type selected.

The Script Include
---------------------

This is probably up for debate, but I decided to keep the same object format for
my script include using Class.create() and .prototype.

.. admonition:: Script Include Fields
	:class: myOwnStyle

		| Name : **parkingByParkingType**
		| Client callable : **True**

.. code-block:: javascript

	var parkingByParkingType = Class.create();
	parkingByParkingType.prototype = {
	    initialize: function() {
	    },
		
		getSpots: function() {
			
			var result = [];
			
			var res = new GlideRecord("u_parking_spot");
				res.addQuery("u_assigned", false);
				res.addQuery("u_type", current.variables.parking_type);
				res.query();
			
			while ( res.next() ) {
				result.push(res.sys_id.toString());
			}
			
			var au = new ArrayUtil();
			
			return au.unique(result);
		},

	    type: 'parkingByParkingType'
	};


The function of interest is the .getSpots() function.  It's a basic query in the
u_parking_spot table, but with a Dynamic Query we have acccess to *current* which
we can use to add to query.  In this example we're using the parking_type variable,
which is a selection.


The Dyanmic Filter Option
----------------------------


Ref: https://www.packtpub.com/mapt/book/Networking%20and%20Servers/9781782174219/02/ch02lvl1sec26/Scripting%20Reference%20Qualifiers