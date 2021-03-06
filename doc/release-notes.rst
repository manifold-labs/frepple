Release notes
-------------

4.4.1 (Upcoming release)
========================

4.4.0 (2018/08/02)
==================

.. rubric:: Production planning
  
- Resources can now have an `efficiency percentage <user-guide/model-reference/resources.html>`_. This allows
  the resource to perform an operation faster or slower than the standard operation time.

- The `resource report <user-guide/user-interface/plan-analysis/resource-report.html>`_ now displays the 
  available capacity as a line, replacing the green bar in previous releases to show the free capacity.

- | Performance optimization of the solver algorithm. The solver now passes down the minimum shipment 
    information from the demand to all upstream entities, which allows the algorithm to perform a more
    efficient search.
  | In complex models, the resulting plan may be slightly different - for the better.

- Resource build-ahead penalty calculation now also working for 0-cost resources.

- New rows to the `purchase order summary <user-guide/user-interface/plan-analysis/purchase-order-summary.html>`_ 
  and `distribution order summary <user-guide/user-interface/plan-analysis/distribution-order-summary.html>`_
  reports to show the quantity on order or in transit.

- New rows to the `inventory report <user-guide/user-interface/plan-analysis/inventory-report.html>`_
  to show 1) days of cover of the starting inventory, 2) the safety stock and 3) more details
  on the supply and consumption type.

- | The minimum field on the buffer defines a safety stock. In previous releases this safety stock was
    effective from the horizon start in 1971. Now this safety stock is effective from the current
    date of the plan onwards.
  | This change will give a different result for safety stock replenishments in an unconstrained plan.
    In a lead time constrained plan the results will be identical.  

- Remove buffers of type procurement from the planning engine code. This buffer type was already long
  deprecated and hasn't been accessible to users for quite some time now. 
  
- Simpler and more generic modeling of fixed material consumption and production by operations. 
  The types 'fixed_end' and 'fixed_start' on `operation material <user-guide/model-reference/operation-materials.html>`_
  records are replaced with a field 'fixed_quantity'.

- Renamed the "demand plan detail" report to `delivery orders <user-guide/model-reference/operation-materials.html>`_,
  and enable uploading confirmed or approved shipments to customers as input data.

- | When expanding a confirmed manufacturing order on a routing operation, the automatic creation of the
    child manufacturing orders for each routing step now also considers the post-operation time.
  | Note that such child manufacturing orders are only generated if they aren't provided in the input 
    data yet.   

.. rubric:: User interface

- Bug fix when copying a what-if scenario into another what-if scenario. 

- Bug fix when uploading data files using the Microsoft Edge browser.

.. rubric:: Deprecation

- | Operations of types alternate, routing and split should not load any resources, 
    or consume or produce materials. The suboperations should model all material and capacity 
    usage instead.
  | Note that in the majority of models, the explicit modeling of alternate operations is no
    longer needed. The planning engine detects situations where an item-location can be replenished
    in multiple ways and automatically generates an alternate operation.

4.3.4 (2018/06/08)
==================

.. rubric:: Production planning

- Added new reports `purchase order summary <user-guide/user-interface/plan-analysis/purchase-order-summary.html>`_ 
  and `distribution order summary <user-guide/user-interface/plan-analysis/distribution-order-summary.html>`_
  to summarize the purchase orders or distribution orders per time bucket.

- For consistency with the previous change, the operation report is renamed 
  to `manufacturing order summary <user-guide/user-interface/plan-analysis/manufacturing-order-summary.html>`_.

.. rubric:: Integration

- Extended the `exporttofolder <user-guide/command-reference.html#exporttofolder>`_ 
  command to export additional plan results into CSV or Excel files.

- The data type of all numeric fields is changed from 15 digits with 6 decimals
  to 20 digits with 8 decimals. This allows a larger range of numbers to be
  accurately represented in the database.
  
- The `remote web commands API <integration-guide/remote-commands.html>`_ now 
  supports user authentication with `JSON Web Tokens <https://jwt.io/>`_ to launch tasks,
  download data and upload data. 


4.3.3 (2018/05/03)
==================

.. rubric:: Production planning

- Solver performance optimization where there are availability calendars.
  The plan generation time can be reduced with a factor 3 to 4 in some models.
- Solver enhancements for planning with setup matrices.
- Solver optimization to handle infinite buffers more efficiently.
- Bug fix: Compilation error with Python 3.6

.. rubric:: User interface

- Bug fix for spreadsheet import: more robust handling of empty rows and rows with
  empty fields at the end 
  
.. rubric:: Odoo connector

- Correction to maintain a single root hierarchy.


4.3.2 (2018/03/19)
==================

.. rubric:: Production planning

- | New operationmaterial policy 'transfer_batch' which allows material production
    or consumption in a number of batches of fixed size at various moments during
    the total duration of the operationplan.
  | A new field operationmaterial.transferbatch is introduced.
- A new field 'end items' is added to the manufacturing order, purchase order and
  distribution orders screens. It is similar to the 'demands' which shows the 
  demands 

.. rubric:: API

- Bug fix: backward compatibility after command renaming in 4.3.1

.. rubric:: Third party components

- Upgrade to PostgreSQL 10. 
  PostgreSQL 9.5 and 9.6 remain fully supported.

4.3.1 (2018/02/17)
==================

.. rubric:: Bug fixes

- The autofence now also considers approved supply, and not only confirmed supply.
- Excel files with some non-standard internal structure are now also recognized.
- Work-in-progress operationplans with quantity 0 are no longer rejected.

.. rubric:: Deprecations

- Command frepple_run is renamed to runplan.
- Command frepple_runserver is renamed to runwebserver.
- Command frepple_copy is renamed to scenario_copy.
- Command frepple_importfromfolder is renamed to importfromfolder.
- Command frepple_exporttofolder is renamed to exportfromfolder.
- Command frepple_flush is renamed to empty.
- Command frepple_backup is renamed to backup.
- Command frepple_restore is renamed to restore.
- Command frepple_simulation is renamed to simulation.
- Command frepple_createbuckets is renamed to createbuckets.
- Command frepple_createmodel is renamed to createmodel.
- Command frepple_loadxml is renamed to loadxml.
- Command frepple_runworker is renamed to runworker.
