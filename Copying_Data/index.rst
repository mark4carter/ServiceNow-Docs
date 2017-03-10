.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Copying Data
##########################


Worknotes
*********************************

.. code-block:: javascript
    
    var notes = current.work_notes.getJournalEntry(-1);
    bCase.work_notes = "Idea Task Work Notes ::\n" + notes;

Currency Fields
*********************************

.. code-block:: javascript
    
    bCase.u_ppm_funds_other_amt = bCase.u_ppm_funds_other_amt.getReferenceCurrencyCode() + ';' + current.u_ppm_funds_other_amt.getReferenceValue();