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

**Introduction to the Islandora Webform module**
* 1. Basic capabilities  
* 2. Credits  

**For Webform Managers**
* 3. Creating and configuring a new Islandora Webform   
* 3b. Enabling webforms on only certain objects  
* 4. Configuring Drupal accounts for the Islandora Webform module  

**For End Users**
* 5. Submitting an Islandora Webform  

**For Administrators**
* 6. Islandora Webform installation preliminaries  
* 7. Understanding the Islandora Simple Text content model  
* 8. Installing the Islandora Webform module  
* 9. Configuring permissions for the Islandora Webform module  
* 10. Configuring the Islandora Webform module’s XML Form  
* 11. Configuring the Drupal block of Islandora Webform submissions  
* 12. Upgrading from an earlier version of the Islandora Webform module  

**Enhanced Development**
* 13. Uploading a file [not implemented yet]  
* 14. Search and retrieval of submissions [not written yet]  

## Warranty and Copyright

Guide for use: If you are an Islandora administrator with previous experience setting up Drupal webforms, then you will find this document offers more details than you probably need, but we hope that even you will find the level of detail into which this documentation goes helps you avoid making mistakes that can result in frustration and delays in implementation.

## Introduction to the Islandora Webform module

**1. Basic capabilities**

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

**3. Creating and configuring a new Islandora Webform**

