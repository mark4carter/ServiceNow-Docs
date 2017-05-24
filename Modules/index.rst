.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Modules
##########################

Open new window from module
************************************************

This will require two metric definitions.  One will track the assignment group field and
the other will track the state field.  When the assignment group is filled the metric begins
and when the state turns to close, the metric will find the assignment group metric and end the duration.


.. admonition:: Module
  :class: myOwnStyle

    | Link Type : URL (from Arguments:)


In the arguments field use the following:
    .. code-block:: javascript
  
      javascript:top.window.open('/sys_user_list.do', '_blank', 'height=700,width=1000');