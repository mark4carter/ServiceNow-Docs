Contract Management
====================================================

Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contract management is the management of contracts made with customers, partners, etc.  In ServiceNow, contract
management can be used to create or maintain contracts.  Contracts can be leases, warranties, maintenance, and
service.

Roles
:::::::

The **contract-manager** role is needed for contract creating/editing.

Contract Compliance Checks
~~~~~~~~~~~~~~~~~~~~~~~~~~

This scheduled job runs on the **Contract [ast_contract]** table automatically each night.

* Changes the contract state to **Active** if the contract is approved and reaches the specified start date.
* Renews the contract if the contract is approved for renewal and reaches teh specified start date.
* Changes the contract state to **Expired** if the contract state is **Active** and reaches the end date.

Contract Life Cycle
~~~~~~~~~~~~~~~~~~~~

    +-----------+-----------------------------------------------------------------------------------------+
    | State     | Description                                                                             |
    +===========+=========================================================================================+
    | Draft     | User adds information about the contract and specifies approver                         |
    +-----------+-----------------------------------------------------------------------------------------+
    | Active    | Contract was approved and has reached the specified **Start date**.                     |
    +-----------+-----------------------------------------------------------------------------------------+
    | Expired   || Contract reached the specified **End date**. Expired contracts with an active renewal  |
    |           || workflow that are waiting for approval has a substate of **Awaiting Review**.          |
    |           || Expired contracts with an active renewal workflow where the renewal was                |
    |           || approved, but the renewal date has not yet passed, have a substate of                  |
    |           || **Renewal Approved**.  Expired contracts with no active renewal or extension           |
    |           || pending workflow have an empty substate.                                               |
    |           ||                                                                                        |
    +-----------+-----------------------------------------------------------------------------------------+
    | Canceled  | Contract was discontinued and is no longer active                                       |
    +-----------+-----------------------------------------------------------------------------------------+

Contract Substates
::::::::::::::::::::

    +---------------------+-------------------------------------------------------------------------------+
    | Substate            | Description                                                                   |
    +=====================+===============================================================================+
    | Awaiting Review     | Contract is being prepared for review                                         |
    +---------------------+-------------------------------------------------------------------------------+
    | Under Review        | Contract is sent to the approver and the approver is reviewing the contract.  |
    +---------------------+-------------------------------------------------------------------------------+
    | Approved            | Contract is reviewed and accepted by the approver.                            |
    +---------------------+-------------------------------------------------------------------------------+
    | Rejected            | Contract is reviewed and declined by the approver.                            |
    +---------------------+-------------------------------------------------------------------------------+
    | Renewal Approved    | Contract renewal is approved by the approver.                                 |
    +---------------------+-------------------------------------------------------------------------------+
    | Renewal Rejected    | Contract renewal is rejected by the approver.                                 |
    +---------------------+-------------------------------------------------------------------------------+
    | Extension Approved  | Contract extension is approved by the approver.                               |
    +---------------------+-------------------------------------------------------------------------------+
    | Extension Rejected  | Contract extension is rejected by the approver.                               |
    +---------------------+-------------------------------------------------------------------------------+
    | None                | No substate is specified                                                      |
    +---------------------+-------------------------------------------------------------------------------+

Creating Contracts
~~~~~~~~~~~~~~~~~~~~

Obtaining Contract Approval
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once in **Draft** state a contract can be sent for approval to only one approver.  The approver name cannot be changed.

Contract Management Tutorial
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Overview Module
:::::::::::::::::

OOB shows Active Contracts by Vendor and shows
many differen drill downs

Most selections are self-explanatory

Data shown on contract record
::::::::::::::::::::::::::::::::::

Quick Buttons include: Update, Adjust, Cancel Contract, Extend, Renew

Most all fields are locked down and must be changed through the buttons
and they cannot be changed without approval.

Contract Rate Cards
:::::::::::::::::::::

Every night the scheduler will run to check and will automtically produce
an expense line

Create New Contract Type
:::::::::::::::::::::::::

Go to Product Models -> Contract Models -> New