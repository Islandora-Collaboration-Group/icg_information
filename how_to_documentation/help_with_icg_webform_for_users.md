# How to Use an Islandora Webform - For End Users

##Table of Contents

* 1. How to submit data using an Islandora Webform
* 2. How to update date previously submitted using an Islandora Webform
* 3. How to uploading a file using an Islandora Webform

***

##1. How to submit data using an Islandora Webform

* The person who sets up a webform is required to specify under what conditions the webform may be used.
* When you visit an Islandora repository, you will be able to use that webform only if these conditions are met, e.g.
  * The object you are viewing must have properties that match the properties set by a webfor
    * it must be a PDF file if the webform only works for PDF objects or image object.
    * It might have to be inside a specific collection of objects.
  * You might not have permission to use the webform, e.g.
    * anonymous users are often prohibited from using a webform (request an account on the website if you need to).
  * If you do see a link to a webform, then feel free to use it.

***

![webform_12.png](/how_to_documentation/images/webform_12.png)

* Figure 1: An Islandora objectpage showing a link to the Islandora webform at the bottom of the window.

***

* To use the webform:
  * Click on the link to the webform and a webform box will open for you to fill in.

***

![webform_13.png](/how_to_documentation/images/webform_13.png)

* Figure 2: View of a webform as seen by an end user

***

*  
  * Fill in the fields in accordance with the on-screen instructions.
  * When finished, click "Submit".
  
##2. How to update a previously submitted using an Islandora Webform

* Go to the object page you submitted a webform on.
* Click the "Submissions" link on that page (if you see one).

***

![webform_14.png](/how_to_documentation/images/webform_14.png)

Figure: 3: View of what users can see if they want to view, edit or delete their submission.

***

* You can then “View”, “Edit” or “Delete” your submission on the “Submissions” page.
* Find your submission, which is probably the last one added to the list. If it has not yet been ingested, you can safely edit it.
* Click "Edit".
  * Make your changes.
* Click “Save”.

* PLEASE NOTE that you cannot edit a webform that has already been submitted if you see the link “Re-ingest’ (in red font) because that means it has already been approved and ingested into Islandora. Ingested ones cannot be changed. If you decide to edit it anyway, a new Islandora submission object will be created and the original one will remain as well; there is no way you can delete the old one.

***

##3How to upload a file using a webform

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
