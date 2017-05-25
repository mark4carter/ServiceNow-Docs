.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

RegEx
##############################

Replace with callback
================================

Regex can be used for replacing a string, but if you want to use the string still or store it,
you can use a callback function

The code below will find a string, store it in a table, and replace it with the sys_id of the record



.. code-block:: javascript

    var body = textWithURLs;
	var newBody = "";

	var trackGR = new GlideRecord("url_table");

	//Here we see the "url" variable will hold each matched string
	// {string}  The return string of each replace will replace the matched string
	var newBody = body.replace(/href\s*=\s*["'][^'"]*["']/ig, function createTracking(url) {

	  trackGR = new GlideRecord("url_table");
	  trackGR.initialize();
	  trackGR.u_email_message = current.sys_id.toString();
	  var formattedUrl = url.toString().split(/["']/)[1];
	  trackGR.u_url_link = formattedUrl;
	  var trackID = trackGR.insert();

	  return "href='https://devXXXXX.service-now.com/nav_to.do?uri=url_table.do?sys_id=" + trackID + "'";
	});

	textWithURLs = newBody;
