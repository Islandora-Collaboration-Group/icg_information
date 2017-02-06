# How to Install and Configure the ICG Webform module

Guide for use: If you are an Islandora administrator with previous experience setting up Drupal webforms, then you will find this document offers more details than you probably need, but we hope that even you will find the level of detail into which this documentation goes helps you avoid making mistakes that can result in frustration and delays in implementation.

## Table of Contents

* Credits
* Test Environment
* 1. Islandora Webform installation preliminaries
* 2. Install the Drupal Webform module
* 3. Install the Webform AJAX module
* 4. Install the Islandora Webform module
* 5. Configure Drupal Roles for the Islandora Webform module
* 6. Configure Drupal Accounts for the Islandora Webform module
* 7. Configuring the Drupal block of Islandora Webform submissions
* 8. Upgrading from an earlier version of the Islandora Webform module

***

## Credits

* The Islandora Webform module was conceived by the Islandora Collaboration Group (ICG)
  * https://github.com/Islandora-Collaboration-Group
* The module development was coordinated by the Digital Humanities Initiative (DHi) at Hamilton College (http://dhinitiative.org/) and supported by funds from an Andrew W. Mellon Foundation grant to DHi.
* The development was performed by Common Media (Patrick Dunlavey, developer)
  * http://commonmedia.com
* Beta testing was first performed by the DHi Collection Development Team) and later reviewed by other members of the ICG.

***

## Test Environment

**1. Islandora Webform installation preliminaries**

* Ensure that all basic Islandora modules and dependencies are installed and working.
* DHi last tested the IW module in February of 2017 using the following versions of each of these modules and libraries:

| Module Name | Status |
| ------------- |:-------------:| -----:|
| Drupal | 7.51 |
| Islandora | 7x-1.7 |
| Tuque | 7x-1.7 |
| Islandora Basic Collection | 7x-1.7 |
| Isandora XML Forms | 7x-dev |
| Webform | 7.x-4.14 |
| Webform AJAX | 7.x-1.1 |

***

**2. Install the Drupal Webform module**

```
> drush dl -y webform
> drush en -y webform (add @sites for multi-site setups)
> drush update (add @sites for multi-site setups)
```
* Administer > Configuration > [Content Authoring] Webform settings (or <your_site>/admin/config/content/webform)
  * See Figure 1: Configuring the Drupal webform module
* Uncheck any fields you don’t think you’ll need in any of your Webforms. [Or, just leave them all checked.]

![webform_15.png](/how_to_documentation/images/webform_15.png)

Figure 1: Configuring the Drupal webform module

* From address: "dhitech@hamilton.edu" (example only)
* From name: "Digital Humanities Initiative" (example only)
* Default subject: "Form submission from: [node:title]" (example only)
* Click "Save configuration".

***

**3. Install the Webform AJAX modules**
```
> drush dl -y weborm_ajax
> drush en -y webform_ajax
```

***

**4. Install the Islandora Webform module (there is more than one way to do this)**

* The IW module actually consists of three modules:
  # islandora)webform
  # islandora_webform_ingest
  # islandora_simple_text_module
* The islandora_simple_text_module comes with its own Content Model.
* To learn more about each IW module, you should read the README file for each one on the IW code distribution repo.
  * Common Media’s code repo:
    * github.com/commonmedia/islandora_webform.git
  
* On the Drupal server, navigate to "sites/all/modules".
* Clone the islandora_webform module:
```
> git clone https://github.com/commonmedia/islandora_webform.git
```
* If you are just upgrading the IW modules, see the section 8. later in this document.

**Enable the Islandora Webform module for each site that needs it.**

* Shell method: SSH to the server
  * To enable it for the default site, run at sites/all/modules:
  ```
> drush en -y islandora_webform
> drush en -y islandora_webform_ingest
```
  * To enable it for all sites in multi-site, run at sites/all/modules:
  ```
> drush @sites en -y islandora_webform
> drush @sites en -y islandora_webform_ingest
```
  * To enable it for a specific site:
  ```
> drush en -y islandora_webform --uri=http://<your_site>
> drush en -y islandora_webform_ingest --uri=http://<your_site>
```
* Drupal method: Log into a Drupal site
  * Administer > Modules
    * Enable "Islandora Webform" (islandora_webform)
    * Enable "Islandora Webform Ingest" (islandora_webform_ingest)
    * Enable "Islandora example simple text" module (islandora_example_simple_text)
      * This module was installed as a submodule when the main IW module was installed, but you have to enable it manually.
