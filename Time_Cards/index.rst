Time Card Modifications
====================================================

Generate Time Cards based on Resource Allocations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Currently timecards are only generated for the table planned_task and only for the current week

Goal
------

  * Generate timecards when the current user is assigned as a resource allocation
  * Generate timecards for upcoming weeks (not just the current week)

Script Include
---------------

  The only script we need to edit is the **TimeCardAjax** script include.  Since this is OOB, it's best to insert-and-stay
  then mark the original as inactive.

  The only OOB function we will be editing is **ajaxFunction_generateTaskCards()**, the rest we will be creating
  ourselves.

    .. code-block:: javascript

        ajaxFunction_generateTaskCards: function(){
          //get request info
          this.weekStart = this._getWeekStart();
          this.user = this.getParameter('sysparm_user');
          this.weekEnd = this._getWeekEnd();
          this.newCards = []; //list of cards created
          this.existingCards = this._getExistingCards();
          this.plannedTasks = this._getPlannedTasks();
          this._generateMissingCards(this.plannedTasks);
          this._generateMissingCards(this.tasks);

          //added two functions to be run for Resource Allocations
          this.resourceAllocations = this._getResourceAllocations();
          this._generateMissingAllocations();
              
           this._buildResult();
        },

  This is the function that gets run initially, when TimecardAjax is called.  What I added were two lines between **this._generateMissingCards(this.plannedTasks)**
  and **this._buildResult();**.  

  Both functions should be self explanatory.  The **._getResourceAllocation()** grabs all resource allocations for the user
  and **._generateMissingAllocations()** will generate timecards if there are no timecards associated.

Unit Tests
------------

  .. code-block:: javascript

    var alloc = new GlideRecord("resource_allocation");
    alloc.user = "0ac0a7f7db20220003ee793ebf961970";
    var date = new GlideDate();
    date.setValue('2016-11-05');
    alloc.start_date = date;
    var date2 = new GlideDate();
    date2.setValue('2016-11-23');
    alloc.end_date = date2;
    alloc.requested_hours = "30";
    alloc.task = "48b1d30ddb95a20003ee793ebf961942"
    alloc.resource_plan = "e3bc5091db19a20003ee793ebf961943"
    var test = alloc.insert();
    gs.log(test);


  .. code-block:: javascript

  var newTask = new GlideRecord("cert_follow_on_task");
  newTask.assigned_to = "0ac0a7f7db20220003ee793ebf961970";
  newTask.short_description = "Unit Test 08171131";

  var taskId = newTask.insert();
  gs.log("taskID = " + taskId);

  var newRP = new GlideRecord("resource_plan");
    newRP.task = taskId;
    newRP.start_date = "2015-01-01";
    newRP.end_date = "2019-01-01";
    newRP.user_resource = "0ac0a7f7db20220003ee793ebf961970";
    newRP.resource_type = "user";
    newRP.planned_hours = 0;

  var resourceId = newRP.insert();
  gs.log("resourceID = " + resourceId);

  var alloc = new GlideRecord("resource_allocation");
      alloc.user = "0ac0a7f7db20220003ee793ebf961970";
      var date = new GlideDate();
      date.setValue('2016-11-05');
      alloc.start_date = date;
      var date2 = new GlideDate();
      date2.setValue('2016-11-23');
      alloc.end_date = date2;
      alloc.requested_hours = "30";
      alloc.task = taskId;
      alloc.resource_plan = resourceId;

  var allocationId = alloc.insert();
  gs.log("allocationdId = " + allocationId);

  var alloc2 = new GlideRecord("resource_allocation");
      alloc2.user = "0ac0a7f7db20220003ee793ebf961970";
      var date = new GlideDate();
      date.setValue('2016-11-16');
      alloc2.start_date = date;
      var date2 = new GlideDate();
      date2.setValue('2016-12-02');
      alloc2.end_date = date2;
      alloc2.requested_hours = "30";
      alloc2.task = taskId;
      alloc2.resource_plan = resourceId;

  allocationId = alloc2.insert();
  gs.log("allocationID2 = " + allocationId);

