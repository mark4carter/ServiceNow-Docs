
Slack Questions
====================================================

State choices from incident table API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**taygun [8:30 AM]**

Hello again! I want to build an Incident integration for service now. Is there a way I can retrive (API) all the state choices for Incident table?

**artemis [8:38 AM]**

@taygun: I tried table api and it worked...  
use this : /api/now/table/sys_choice?sysparm_query=name=incident^element=state^inactive=0&sysparm_fields=value,label