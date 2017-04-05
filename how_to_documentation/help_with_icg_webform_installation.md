# How to Install the Islandora Webform module

Guide for use: If you are an Islandora administrator with previous experience setting up Drupal webforms, then you will find this document offers more details than you probably need, but we hope that even you will find the level of detail into which this documentation goes helps you avoid making mistakes that can result in frustration and delays in implementation.

## Table of Contents

* Credits
* Test Environment
* 1. Installation preliminaries
* 2. Install the Drupal "Webform" module
* 3. Install the "Webform AJAX" module
* 4. Install the "Islandora Webform" module
* 5. Create Drupal Roles and set permissions for users of the Islandora Webform module
* 6. Create Drupal User Accounts and assign Roles for users of the Islandora Webform module
* 7. Enable the Drupal block for Islandora Webform submissions

APPENDIX: Upgrading from an earlier version of the Islandora Webform module

***

## Credits

* The Islandora Webform module was conceived by the Islandora Collaboration Group (ICG)
  * https://github.com/Islandora-Collaboration-Group
* The module development was coordinated by the Digital Humanities Initiative (DHi) at Hamilton College (http://dhinitiative.org/) and supported by funds from an Andrew W. Mellon Foundation grant to DHi.
* The development was performed by Common Media (Patrick Dunlavey, developer)
  * http://commonmedia.com
* Beta testing was first performed by the DHi Collection Development Team and reviewed by other members of the ICG.

***

##1. Installation preliminaries

**Test Environment**
* DHi last tested the IW module in February of 2017 using the following versions of each of these modules and libraries:

| Module Name | Version |
| ------------- |:-------------:| -----:|
| CentOs | - |
| Drupal | 7.51 |
| Islandora | 7x-1.7 |
| Tuque | 7x-1.7 |
| Islandora Basic Collection | 7x-1.7 |
| Islandora XML Forms | 7x-dev |
| Webform | 7.x-4.14 |
| Webform AJAX | 7.x-1.1 |

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |

* Ensure that basic Islandora modules and dependencies are installed and working, namely
  * Islandora, Islandora Basic Colelction, Islandora XML Form, and Tuque.
  * Ensure that the Islandora connection to Fedora is working (administration > Islandora)

***

##2. Install the Drupal "Webform" module

```
> drush dl -y webform
> drush en -y webform (add @sites for multi-site setups)
> drush -y updatedb (add @sites for multi-site setups)
```

**Configure the Drupal "Webform" module**

* Administer > Configuration > Content Authoring > Webform settings (or <your_site>/admin/config/content/webform)

***

![webform_18.png](/how_to_documentation/images/webform_18.png)

Figure 1: Configuring the Drupal webform module (part 1 of 2)

***

* Uncheck any fields you don’t think you’ll need in any of your Webforms. [Or, just leave them all checked.]

***

![webform_15.png](/how_to_documentation/images/webform_15.png)

Figure 2: Configuring the Drupal webform module (part 2 of 2)

***

* Fill in the e-mail values as appropriate.
* Click "Save configuration".

***

##3. Install the "Webform AJAX" module

```
> drush dl -y weborm_ajax
> drush en -y webform_ajax (add @sites if needed for all sites in a multi-site Drupal installation)
```

***

##4. Install the "Islandora Webform" module

* The IW module actually consists of three modules and they all need to be enabled individually (in Drupal or with drush).
  * islandora_webform
  * islandora_webform_ingest
  * islandora_simple_text_solution_pack

* On the Drupal server, navigate to "sites/all/modules".
* [If you are upgrading the IW modules, see the APPENDIX to this document before proceeding.]
* Clone the islandora_webform module:
```
> git clone https://github.com/commonmedia/islandora_webform.git
```
* Enable the Islandora Webform module for each site that needs it.
```
> drush en islandora_webform
> drush en islandora_webform_ingest
> drush en islandora_example_simple_text
```
* Update the database.
```
> drush updatedb (or in the Drupal GUI: "<your_site>/update.php")
```
* The directory structure of the IW modules
```sites/all/modules
 |_islandora-webform
   |_islandora_webform_module
   |_submodules
     |_islandora_webform_ingest
       |_islandora_webform_ingest.module
       |_examples
         |_islandora_example_simple_text_solution_pack
           |_islandora_example_simple_text.module
```
* To learn more about each IW module, consult the README file for each one on the IW code distribution repo.
  * github.com/commonmedia/islandora_webform.git
  
**Ensure that all dependencies for these webform modules are installed and enabled**

* Administer > Modules
* Look for any Required but "missing" or "disabled" dependencies for the modules: Webform, Webform AJAX, Islandora Webform, and Islandora Webform Ingest modules, Islandora Example Simple Text.
* There are no global configuration options for the IW module. All configuration is managed separately for each webform created by users of the IW module.

***

##5. Create Drupal Roles and sest permissions for the Islandora Webform module

* Depending on your needs, you may need to create a couple of new Drupal user roles so you can give different sets permissions to difference groups of webform users.
* Administer > People > Permissions > Roles

***

![webform_16.png](/how_to_documentation/images/webform_16.png)

Figure 3: Configuring Drupal Roles for the Islandora Webform module users 

***

* Add as many new roles as you think you'll need, e.g.
  * webform manager (=authenticated user + all webform permissions)
  * webform submitter (=authenticated user + limited webform permissions)
* Set desired permissions for each user role here:
  * Administer > Modules > Islandora Webform > Permissions (i.e., /admin/people/permissions#module-islandora_webform)

**Configure Islandora Webform Permissions**

* These permission are currently set restrictively, but can easily be loosened up.
  * Full management permissions are granted to the “administrator” and webform manager” roles.
  * Submission permissions are granted to the “webform submitter” role.
  * No webform permissions are granted to the “anonymous” and “authenticated” roles.

***

**Node (scroll down to the 'Webform:" settings)**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Webform: Create new content | - | - | X | X | X |
| Webform: Edit own content   | - | - | X | X | X |
| Webform: Edit any content   | - | - | X | X | - |
| Webform: Edit any content   | - | - | X | X | X |
| Webform: Delete any content | - | - | X | X | - |

***

**Islandora**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| View repository objects | X | X | X | X | X |

***

**Islandora Solr**
* Search the Solr Index (Checck all roles)

***

**Islandora Webform**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Manage Isl. Webforms      | - | - | X | - | - |
| Link Isl obj. to webforms | - | - | X | X | - |

***

**Islandora Webform Ingest**

| Feature | anon. | authen. | admin. | webform mgr | webform submitter |
| ------------- |:-------------:| :-----:| :-------------: |:-------------:| :-----:|
| Ingest Isl. Webform Submissions  | - | - | X | X | - |

***

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

##6. Create and Configure Drupal accounts for users of the Islandora Webform module

* The IW module and IW Ingest modules automatically set some user permissions, but an administrator should verify that these permissions meet local needs.
* If a link to your webform is to be seen by only authenticated users, an administrator should set permissions to restrict webform access to authenticated users only.
* Create a Drupal account for those users according to local needs.
  * Username:  [username of individual user]
  * E-mail: [email address of the user]
  * Password: [any_dummy_password] (user can change this upon first use)
  * Status: Active (set to “Inactive” to prevent logging in)
  * Roles: webform submitter (has “authenticated” user permissions)

***

##7. Enable the Drupal block for Islandora Webform submissions

* All of the submissions for an Islandora object can be made visible to users by configuring the IW block.
* Go to Administer > Structure > Blocks (ie. /admin/structure/block)
* In the section labeled "Disabled", find the block titled "Objects with isAnnotationOf relation" [The title may vary.]
* Select position: "Content" (Means place the block in the “content” region of the Drupal page.)
* Move the block to, say, the top of the "Content" list of items if you want the "Submission" link to be displayed at the top of the content block.
* Click "Save blocks"
* Click "configure" next to the "Objects with isAnnotationOf relation".

***

![webform_19.png](/how_to_documentation/images/webform_19.png) [need image]

* Figure 4: Configuring the Drupal block of Islandora Webform submissions

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

##APPENDIX: Upgrading from an earlier version of the Islandora Webform module.**

* An upgrade of these modules will not delete any webforms you have created (they are in mySQL), but your webforms may need to be tweaked to become compatible with the newer version of the IW module.
* When you upgrade the IW modules from an earlier version, do the following steps before cloning the new webform:
* Disable the Islandora webform module
```
> cd sites/all/modules (or wherever islandora_webform in located)
> drush cache-clear all
> drush dis islandora_webform (this also disables islandora_webform_ingest)
```
* If you need to wipe out IW completely and start over, run pm-uninstall after you disable the modules. This does not wipe out the webforms or the XML forms, but it will wipe out all your settings related to Islandora Ingest.
```
> drush pm-uninstall islandora_webform_ingest
> drush pm-uninstall islandora_webform
```
* Delete any existing “islandora_webform" directory and all its files.
* Before you delete the modules back up any files that you have customized in the Islandora Weborm directories. These will be overwritten when you upgrade the modules, such as:
```
islandora_webform/submodules/islandora_webform_ingest/examples/ .
      islandora_example_simple_text_solution_pack/xsl/modsrelated_to_dc.xsl
```
* When you are ready to delete all IW files, you can do this:
```
> rm -rf islandora_webform
> drush update
```

*** 