**3.1. Create a new Drupal webform**
* Log in to the site (URL) where you want to create a webform. Be sure your account/role is permitted to create webforms.
* Administer > Content; Click Add content; Select "Webform" (i.e., /node/add/webform).
  * [If a webform has never been created before on this site, you might not see “webforms” in the list of content types. If "Webform" is not listed here, then your administrator will have to add it (see Administer > Structure > Content types (i.e., /admin/structure/types)
* Create Webform
  * Add values to the fields to the webform as follows:

[image]
*  
  * Title: "IW PDF webform." (Customize this text to include the object content type (PDF, etc.) and/or the target collection name.
    * Actually, you can name it however you want -- depending on how narrowly or broadly you want the form to be used.
    * For example: "IW PDF webform for the Sacred Centers of India collection."
  * Comment settings (appears only of "comments" is enabled for your site):
    * Closed: [check] (The IW module works just fine with the built-in Comments set to “Closed”.]
  * Publishing options:
    * Published: [check]
    * Promoted to front page: [uncheck]
    * Sticky at top of lists: [uncheck]
* Click "Save" (button).

**2. Add Components and fields to your webform**

* If this is your first webform, you will now be at the Webform > Form components page.  
  * But if you are returning to edit an existing webform, you will first need to select the webform that you want to work on: Administer > Content > Webforms (e.g., /admin/content/webform). Then find the title of your webform.  

[image]
[image]

*  
  * Create as many components (fields) as you want to be displayed on the form for the user to fill out.

* For a new webform, the only component required is one for the submitted text (i.e., the “Caption”, “Transcription”, whatever). 
  * Other components that you might find useful to configure are: 
    * today’s date
    * user’s Drupal account ID
    * submission type (a select box offering, say “Caption”, “Transcription”, and “Other”
  * but the IW module only requires a field to hold the submitted text. The rest are optional and should be determined by your needs.
  * Enter values for each desired component of the form (the following are example values only)
    * Label: "Caption or Transcription" (or, maybe, just “Submission text”)
    * Type: select "Textarea" (“textarea” provides a larger area for text entry than “textfield” does.)
    * Value: [blank] (You will edit this field later.)
    * Required: [check]
  * Click "Add" (button) to save each component as you create it.
* When you click “Add”, you will be taken to a page where you should continue configuring the component you just chose to Add.
 
 [image]
*  
  * Configure this component
    * Label: [prepopulated] (Will show the Label you previously specified for this component.)
    * Field Key: [prepopulated] (Will be created automatically from the component's Label.)
    * Default value (optional):  [Leave blank and use the “Placeholder” setting discussed below.]

[image]

  *  
    * Description: [Usually you will just leave this blank, but you can add text as seen here.]
      * Note: Most HTML tags are ignored in the Description box.
      * Example (using “Filtered HTML” since it looks like "Full HTML" is not allowed):
      
      `<strong>Instructions</strong>: HTML tags you may use: &lt;a&gt; &lt;strong&gt; &lt;p&gt; and &lt;br&gt;. [If you are doing a transcription, please follow the <a href="/transcription-instructions" target="_blank">Transcription instructions</a>]`
      
[image]

**Validation**
* Required: [check]

**Display**
* Resizable: [check]
* Label display: select "Above" [can be changed later]

**Placeholder**
* Supply message (optional): “-- Put your input here. --”

[Other options may be left blank for now.]

* Click "Save component" (button).
* Now you can add more components until you have added all the ones you want, such as "First Name", "Last Name", "Drupal user account", "Date" and so on. If you create custom fields, you will later have to modify the metadata XML form to ensure there is a matching MODS element there you can map the component to.
* When done adding components, click "Save" (button) to save the whole webform. This is very important, but easy to forget.

**3. Configure the Confirmation message as follows:**

* Be sure you are on the “Form settings” page.
  * Help finding "Form settings" page
    * Administer > Content > Webforms (i.e., /admin/content/webform)
    * Find your webform, click the "Edit" link, then click the "Webform" tab, then click the "Form settings" button.

[image]

* Submission Settings
  * Confirmation message: "Thank you for submitting your caption." (example only)
    * You can add Drupal tokens in the confirmation message, e.g.
      * “Thank you [current-user:name] for your submission.”
      * “[current-user:name]” is a Drupal token you can use here if you want.
  * Text format: "Full HTML" (your text format options may differ -- depending on how "text formats" are set up on your Drupal instance)
    * Help configuring Text formats:
      * Administer > Configuration > Content authoring > Text formats  (i.e., /admin/config/content/formats).
  * “Full HTML” allows you to use any HTML tags you want.
  * Redirection location
    * Confirmation page: [uncheck]
    * Custom URL: [leave blank]
    * No redirect (reload current page): [check] [The other two options cause navigation problems for users.]            
* Fill in any remaining options as needed, but the defaults should all work fine.
* Inline Islandora Webform [If this fieldset is missing, it is because the webform_ajax" module has not been installed.]

[image]

*  
  * Inline AJAX mode: [check] (AJAX is used to put the webform inline with the original (target) object being commented on.
  * Show confirmation screen: [check, if visible] (Possible bug: this has been known to generate duplicate confirmation messages, but unchecking it may generate an error.)

* **Submission Access - Roles that can submit this webform**
  * anonymous user: [uncheck]
  * authenticated user: [uncheck]
    * [Unless, of course you actually do decide to let all authenticated users make a submission.]
  * administrator: [check]
  * webform manager: [check]
  * webform submitter: [check]
* Fill in any remaining options as needed, but the defaults should all work fine.

* **Progress Bar [no changes required]**
* **Preview Page**
  * Enable preview page: [leave this unchecked] (Do not enable this without thoroughly testing the user experience.)
* **Advanced Settings**
  * Accept the defaults settings for now because no best practices exist for these settings yet.             
* Click "Save configuration" (button).

**4. Configure the Islandora settings for the webform**

* WARNING: Before you change anything on this page, be aware that if this webform has already been used for any submissions and those submissions have not yet been ingested, those submissions might not ingest properly. As a precaution, you should ingest all pending webforms submissions before making any changes to an existing webform’s Islandora settings. If you are creating a new webform, you don't have to worry about this.
  * Ensure you are on the “Form settings” page, if not…
  * Go to Administer > Content > Webforms (i.e., /admin/content/webform)
  * Find the title of your webform and click the "Components" link.
* Click the Webform (tab) and then "Islandora settings" (button)

[image]

* **Islandora Options**
  * Enabled: [check]
  * Content model filter: [Select one of the options]
* This setting determines which Islandora pages will have a link to this webform on them.
* The drop-down list shows the names of all content models it finds in Fedora. The labels shown come from the Label property of the Fedora object itself.
  * “Any” [Do not select this option. This would place a webform link on every object --  including collection objects and under thumbnails of every object in a search result set.]
  * Example: "Islandora PDF Content Model"
* Collection filter: [Select one of the options.]
  * "Any" (This option means this form can be used in any collection/site.)
  * [It is recommended that you not set this to “Any” on a production site.]
* The drop-down list shows the titles of all "collection" objects (MIME-type collections and content collections and "sub-collection" objects). The labels shown come from the Label property of the Fedora object itself.
  * "American Prison Writing Project"
* Specifying a collection means that this form will be offered as a link on objects only in that collection.
* Be sure to select a collection that has objects that subscribe to the content model you specified for the “Content model filter.”
  * PID Search String: [leave blank if all objects that qualify according to the above criteria.]
    * regex options are: [no example available]
      * [COMMENT: We need examples of this to guide us, try "sci:1*, lib*]
  * Add a link to...: [select one of the two option below]
    * "All matched objects" (Means a link to the webform will appear on all objects as defined on this page.)
    * "Only those objects that are manually tagged for this webform"
* If you select this, you will later need to select each object that should have a link to the webform. (see section “”##).
  * Link Text: "Add a caption for this item." [example only]
    * Other examples: "Transcribe this item." or a general use one like “Comment on this item.”
  * Link help text: "Your input is greatly appreciated." [example only]
* **Islandora Ingest**
  * Enable: [check]
  * Ingest destination: Select "Create new Islandora Simple Text Content Model" (Means create a Fedora object that subscribes to the islandora:sp_example_text content model.)
  
[image]

* If you do not see "Create new Islandora Simple Text Content Model", save this page (first uncheck "Enable" though) and ask the administrator to download/install/enable the "Islandora Example Simple Text Solution Pack". The Fedora content model object for the Solution Pack has to be installed too. Then come back and finish these instructions.
  * Relationship to current object: Select "is Annotation Of"
    * [WARNING: Do not use the predicate “isMemberOfCollection”. Doing so brings the risk of relationships corruption throughout your Fedora database.]
* At the moment, the "master" branch in IW is configured to use the default Fedora ontology only.
* There is a proposed enhancement to allow configuring any standards-based ontology here, but it is not yet an official project.
* You should consult the default fedora ontology for the meaning of the various predicates in this list:
* Fedora Digital Object Relationships (Fedora 3.x)
  * http://www.fedora-commons.org/documentation/3.0/userdocs/digitalobjects/introRelsExt.html
* Fedora Object Ontology (Fedora 3.x)
  * http://www.fedora.info/definitions/1/0/fedora-relsext-ontology.rdfs
* Namespace of new object: "apwiw" [example only]
* Ensure that whatever namespace you choose is allowable in the collection you specified above under "Collections filter". [NOTE: Not sure this is true. That is, does Solr need it for searching. Still TBD.]
* Click "Save configuration" (button).

**5. Configure Islandora Ingest Mapping (to specify where the component’s content will be stored in the Fedora object)**

* The IW module doesn't predetermine which components (i.e. form fields) you use in your webform. This is determined by your needs, but whatever components you choose must be mapped to MODS element paths in the specified metadata XML form. That said, since most content models require a <mods:title> element. However, the crosswalk that comes with the IW module crosswalks <mods:title> to <dc:relation>. DHi@Hamilton changed this crosswalking XSLT so it maps it to <dc:title>. (But this is not the place for a full explanation of how to do this.)
* Navigate to the Webform "Form components" page:
* Administer > Content > Webforms (tab) > find the title of your webform and click "Components" (link).
* Find the component that will store the text of the submission and click the "Edit" link.

* **Islandora Ingest Mapping**

[image]

*  
  * Ingest?: Select "Append" [This is the preferred option. The other options are: "Do not ingest" and "Replace"]
  * DataStream: "Select MODS" (The datastream labels listed here are those of the “Islandora Simple Text Content Model” which is used by Islandora for creating the caption object in Fedora.)
  * Field: Select "relatedItems:relTitleInfo:relTitle (text/plain)" [Select the path to the MODS form element where you want the main webform text to be stored. The default XML form is "Simple Text Related Item MODS form".]
* Click "Save component" (button)
* Now you can proceed to map all the remaining components (except for the "Islandora object PID") to MODS fields in the XML form. Here are some example mappings from one of DHi's forms:
  * Submission - relatedItems:noteTab:0:noteText (text/plain)
  * Type of Submission - relatedItems:relatedGenre (text/plain)
  * Short title - relatedItems:relTitleInfo:relTitle (text/plain)
  * Last Name - relatedItems:relNameInfo:family (text/plain)
  * First Name - relatedItems:relNameInfo:given (text/plain)
  * User Account - relatedItems:relNameInfo:affiliation (text/plain)
  * Date - relatedItems:relOriginInfo:relDateCreated (text/plain)
  
**6. (Optional) Check out the Islandora object PID component**

* At this point, the Islandora Webform module has silently added a new component to your webform labeled "Islandora object PID".
* The "Islandora object PID" component holds the PID of the parent Islandora object. It does not need to be edited manually. It is automatically generated and inherits some settings from other components in the same webform. Upon ingest of a submission, the IW code stores the parent PID in the RELS-EXT datastream of the new object. Example:
```<fedora:isAnnotationOf rdf:resource="info:fedora/islandora:1">
</fedora:isAnnotationOf>```
* (Optional) Examine this new component
* Administer > Content > Webforms (i.e. /admin/content/webform)
* Find the title of your webform > click "Components", and you will see the component "Islandora object PID".
  * Label: "Islandora object PID"
  * Type: "Textfield"
  * Value: -
  * To see more of its fields, click "Edit".
    * Label: "Islandora object PID" [do not change]
    * Field Key: "islandora_object_pid" [do not change]

[image]

**3b. Enabling webforms on only certain objects**

* If you want links to the webform to appear on only Islandora pages for only certain objects, you need to indicate this when editing the “Islandora settings” page. Look for “Add a link to” and select "Only those objects that are manually tagged for this webform".
* Then you need to navigate to each Islandora object display page on which you want a link to the webform to appear and click the following link (“Go to web form” will be the name of your webform).
  * add webform link: "Go to web form" (wording may vary)

**4. Configuring Drupal accounts for the Islandora Webform module**

* The IW module and IW Ingest module automatically set some user permissions, but an administrator should verify that they meet local needs.
* If a link to your webform is to be seen by only authenticated users, an administrator should set permissions to restrict webform access to authenticated users only and create a Drupal account for those users and have them notified that they now have an account.
  * Username:  [username of individual user]
  * E-mail: [email address of the user]
  * Password: [any_dummy_password] (user can change this upon first use)
  * Status: Active (set to “Inactive” to prevent logging in)
  * Roles: webform submitter (has “authorized” user permissions)

## For End Users

**5. Submitting an Islandora Webform**

* An authenticated user will see in a link that will launch a webform, when s/he is in an Islandora collection for which an IW webform has been enabled and is viewing an object of the type for which a webform has been designed.

[image]

* To submit a new webform:
  * Click on the link to submit a caption. A form box will open.

[image]

*  
  * Fill in the fields with your submission text.
  * When finished, click "Submit". You can then “View”, “Edit” or “Delete” you submission on the “Submissions” page.        
* To edit a previously submitted caption:
  * Go to the object you submitted a caption on.
  * Click the "Submissions" link.

[image]

* You cannot edit a previously submitted caption if you see the link “Re-ingest’ (in red font) because that means it has already been approved and ingested into Islandora. Ingested ones cannot be changed. If you decide to edit it anyway, a new Islandora submission object will be created and the original one will remain as well; there is no way you can delete it.
  * Find your submission, which is probably the last one added to the list. If it has not yet been ingested, you can safely edit it.
  * Click "Edit".
    * Make your changes.
  * Click “Save”.

## For Administrators

**6. Islandora Webform installation preliminaries**

* Ensure that all basic Islandora modules and dependencies are installed and working.
* DHI@Hamilton tested the IW module with the latest versions of each of these modules enabled:

[table]

**7. Understanding the _Islandora Simple Text Content Model_**

* The IW module comes bundled with a content model, the “Islandora Simple Text Content Model”. It helps to be aware of how this content model accommodates the values submitted by a webform. Understanding the content model can help you configure the webform components properly. So spend some time examining the content model and the XML metadata form it is associated with.
* The Content Model that is used by the IW module is part of the "Islandora Example Simple Text Solution Pack", which is installed when you install the main Islandora Webform module.
* The code (in Islandora Webform Ingest) supporting this CM grabs a form’s output and creates a Fedora object and plugs in those values in a programmatic way into a MODS datastream which gets crosswalked to DC according to rules you can configure in an XSLT file.
* The IW module “derivatives.inc" creates a MODS datastream (based on the <mods: relatedItem> element from MODS: http://www.loc.gov/standards/mods/userguide/relateditem.html). 
* The code includes the parent object’s PID as the property of an xlink attribute of the <mods:relatedItem> element.
* The code puts the submitted text in the <mods:title> element.
* For other fields you use one of the IW menus to configure how each field in your form gets mapped to MODS (see discussion above).
* The MODS datastream in Fedora (Content: managed, MIME type: text/xml) might look something like this.
```<?xml version="1.0"?>
<mods xmlns="http://www.loc.gov/mods/v3"
xmlns:mods="http://www.loc.gov/mods/v3"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xlink="http://www.w3.org/1999/xlink"
xsi:schemaLocation="http://www.loc.gov/mods/v3
http://www.loc.gov/standards/mods/v3/mods-3-4.xsd">
 <relatedItem type="host" xlink="http://lis.hamilton.edu/islandora/object/islandora%3A1">
    <titleInfo lang="" displayLabel="">
     <title>This photograph was probably taken in Toledo, Ohio.</title>
     <subTitle/>
    </titleInfo>
    <name type="personal">
     <namePart>Peter MacDonald</namePart>
     <namePart type="family">MacDonald</namePart>
     <namePart type="given">Peter</namePart>
    </name>
 </relatedItem>
</mods>```
* It creates a stub of a Dublin Core datastream that might look something like this:
  * DC (inline, text/xml)
```<oai_dc xmlnsdc::oai_dc="http://www.openarchives.org/OAI/2.0/oai_dc/" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.openarchives.org/OAI/2.0/oai_dc/ http://www.openarchives.org/OAI/2.0/oai_dc.xsd">
<dc:title>This photograph was probably taken in Toledo, Ohio</dc:title>
 <dc:contributor>Peter, MacDonald</dc:contributor>
 <dc:identifier>apw:235</dc:identifier>
<dc:date>2016-01-26</dc:date>
 <dc:description>This photograph was probably taken in Toledo, Ohio. </dc:description>
</oai_dc:dc>
```
* The code puts an RDF triple pointing to the PARENT_PID in the RELS-EXT datastream adds.
* RELS-EXT (inline, applications/rdf+xml)
```
<fedora:isAnnotationOf rdf:resource="info:fedora/islandora:1">
</fedora:isAnnotationOf>```
**8. Installing the Islandora Webform module**

* The IW module actually consists of three modules plus a text-based content model. To learn more about each IW module, you should read the README file for each one on the code distribution repo.
* Common Media’s code repo:
  * github.com/commonmedia/islandora_webform.git

**8.1. First of all Install and Configure the Drupal Webform module**
```        > drush dl -y webform
        > drush en -y webform (add @sites for multi-site setups)
        > drush update (add @sites for multi-site setups)```

* Before you can start using webforms in Drupal you should configure it:
Administer > Configuration > [Content Authoring] Webform settings
(or <your_site>/admin/config/content/webform)
* Uncheck any fields you don’t think you’ll need in any of your Webforms. [Or, just leave them all checked.]

[image]

* From address: "dhitech@hamilton.edu" (example only)
* From name: "Digital Humanities Initiative" (example only)
* Default subject: "Form submission from: [node:title]" (example only)
* Click "Save configuration".

**8.2. Download/Install the "Webform AJAX" modules**
```> drush dl -y weborm_ajax
> drush en -y webform_ajax```

**8.3. Download/Install the "Islandora Webform" module (there is more than one way to do this)**

* SSH into the Drupal server.
* Navigate to "sites/all/modules".
* Clone the islandora_webform module:
```> git clone https://github.com/commonmedia/islandora_webform.git```
* If you are just upgrading the IW modules from an earlier version, do the following steps before cloning the new webform:
  * Clear all caches for all sites
  * Disable the IW modules
  * Update the database for your sites. (remove "@sites" if not a multi-site setup)
  ```> drush @sites cc all
> drush @sites dis islandora_webform
> drush @sites dis islandora_webform_ingest
> drush @sites dis islandora_example_single_text
> drush @sites update```
* Back up an customizations that will be overwritten when you upgrade the modules, such as:
```islandora_webform/submodules/islandora_webform_ingest/examples/islandora_example_simple_text_solution_pack/xsl/
modsrelated_to_dc.xsl```

**8.4. Enable the Islandora Webform module for each site that needs it.**

* Shell method: SSH to the server
  * To enable it for the default site, run at sites/all/modules:
```> drush en -y islandora_webform
> drush en -y islandora_webform_ingest```
  * To enable it for all sites in multi-site, run at sites/all/modules:
```> drush @sites en -y islandora_webform
> drush @sites en -y islandora_webform_ingest```
  * To enable it for a specific site:
```> drush en -y islandora_webform --uri=http://<your_site>
> drush en -y islandora_webform_ingest --uri=http://<your_site>```
* Drupal method: Log into a Drupal site
  * Administer > Modules
    * Enable "Islandora Webform" (islandora_webform)
    * Enable "Islandora Webform Ingest" (islandora_webform_ingest)
    * Enable "Islandora example simple text" module (islandora_example_simple_text)
      * This module was installed as a submodule when the main IW module was installed, but you have to enable it manually.
* Update the database
```> drush update (or in the Drupal GUI: "<your_site>/update.php")```
* There are no configuration options for this module.

**8.5. Ensure that all dependencies are enabled**

Administer > Modules

Look for any Required but "missing" or "disabled" dependencies for the modules: Webform, Webform AJAX, Islandora Webform, and Islandora Webform Ingest modules, Islandora Example Simple Text.

8.6 Understanding the structure of the IW modules

Module(s) directory structure (the three modules are italicized here):

sites/all/modules
 |_islandora-webform
               |_README.txt
   |_submodules
     |_islandora_webform_ingest
       |_README.txt
       |_examples
         |_islandora_example_simple_text_solution_pack
                  |_README.md

Content Model
Islandora Simple Text Content Model (islandora:sp_example_text)
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
9. Configuring permissions for the Islandora Webform module

Administer > People > Permissions > Roles

[image]

... add more later
