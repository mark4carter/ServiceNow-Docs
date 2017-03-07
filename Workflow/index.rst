.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Workflows
##########################


Canceling and Reopening Workflow
*********************************


.. code-block:: javascript

    function server_cancel_business_case(){
        //Cancels all approvals for Business Case and delete workflow
        new WorkflowApprovalUtils().cancelAll(current, "Placed on hold by " + gs.getUser().name);
        new Workflow().deleteWorkflow(current);
        
        current.u_ppm_bc_state = 'closed_cancelled';
        current.update();
        action.setRedirectURL(current);
    }


.. code-block:: javascript
    
    //Cancels all approvals for Business Case and delete workflow
    new WorkflowApprovalUtils().cancelAll(current, "Re-Opened by " + gs.getUser());
    new Workflow().deleteWorkflow(current);