# How to Install and Configure the ICG Webform module

Guide for use: If you are an Islandora administrator with previous experience setting up Drupal webforms, then you will find this document offers more details than you probably need, but we hope that even you will find the level of detail into which this documentation goes helps you avoid making mistakes that can result in frustration and delays in implementation.

***

## Table of Contents

* Credits
* Test Environment

***

**2. For Administrators**
  * 1. Islandora Webform installation preliminaries
  * 3. Installing the Islandora Webform module
  * 4. Configuring permissions for the Islandora Webform module
  * 5. Configuring the Islandora Webform module’s XML Form
  * 6. Configuring the Drupal block of Islandora Webform submissions
  * 7. Configuring Drupal accounts for the Islandora Webform module
  * 8. Upgrading from an earlier version of the Islandora Webform module

**4. Enhanced Development**
  * 1. DHi @hamilton (local customizations)
  * 2. Uploading a file [not implemented yet]
  * 3. Search and retrieval of submissions [not written yet]
***

## Credits

* The Islandora Webform module was conceived by the Islandora Consortial Group (ICG)
  * https://github.com/Islandora-Collaboration-Group
* The module development was coordinated by the Digital Humanities Initiative at Hamilton College (http://dhinitiative.org/) and supported by funds from an Andrew W. Mellon Foundation grant to DHi at Hamilton College (http://dhinitiative.org/)
* The development was performed by Common Media (Patrick Dunlavey, developer)
* Beta testing was first performed by DHi at Hamilton College Collection Development Team (DHi Collection Development Team) and later reviewed by other members of the ICG.

***

## Test Environment
* Webform: 7.x-4.9 (webform)
* Webform AJAX: 7.x-1.1 (webform_ajax)
* Islandora Webform Module (islandora_webform)
* Islandora Ingest Module (islandora_webform_ingest)
* [includes Islandora Simple Text Module (islandora_simple_text_module)]
* Islandora: 7.1.7, and HEAD
* Drupal: 7.51

***

## Introduction to the Islandora Webform module

## For Administrators

**1. Islandora Webform installation preliminaries**

* Ensure that all basic Islandora modules and dependencies are installed and working.
* DHI@Hamilton tested the IW module with the latest versions of each of these modules enabled:

| Module Name | Status |
| ------------- |:-------------:| -----:|
| Drupal | required |
| Islandora | required, plus dependencies |
| Tuque | required |
| Islandora Basic Collection | required |
| Isandora XML Forms | required if Igest module is enabled |
| Webform | required |
| Webform AJAX | required |
| Token | optional |

**2. Understanding the _Islandora Simple Text Content Model_**

* The IW module comes bundled with a content model, the “Islandora Simple Text Content Model”. It helps to be aware of how this content model accommodates the values submitted by a webform. Understanding the content model can help you configure the webform components properly. So spend some time examining the content model and the XML metadata form it is associated with.
* The Content Model that is used by the IW module is part of the "Islandora Example Simple Text Solution Pack", which is installed when you install the main Islandora Webform module.
* The code (in Islandora Webform Ingest) supporting this CM grabs a form’s output and creates a Fedora object (or writes to the original object) and plugs in those values in a programmatic way into a MODS datastream which gets crosswalked to DC according to rules you can configure in an XSLT file.

**3. Installing the Islandora Webform module**

* The IW module actually consists of three modules plus a text-based content model. To learn more about each IW module, you should read the README file for each one on the code distribution repo.
* Common Media’s code repo:
  * github.com/commonmedia/islandora_webform.git

**3.1. First of all Install and Configure the Drupal Webform module**
```
> drush dl -y webform
> drush en -y webform (add @sites for multi-site setups)
> drush update (add @sites for multi-site setups)
```

* Before you can start using webforms in Drupal you should configure it:
Administer > Configuration > [Content Authoring] Webform settings
(or <your_site>/admin/config/content/webform)
* Uncheck any fields you don’t think you’ll need in any of your Webforms. [Or, just leave them all checked.]

[image]

* From address: "dhitech@hamilton.edu" (example only)
* From name: "Digital Humanities Initiative" (example only)
* Default subject: "Form submission from: [node:title]" (example only)
* Click "Save configuration".

**3.2. Download/Install the "Webform AJAX" modules**
```
> drush dl -y weborm_ajax
> drush en -y webform_ajax
```

**3.3. Download/Install the "Islandora Webform" module (there is more than one way to do this)**

* SSH into the Drupal server.
* Navigate to "sites/all/modules".
* Clone the islandora_webform module:
```
> git clone https://github.com/commonmedia/islandora_webform.git
```
* If you are just upgrading the IW modules from an earlier version, do the following steps before cloning the new webform:
  * Clear all caches for all sites
  * Disable the IW modules
  * Update the database for your site(s) [Add "@sites" if you have a Drupal multi-site setup.]
  ```
  > drush @sites cc all
> drush dis islandora_webform
> drush dis islandora_webform_ingest
> drush dis islandora_example_single_text
> drush updatedb
```
* Back up an customizations that will be overwritten when you upgrade the modules, such as:
```islandora_webform/submodules/islandora_webform_ingest/examples/islandora_example_simple_text_solution_pack/xsl/
modsrelated_to_dc.xsl
```
**3.4. Enable the Islandora Webform module for each site that needs it.**

* Shell method: SSH to the server
  * To enable it for the default site, run at sites/all/modules:
> drush en -y islandora_webform
> drush en -y islandora_webform_ingest
  * To enable it for all sites in multi-site, run at sites/all/modules:
> drush @sites en -y islandora_webform
> drush @sites en -y islandora_webform_ingest
  * To enable it for a specific site:
> drush en -y islandora_webform --uri=http://<your_site>
> drush en -y islandora_webform_ingest --uri=http://<your_site>
* Drupal method: Log into a Drupal site
  * Administer > Modules
    * Enable "Islandora Webform" (islandora_webform)
    * Enable "Islandora Webform Ingest" (islandora_webform_ingest)
    * Enable "Islandora example simple text" module (islandora_example_simple_text)
      * This module was installed as a submodule when the main IW module was installed, but you have to enable it manually.
* Update the database
```
> drush update (or in the Drupal GUI: "<your_site>/update.php")
```
* There are no configuration options for this module.

**3.5. Ensure that all dependencies are enabled**

* Administer > Modules
* Look for any Required but "missing" or "disabled" dependencies for the modules: Webform, Webform AJAX, Islandora Webform, and Islandora Webform Ingest modules, Islandora Example Simple Text.

**3.6 Understanding the structure of the IW modules**

* Module(s) directory structure (the three modules are italicized here):
```sites/all/modules
 |_islandora-webform
   |_README.txt
   |_submodules
     |_islandora_webform_ingest
       |_README.txt
       |_examples
         |_islandora_example_simple_text_solution_pack
           |_README.md
```

* Content Model
  * Islandora Simple Text Content Model (islandora:sp_example_text)
```
<dsCompositeModel xmlns="info:fedora/fedora-system:def/dsCompositeModel#">
 <dsTypeModel ID="DC">
     <form FORMAT_URI="http://www.openarchives.org/OAI/2.0/oai_dc/" MIME="application/xml"></form>
 </dsTypeModel>
 <dsTypeModel ID="RELS-EXT" optional="true">
     <form FORMAT_URI="info:fedora/fedora-system:FedoraRELSExt-1.0" MIME="application/rdf+xml"></form>
 </dsTypeModel>
 <dsTypeModel ID="RELS-INT" optional="true">
     <form FORMAT_URI="info:fedora/fedora-system:FedoraRELSInt-1.0" MIME="application/rdf+xml"></form>
 </dsTypeModel>
 <dsTypeModel ID="MODS" optional="true">
    <form FORMAT_URI="http://www.loc.gov/mods/v3" MIME="application/xml"></form>
 </dsTypeModel>
 <dsTypeModel ID="HTML" optional="true">
     <form MIME="text/html"></form>
    </dsTypeModel>
 <dsTypeModel ID="TN" ORDERED="false" optional="true">
    <form MIME="image/jpg"></form>
    <form MIME="image/jpeg"></form>
    <form MIME="image/png"></form>
 </dsTypeModel>
</dsCompositeModel>
```

**4. Configuring permissions for the Islandora Webform module**

* Administer > People > Permissions > Roles

[image]

  * Built-in roles:
    * anonymous
    * authenticated user
administrator
  * Add as many more roles as you think you'll need, e.g.
    * webform submitter (=authenticated user + all webform permissions)
    * webform manager (=authenticated user + limited webform permissions)
* Set desired permissions for each user role here:
  * Administer > Modules > Islandora Webform > Permissions (i.e., /admin/people/permissions#module-islandora_webform)
* See separate section below for permission settings: "Islandora Webform Permissions Settings".

**6. Configuring the Drupal block of Islandora Webform submissions**

* All of the submissions for an Islandora object can be made visible by configuring the IW block.
* Go to Administer > Structure > Blocks (ie. /admin/structure/block)
* In the section labeled "Disabled", find the block titled "Objects with isAnnotationOf relation" [The title may vary.]
* Select position: "Content" (Means place the block in the “content” region of the Drupal page.)
* Move the block to the bottom of the "Content" list of items, if necessary, so it displays at the bottom of the page.
* Click "Save blocks"
* Click "configure" next to the "Objects with isAnnotationOf relation".

[SHOULD THERE BE A SCREENSHOT HERE OF THE BLOCK CONFIG PAGE? MIGHT NOT REALLY BE NECESSARY, PJM]

***

  * Block title: "User Contributed Captions and Transcriptions". [example only]
  * View mode: "Links" [This is the most compact mode because it doesn't show thumbnails.]
  * Check "Only IW"
  * Pages (section)
    * Only the listed pages: [check]
    * In box: "islandora/object/*" (Means show this block only when displaying Islandora objects.)
  * Page Count: 10 (example only)
  * Roles (section)
    * authenticated user: [check] (make your own decision here whom to allow to see the submissions)
  * Click "Save".
* Click "Save blocks".

***

**7. Configuring Drupal accounts for the Islandora Webform module**

* The IW module and IW Ingest module automatically set some user permissions, but an administrator should verify that they meet local needs.
* If a link to your webform is to be seen by only authenticated users, an administrator should set permissions to restrict webform access to authenticated users only and create a Drupal account for those users and have them notified that they now have an account.
  * Username:  [username of individual user]
  * E-mail: [email address of the user]
  * Password: [any_dummy_password] (user can change this upon first use)
  * Status: Active (set to “Inactive” to prevent logging in)
  * Roles: webform submitter (has “authorized” user permissions)

***

**8. Upgrading from an earlier version of the Islandora Webform module.**

* Delete any existing “islandora_webform" directory and all its files.
```
> cd sites/all/modules (or wherever islandora_webform in located)
> drush cache-clear all
> drush dis islandora_webform (this also disables islandora_webform_ingest)
> rm -rf islandora_webform
> drush update
```
NOTES: 
* If you remove (rm) the modules you should protect files you may have manually customized such as 
```
islandora_webform/submodules/islandora_webform_ingest/examples/ .
      islandora_example_simple_text_solution_pack/xsl/modsrelated_to_dc.xsl
```
* If you need to wipe out IW completely and start over, run pm-uninstall after you disable the modules. This does not wipe out the webforms or the XML forms, but it will wipe out all your settings related to Islandora Ingest.
```
> drush pm-uninstall islandora_webform_ingest
> drush pm-uninstall islandora_webform
```

*** 

##Enhanced development

**1. DHi @hamilton (local customizations)**

* We add “User contribution:” to the title of a Fedora object created using the IW module.
  * <dc:title>User contribution: [title]</dc:title>
* This would probably better be done with RELS-EXT predicates, but we didn’t want to have separate forms for Captions and Transcriptions.
* We use “isAnnotationOf” as the predicate in the RELS-EXT of all Fedora objects created by the IW module, but a richer ontology should be desirable for reporting and searching purposes.

**2. Uploading a file**

* [THIS HAS NOT YET BEEN IMPLEMENT OR VERIFIED YET.]

* Be sure you are in the collection to which you want to submit your upload.
* If you are authorized to upload an object to this collection, you will see a block in the left sidebar labeled "Submitter Options" and in it a link labeled "Upload a file".
* The purpose of this is to make it possible for an authenticated user to upload objects that are ingested as related to the object being viewed.

* Click the “Upload a file” link.
* Select the content type of the object you will be uploading (PDF, basic image, etc.)
* Enter some metadata (only a "Title" is actually required).' Click "Next".
* Click "Browse".
  * Select the file on your computer.
  * Click "Upload".
* Click "Ingest".

* Then if you want to add a caption to it, click the link under the object "Submit a caption or transcription."
* These uploads will be ingested into Fedora, but they will not be visible to anonymous users until they are approved.
* [dev comment: We still have to look into the details of permissions to be sure these users can't mess with with objects other than their own. I'm not sure that is possible.

**3. Search and retrieval of submissions**

* All submitted text is put into an HTML datastream and the dc:relation field. We can offer searches that query those datastreams, but, unfortunately, Drupal/Islandora ignores the HTML tags in those fields and runs all the text together. So DHi decided to map the submission text MODS note element to the dc:description element in the "text/plain" DC datastream.
* I think we will have to find another way to render the transcription with the HTML tags.

***

Warranty and Copyright
(This statement has not yet been approved by Common Media, DHi, or ICG)

Copyright (C) 2015 ????

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU General Public License for more details.

***

**Islandora Webform Permission Settings**

* These permission are currently set restrictively, but can easily be loosened up.
  * Full management permissions are granted to the “administrator” and webform manager” roles.
  * Submission permissions are granted to the “webform submitter” role.
  * No webform permissions are granted to the “anonymous” and “authenticated” roles.

**Node (scroll down to the 'Webform:" settings)**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Webform: Create new content | - | - | X | X | X |
| Webform: Edit own content   | - | - | X | X | X |
| Webform: Edit any content   | - | - | X | X | - |
| Webform: Edit any content   | - | - | X | X | X |
| Webform: Delete any content | - | - | X | X | - |

**Islandora**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| View repository objects | X | X | X | X | X |

**Islandora Solr**
* Search the Solr Index (Checck all roles)

**Islandora Webform**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Manage Isl. Webforms      | - | - | X | - | - |
| Link Isl obj. to webforms | - | - | X | X | - |

**Islandora Webform Ingest**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Ingest Isl. Webform Submissions  | - | - | X | X | - |

**Webform (Drupal)**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Access all webform results | - | - | X | X | X |
| Access own webform results | - | - | X | X | X |
| Edit all webform submissions | - | - | X | X | - |
| Delete all webform submissions | - | - | X | X | - |
| Access own webform submissions | - | - | X | X | X |
| Edit own webform submission |  | - | X | X | X |
| Delete own webform submissions | - | - | X | X | X |
| Content authors: access and edit webofrm componenets and settings  |  |  | X | X | - |
***
