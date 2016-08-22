
Slack Questions
====================================================

State choices from incident table API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**taygun [8:30 AM]**

Hello again! I want to build an Incident integration for service now. Is there a way I can retrive (API) all the state choices for Incident table?

**artemis [8:38 AM]**

@taygun: I tried table api and it worked...  
use this : /api/now/table/sys_choice?sysparm_query=name=incident^element=state^inactive=0&sysparm_fields=value,label


jvar_cart
~~~~~~~~~~

**englep10 [9:21 AM]** 
Good morning everyone! I had a quick question when it came to jelly. I see the syntax calling what I am assuming are script includes but I presently can *not* find them. The lines in question are:
  
.. code-block:: html

	<g:include_script src="CartCheckoutFunctionsV2.jsdbx" />
	<j:set var="jvar_skip_attachment_footer" value="true" />
	<j:set var="jvar_req_for" value="${jvar_cart.getRequestedFor()}" />

If someone could point me to the location of those functions *getRequestedFor()* that would be *most* appreciated

**pheedbaq [10:35 AM]** 
englep10 nabil jvar_cart is a reference to a **Java** object. getRequestedFor is a java method, exposed to javascript, on the GlideappCart object. Looks lke the specific method `getRequestedFor` looks at the sc_cart record that the GlideappCart is used with, and returns the sys_id of the user in the “requested_for” field on that sc_cart record.