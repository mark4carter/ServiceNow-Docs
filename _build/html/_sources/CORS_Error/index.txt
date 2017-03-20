.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

CORS Error
##########################


How to get around CORS Exception
*********************************

.. code-block:: PowerShell
    
    chrome.exe --user-data-dir="C:/Chrome dev session" --disable-web-security

Depending on location of Chrome, file can be run with single line below

.. code-block:: PowerShell

	"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --user-data-dir="C:/Chrome dev session" --disable-web-security

.. warning:: 

	Goes without saying !! be careful of security