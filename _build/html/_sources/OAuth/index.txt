.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

OAuth
##########################


Manual Oauth
*********************************

Oauth profile needs to be first set up on ServiceNow.  After set up,
code below can run Oauth for each REST call.  This is taken form a SalesForce
Integration.

.. code-block:: Javascript
    
    var oAuthClient = new sn_auth.GlideOAuthClient();
	var params = {grant_type:"password", username: username, password: password};
	var json = new global.JSON();
	var text = json.encode(params);
	var tokenResponse = oAuthClient.requestToken("nameless-dev-ed.my.salesforce.com", text);
	var token = tokenResponse.getToken();

	gs.info("AccessToken:" + token.getAccessToken());
	gs.info("AccessTokenExpiresIn:" + token.getExpiresIn());
	gs.info(" RefreshToken:" + token.getRefreshToken());

	var response, responseBody, status;

	try {

	var restMessage = new sn_ws.RESTMessageV2();
	restMessage.setHttpMethod("get");
	restMessage.setEndpoint("https://nameless-dev-ed.my.salesforce.com/services/data/v39.0/query/?q=SELECT+FirstName,+LastName,+Company,+MobilePhone+from+Lead")
	restMessage.setRequestHeader("Authorization", "Bearer " + token.getAccessToken());

	response = restMessage.execute();
	responseBody = response.haveError() ? response.getErrorMessage() : response.getBody();
	status = response.getStatusCode();

	} catch(ex) {
		responseBody = ex;
		status = '500';
	} finally {
		requestBody = restMessage ? restMessage.getRequestBody():null;
	}

	gs.info("Request Body: " + requestBody);
	gs.info("Response: " + responseBody);
	gs.info("HTTP Status: " + status);