.. ServiceNow Documentation documentation master file, created by
   sphinx-quickstart on Tue Aug  2 08:42:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Copying Data
##########################


Worknotes
*********************************

Copying the full set of work notes to another area

.. code-block:: javascript
    
    //Gets all worknotes associated with current
    var notes = current.work_notes.getJournalEntry(-1);

    var newNotes = "Copied notes ::\n" + notes;

Currency Fields
*********************************

Copying old funds in current to new funds in another field

.. code-block:: javascript
    
    bCase.new_funds = bCase.new_funds.getReferenceCurrencyCode() + ';' + current.old_funds.getReferenceValue();