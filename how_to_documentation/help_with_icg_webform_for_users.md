# How to Use an Islandora Webform - For End Users

##Table of Contents

* 1. How to submit an Islandora Webform
* 2. How to uploading a file

***

**1. How to submit an Islandora Webform**

* When a visitor to the Islandora site views an object whose properties match the properties set by a webform, she will see a link to on the object view page that will launch that webform, but only if the visitor's Drupal user role permits access to the webform.
* The person who set up the webform may have set it up so only authenticated users will have access to it.

***

![webform_12.png](/how_to_documentation/images/webform_12.png)

* Figure 1: Object view page showing a link to the Islandora webform below the object frame.

***

* To use the webform:
  * Click on the link to the webform and a webform box will open for you to fill in.

***

![webform_13.png](/how_to_documentation/images/webform_13.png)

* Figure 2: View of a webform as seem by an end user

***

*  
  * Fill in the fields in accordance with the on-screen instructions.
  * When finished, click "Submit".
* To edit a previously submitted webform:
  * Go to the object you submitted a webform on.
  * Click the "Submissions" link.
  * You can then “View”, “Edit” or “Delete” your submission on the “Submissions” page.

***

![webform_14.png](/how_to_documentation/images/webform_14.png)

Figure: 3: View of what users can see if they want to view, edit or delete their submission.

***

  * Find your submission, which is probably the last one added to the list. If it has not yet been ingested, you can safely edit it.
  * Click "Edit".
    * Make your changes.
  * Click “Save”.
* PLEASE NOTE that you cannot edit a webform that has already been submitted if you see the link “Re-ingest’ (in red font) because that means it has already been approved and ingested into Islandora. Ingested ones cannot be changed. If you decide to edit it anyway, a new Islandora submission object will be created and the original one will remain as well; there is no way you can delete it.

***

**2. How to upload a file**

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
