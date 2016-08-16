.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Working With Variable Sets
##########################


Variable Iteration
******************

Thanks to Andrew Sainz for finding this

.. code-block:: javascript

    var item = new GlideRecord('sc_req_item');
    item.addQuery('sys_id',current.sysapproval);
    item.query();
             
    if(item.next())     {
        for (var key in item.variables)      {          
            var v = item.variables[key];
           
            if (v != '' && !v.nil()) {
                current.u_approval_summary +=v.getGlideObject().getQuestion().getLabel() +
                		': ' + v.getDisplayValue() + "\n";  
            }
        }
    }

