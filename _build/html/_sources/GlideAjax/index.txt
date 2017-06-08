.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

GlideAjax
##########################


Returning multiple values
*********************************

You can return more than one value easiest if you return it as a JSON string.

.. code-block:: Javascript
    
	var GetUserRecord = Class.create();
	GetUserRecord.prototype = Object.extendsObject(AbstractAjaxProcessor, {
		
		getForCorrectiveItem: function () {
			var userID = this.getParameter("sysparm_user_id");
			
			var userGR = new GlideRecord("sys_user");
			userGR.addQuery("sys_id", userID);
			userGR.query();
			
			var userProps = {};
			
			if (userGR.next()) {
				userProps.name = userGR.name.toString();
				userProps.manager = userGR.manager.toString();
				userProps.department = userGR.department.toString();
				userProps.location = userGR.location.getDisplayValue();
			}
			
			var json = new JSON();
			var data = json.encode(userProps);
			
			return data;
		},

	    type: 'GetUserRecord'
	});