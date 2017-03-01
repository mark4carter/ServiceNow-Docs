Hiding non-readable Rows in List View
######################################

.. admonition:: Row Level Security and On Query Business Rules
  :class: myOwnStyle

      |

Separating Readable Projects By Department
**************************************************

If you ever try placing security by record (or by row), your users may start seeing lists views with a count of Rows removed by Securiy contraints.
Even worse they may think there are no more records, when records can easily be on the first and last page with any number of removed rows in between.

.. image:: img/Constraints.JPG
      :width: 100%

Creating a Before Query Business Rule
=================================================

The query created in the Business Rule can be thought of as a filter.  So let's say one requirement is to allow anyone from the InfoSec Department to see any
Contract record.  We would start the Business Rule, by wrapping the filter with an if statement.

  .. code-block:: javascript

    if (gs.hasRole('admin') || userIsInInfoSec()) {
      // Add filter query here
    }

    function userIsInInfoSec() {
      //Normal Glide Record query to see if user's Dept is InfoSec
    }

Next, we need to apply the query.  Let's say there's a department field on each contract and if a user is in the same department as the one listed in contracts then they
should be able to view it.

  .. code-block:: javascript

    if (gs.hasRole('admin') || userIsInInfoSec()) {
      var uID = gs.getUserID();
      var uGR = new GlideRecord("sys_user");
      uGR.get(uID);

      current.addQuery('department', uGR.department);
    }

What the query is doing here is returning only records that match department with the current user's department.  These will be the only records that will show in list view and will
remove the security constraints, as long as they have security rights.  Below, we are going to add another query where all contracts in the "Guest" department can be viewed as well.

  .. code-block:: javascript

    if (gs.hasRole('admin') || userIsInInfoSec()) {
      var uID = gs.getUserID();
      var uGR = new GlideRecord("sys_user");
      uGR.get(uID);

      var q = current.addQuery('department', uGR.department);
      q.addOrCondition('department', 'Guest');
    }

