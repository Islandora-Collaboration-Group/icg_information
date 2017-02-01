# Documentation on the Islandora Webform Module
(updated 2016-02-28, by Peter MacDonald)

## Test Environment
* Webform: 7.x-4.9 (webform)
* Webform AJAX: 7.x-1.1 (webform_ajax)
* Islandora Webform Module (islandora_webform)
* Islandora Ingest Module (islandora_webform_ingest)
* [includes Islandora Simple Text Module (islandora_simple_text_module)]
* Islandora: 7.1.5, 7.1.6, HEAD
* Drupal: 7.41

* * * 

## Table of Contents

Introduction to the Islandora Webform module
1. Basic capabilities
2. Credits

For Webform Managers
3. Creating and configuring a new Islandora Webform
3b. Enabling webforms on only certain objects [not written yet]
4. Configuring Drupal accounts for the Islandora Webform module

For End Users
5. Submitting an Islandora Webform

For Administrators
6. Islandora Webform installation preliminaries
7. Understanding the Islandora Simple Text content model
8. Installing the Islandora Webform module
9. Configuring permissions for the Islandora Webform module
10. Configuring the Islandora Webform module’s XML Form
11. Configuring the Drupal block of Islandora Webform submissions
12. Upgrading from an earlier version of the Islandora Webform module.

Enhanced Development
* 13. Uploading a file [not implemented yet]
* 14. Search and retrieval of submissions [not written yet]

## Warranty and Copyright

Guide for use: If you are an Islandora administrator with previous experience setting up Drupal webforms, then you will find this document offers more details than you probably need, but we hope that even you will find the level of detail into which this documentation goes helps you avoid making mistakes that can result in frustration and delays in implementation.

## Introduction to the Islandora Webform module

1. Basic capabilities

* The Islandora Webform (IW) module uses the capabilities of the standard Drupal Webform module to enable users to submit comments (captions, tags, transcriptions, etc.) on digital objects in an Islandora repository.
* In Islandora, a link to a webform appears on the object view page that launches a webform that captures a user’s input and puts the submitted webform into a queue waiting for approval by a webform manager.
* When approved, the submission is ingested into a new Fedora object where the content is mapped by a customizable XML metadata form to designated MODS elements which are crosswalked by a customizable XSLT to Dublin Core, and a relationship statement is placed in the RELS-EXT datastream connecting the submission to the original object.
* All the submissions for a specific object can be displayed along with the original object.
* When an IW webform is configured, it can be bound to a single content model (basic image, IA Book reader, etc.). If you do bind it to a single content model, then you have to create a specific webform for each content model. You can also bind as webform to specific collections.

## Know the Limitations of the IW Module

* After a submission is ingested into Fedora, the IW “Submissions” page will shows “Re-Ingest” in a red font. It will also show links to “View”, “Edit” and “Delete” the submission. However, once the submission has been ingested, any edits made through this page will not replace the text already ingested. If you do edit the text of the submission and you then click the red “Re-ingest” link, the IW module will create a brand new Fedora object -- leaving the original one still on place.
* Implications of this are that it might be advisable to “Delete” a submission from the “Submissions” page once the ingest has been deemed successful. “Delete” only deletes the entry for the submission on the Submissions page (a mySQL deletion) -- it does not delete the Fedora object.
* Another implication is that if you ever need to edit the content of a submission, you should do the editing using the XML metadata form originally used to create that object.
* You can associate a webform with only one Islandora collection object at a time, so if you are in the practice of creating many collection objects to organize your repository’s content, you will need to create a separate webform for each collection. Since there is currently no way to clone a webform, each webform you need will have to be configured separately.

## 2. Credits

* The Islandora Webform module was conceived by the Islandora Consortial Group (ICG)
** https://sites.google.com/site/islandoraconsortiagroup/
* The module development was coordinated by the Digital Humanities Initiative at Hamilton College (http://dhinitiative.org/)
* The development was performed by Common Media (Patrick Dunlavey, developer)
* Beta testing was first performed by DHi at Hamilton College Collection Development Team (DHi Collection Development Team) and later reviewed by other members of the ICG.
* The development was supported by funds from an Andrew W. Mellon Foundation grant to DHi at Hamilton College (http://dhinitiative.org/) 

## For Webform Managers
3. Creating and configuring a new Islandora Webform

1. Create a new Drupal webform

* Log in to the site (URL) where you want to create a webform. Be sure your account/role is permitted to create webforms.
* Administer > Content; Click Add content; Select "Webform" (i.e., /node/add/webform).
** [If a webform has never been created before on this site, you might not see “webforms” in the list of content types. If "Webform" is not listed here, then your administrator will have to add it (see Administer > Structure > Content types (i.e., /admin/structure/types)
* Create Webform
** Add values to the fields to the webform as follows:



