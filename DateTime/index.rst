.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Date Time Servicenow
##########################

Update Review Date
********************


.. code-block:: javascript

    (function executeRule(current, previous /*null when async*/) {

        var gdt = new GlideDateTime(current.ends);
        gdt.addDays(90);
        current.u_review_date_custom = gdt;

    })(current, previous);


.. warning:: 
    
    .addDays() will addDays to the time, but does not return a glideDateTime

    current.ends is a Date (not DateTime) field
