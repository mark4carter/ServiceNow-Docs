.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Emails
##############################

Parsing out Hidden Watermarks
================================


Business Rule on sys_email table
*********************************

.. code-block:: javascript

    (function executeRule(current, previous /*null when async*/) {

		current.subject = String(current.subject).replace(/Re:+/i, "");	
		current.headers = String(current.headers).replace(/In-Reply-To:<[^>]*>/ig, "");	
	
	})(current, previous);


Summary
*********************************

We had a client where an email would continually be marked as a reply with a watermark, 
even after the watermark had been removed.  We found in this case, we needed to remove the
"RE" in the subject and the "In-Reply-To" in the email header