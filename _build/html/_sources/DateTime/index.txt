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


Comparing Due Date with Start Date
*************************************

On Change Client Script for Due Date

.. code-block:: javascript

    function onChange(control, oldValue, newValue, isLoading, isTemplate) {
       if (isLoading || g_form.getValue("expected_start") == "") {
          return;
       }
      
      var start_date = g_form.getValue("expected_start");
      
      //Calls serverside script to check if start date is earlier than due date
      var ajax = new GlideAjax('TransferOrderDateTimeAjax');  
      ajax.addParam('sysparm_name','compareDatesAjax');  
      ajax.addParam('sysparm_startDate', start_date);  
      ajax.addParam('sysparm_endDate', newValue);  
      ajax.getXML(warnIfFalse);

      //Callback will display error if start date is earlier than due date
      function warnIfFalse(response){  
        var answer = response.responseXML.documentElement.getAttribute("answer");
        if (answer == "false") {
          g_form.setValue("due_date", "");
          g_form.showErrorBox("due_date", "Due Date must be after Start Date");
        }
      }
    }

Comparing Dates when days doesn't matter (untested)
******************************************************

  Uses a milisecond timestamp, works for either Date or Date/Time

..code-block:: javascript

    newDate(g_form.getValue("expected_start")).getTime() > newDate(g_form.getValue("due_date")).getTime()