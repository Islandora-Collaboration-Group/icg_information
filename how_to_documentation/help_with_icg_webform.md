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

`<fedora:isAnnotationOf rdf:resource="info:fedora/islandora:1">
</fedora:isAnnotationOf>`

* (Optional) Examine this new component
* Administer > Content > Webforms (i.e. /admin/content/webform)
* Find the title of your webform > click "Components", and you will see the component "Islandora object PID".
  * Label: "Islandora object PID"
  * Type: "Textfield"
  * Value: -
  * To see more of its fields, click "Edit".