* Update the database.
```
> drush update (or in the Drupal GUI: "<your_site>/update.php")
```

**Ensure that all dependencies are enabled**

* Administer > Modules
* Look for any Required but "missing" or "disabled" dependencies for the modules: Webform, Webform AJAX, Islandora Webform, and Islandora Webform Ingest modules, Islandora Example Simple Text.

**Understanding the structure of the IW modules**

* Module(s) directory structure
```sites/all/modules
 |_islandora-webform
   |_submodules
     |_islandora_webform_ingest
       |_examples
         |_islandora_example_simple_text_solution_pack
```

**Configure the Islandora Webform module

* Actually, there are no global configuration options for this module.
* Configuration is managed separately for each webform you set up.

***

**5. Configure Drupal Permissions for the Islandora Webform module**

* Administer > People > Permissions > Roles

![webform_16.png](/how_to_documentation/images/webform_16.png)

Figure 2: Configure Drupal Permissions for the Islandora Webform module 

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

**6. Configure Drupal accounts for the Islandora Webform module**

* The IW module and IW Ingest modules automatically set some user permissions, but an administrator should verify that these permissions meet local needs.
* If a link to your webform is to be seen by only authenticated users, an administrator should set permissions to restrict webform access to authenticated users only.
* Create a Drupal account for those users according to local needs.
  * Username:  [username of individual user]
  * E-mail: [email address of the user]
  * Password: [any_dummy_password] (user can change this upon first use)
  * Status: Active (set to “Inactive” to prevent logging in)
  * Roles: webform submitter (has “authenticated” user permissions)

***

**7. Configuring the Drupal block of Islandora Webform submissions**

* All of the submissions for an Islandora object can be made visible to users by configuring the IW block.
* Go to Administer > Structure > Blocks (ie. /admin/structure/block)
* In the section labeled "Disabled", find the block titled "Objects with isAnnotationOf relation" [The title may vary.]
* Select position: "Content" (Means place the block in the “content” region of the Drupal page.)
* Move the block to, say, the top of the "Content" list of items if you want the "Submission" link to be displayed at the top of the content block.
* Click "Save blocks"
* Click "configure" next to the "Objects with isAnnotationOf relation".

![webform_17.jpg](/how_to_documentation/images/webform_17.jpg)

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

**8. Upgrading from an earlier version of the Islandora Webform module.**

* Delete any existing “islandora_webform" directory and all its files.
```
> cd sites/all/modules (or wherever islandora_webform in located)
> drush cache-clear all
> drush dis islandora_webform (this also disables islandora_webform_ingest)
> rm -rf islandora_webform
> drush update
```

***

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

[TO BE MERGED WITH THE ABOVE SECTION.]

* If you are just upgrading the IW modules from an earlier version, do the following steps before cloning the new webform:
  * Clear all caches for all sites.
  * Disable the IW modules.
  * Update the database for your site(s) [Add "@sites" if you have a Drupal multi-site setup.]
  ```
> drush cc all
> drush dis islandora_webform
> drush dis islandora_webform_ingest
> drush dis islandora_example_single_text
> drush updatedb
```
* An upgrade of these modules will not delete any webforms you have created (they are in mySQL), but your webforms may need to be tweaked to become compatible with the newer version of the IW module.
* Back up any files that you have customized in the Islandora Weborm directories. These will be overwritten when you upgrade the modules, such as:
```
islandora_webform/submodules/islandora_webform_ingest/examples/islandora_example_simple_text_solution_pack/xsl/
modsrelated_to_dc.xsl
```

***

Warranty and Copyright
(This statement has not yet been approved by Common Media, DHi, or ICG)

Copyright (C) 2015 ????

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU General Public License for more details.

***
