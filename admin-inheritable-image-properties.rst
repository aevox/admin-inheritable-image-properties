..
 Thised to reflect this new feature.

 work is licensed under a Creative Commons Attribution 3.0 Unported
 License.

 http://creativecommons.org/licenses/by/3.0/legalcode

==========================================
inheritable admin image properties
==========================================

https://blueprints.launchpad.net/nova/+spec/inheritable-admin-image-properties

Make some image properties inheritable even though the user does not have the
credentials to create them.

Problem description
===================

When snapshotting or shelving an instance nova creates a new image in glance
using the user credentials. If the user does not have the rights to create a
custom property he is not able to make any of those operations.

Use Cases
----------

A cloud-administrator wants to store license-cost properties on a per-image
basis (like how much to charge per hour per cpu). This property can already be
protected by role, but a cloud owner will want this property to be
automatically inherited to child images.

Project Priority
-----------------

None

Proposed change
===============

We propose to create a new option in the nova conf file containing a list of
properties that should be inherited.
Upon instance snapshotting or shelving those properties will be set after
creation of the image by nova using its credentials.

Alternatives
------------

None

Data model impact
-----------------

None

REST API impact
---------------

None

Security impact
---------------

This change require elevated privilege.

Notifications impact
--------------------

None

Other end user impact
---------------------

None

Performance Impact
------------------

With the option enabled there should be a performance impact as the request
will get a new token for authentication.

Other deployer impact
---------------------

None

Developer impact
----------------

None

Implementation
==============

Assignee(s)
-----------

Primary assignee:
  Marc Fouché

Other contributors:


Work Items
----------

  * Change the behavior in compute.api
  * Create function in image.api
  * Create function in image.glance

Dependencies
============

None

Testing
=======

Unit Tests

Documentation Impact
====================

This new feature should be added to the documentation.

References
==========

None

History
=======

None
