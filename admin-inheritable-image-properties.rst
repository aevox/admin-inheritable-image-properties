..
 This work is licensed under a Creative Commons Attribution 3.0 Unported
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

An image in glance can have custom properties that have CRUD rules.
When snapshotting or shelving an instance nova creates a new image in glance
using the user credentials. If the user does not have the rights to create one
of the custom property he is not able to create an image, thus he is not able
to snapshot or shelve the instance.

Use Cases
----------

A cloud-administrator wants to store license-cost properties on a per-image
basis (like how much to charge per hour per cpu). This property can be
protected by role, but a cloud owner will want this property to be
automatically inherited to child images.

Another use case would be an administrator who wants to make operations on
instances depending on image propertiess. For example taging Windows instances
so they are run on a Windows hypervisor. The administrator wants this tag to be
inherited automatically, but he does not want the user to be able to change
this property.

Project Priority
-----------------

None

Proposed change
===============

We propose to create the option "inheritable_admin_image_properties" containing
a list of custom properties.
After creation of the image from snapshotting or shelving the instance, those
properties will be set by nova using its admin credentials.

Alternatives
------------

An alternative would be to create this functionality in glance. However we do
not think it is the way to do it since glance behaves like a simple object
store.
Inheritance is defined by custom properties which leads us back to our problem.

Data model impact
-----------------

None

REST API impact
---------------

None

Security impact
---------------

This change requires elevated privilege.

Notifications impact
--------------------

None

Other end user impact
---------------------

None

Performance Impact
------------------

With the option enabled there should be a performance impact as the request
will get a new token for elevated authentication.

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
  * Unit tests

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

Example of image metadata :
http://docs.openstack.org/image-guide/content/image-metadata.html

Old blueprint with same issue :
https://blueprints.launchpad.net/glance/+spec/inherited-image-property-support

History
=======

None
