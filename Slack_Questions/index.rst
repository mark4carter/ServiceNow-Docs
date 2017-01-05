
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


object in an object
~~~~~~~~~~~~~~~~~~~~


**professor [1:39 PM]**  
oh this one is a bitch

[1:39]  
one sec, I think I wrote a thing to solve this

[1:43]  
blah, here it is

[1:43]

.. code-block:: javascript

  function addObjToObj(parent, child, name) {
    if (!parent) {
        parent = {};
    }
    parent[name] = child;
    return parent;

[1:43]  
one sec, let me jsdoc that and store it in my scripts folder

**nabil [1:46 PM]** 
so what if `parent` and `child` were meant to be the same object?

[1:46]  
im not looking to return a new object

[1:46]  
im looking to modify the existing one in place

**professor [1:47 PM]**
so you want an object to contain... itself?

[1:47]  
an immutable form of itself so that the child changes as the parent changes?

**nabil [1:47 PM]**  
i want to wrap new properties and have the original turn intoa c hild node of it

[1:47]  
basically im building a hierarchecal object

[1:48]  
could be n # of nodes up, n # of nodes down

**professor [1:48 PM]** 
right, so you'd call the function like this: 
`addObjToObj(originalObject, originalObject, "orig");` (edited)

[1:48]  
so you'd say `originalObject = addObjToObj(originalObject, originalObject, "orig");`