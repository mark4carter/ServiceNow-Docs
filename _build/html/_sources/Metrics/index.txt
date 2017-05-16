.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Metrics
##########################

Metric from Assignment Group to Close
************************************************

This will require two metric definitions.  One will track the assignment group field and
the other will track the state field.  When the assignment group is filled the metric begins
and when the state turns to close, the metric will find the assignment group metric and end the duration.


.. admonition:: Metric Definition
  :class: myOwnStyle

    | Name : **Assignment Group has been populated**
    | Type : **Script calculation**


.. code-block:: javascript

    if (!current.assignment_group.nil()) {
    createMetric();
      }

      function createMetric() {
          var mi = new MetricInstance(definition, current);
          if (mi.metricExists())
              return;
          
          var gr = mi.getNewRecord();
          gr.field_value = current.assignment_group;
        gr.start = current.sys_updated_on;
          gr.calculation_complete = false;
          gr.insert();
      }



.. admonition:: Metric Definition
  :class: myOwnStyle

    | Name : **Stop Assignment duration on close**
    | Type : **Script calculation**


.. code-block:: javascript

    // Close Durations on Closed Complete, Closed Incomplete, or Cancelled
  if (current.state == 3 ||  current.state == 4 || current.state == 7) { 
      closeDurations(current);
  }

  function closeDurations(current) {
      var gr = new GlideRecord('metric_instance');
      gr.addQuery('id', current.sys_id);
      gr.addQuery('calculation_complete', false);
      gr.addQuery('definition.name', 'Time to closure');
      gr.query();
      while (gr.next()) {
         var definition = new GlideRecord('metric_definition');
         definition.get(gr.definition);
         var mi = new MetricInstance(definition, current);
         mi.endDuration();
      }
  }

.. warning:: 
  
  Both Metrics need to be placed as "Script calculation" or it will not process correctly