# Use of the Islandora Webform in DHi (Hamilton College)
(by Peter MacDonald, 2017-02-10b)

The following is a general overview of what the IW module is capable of and how it is used for transcribing essays on the American Prison Writers Archive [http://apw.dhinitiative.org].

## What is the ICG Webform module?

  * The ICG "Islandora Webform Module" (IW) is a Drupal module developed by Common Media to add connectivity to an Islandora/Fedora repository.
  * The IW module is based on the Webform module that is compatible with Drupal 7.
  
## Generality

  * The IW module works on any recent version of Islandora 7x repository.
  * The IW module has no limitations on what kinds of repository objects it will work with. We use it with PDF objects, but theoretically it should work with other content type such as images, audio, video, manuscripts, and books with some adjustments in the theming layer, which may be required because Islandora displays different types of objects with different DOM structures.

## Extensibility

  * Because the IW module is built on the Drupal Webform module, it inherits all of the latter's functionality. The full functionality can be learned from online documentation and tutorials [see "Documentation" section below].

## Ease of Use

  * Although help in using the Drupal Webform module's many features is readily available, creators of webforms are wise to keep their webforms as simple as possible in order to reduce set up time and keep troubleshooting to a minimum.
  * Managers can probably get all they need to know about setting up webforms using the Islandora-specific features of the IW module from our ICG documentation, but our documentation only scratches the surface of the full capabilities of the Drupal Webform module itself.
  * Ease of use is ultimately dependent on the complexity of the webform being designed and the level of local familiarity with Islandora and Fedora.
  * A working knowledge of MODS, XML Forms, XSLT, and the Fedora object architecture is pretty much required to handle the configuration of the IW module.
  * Troubleshooting the many moving parts of an IW webform can be time consuming.
  
## Hamilton's Use Case: Transcriptions

* The IW module is installed on Hamilton's Islandora server and a webform has been configured for DHi's American Prison Writers Archive (APWA) site to help gather transcriptions of essays from visitors to the site.

### The "Transcription Tool" (TT)

  * DHi used the IW module to create a webform we call the "Transcription Tool".
  * The TT consists of five fields:
    * __Credit__ - Text that tells the submitter to add their name and date at the end of the transcription if they want credit for being the transciber.
    * __Transcription__ - The place where the submitter puts the transcription they are submitting.
    * __Instructions__ - Text that points the user to instructions on how to transcribe the essay.
    * __User Account__ - A system-generated field holding the submitter's Drupal account ID.
    * __Date__ - A system-generated field holding the current date. [required or automatic? pjm]
    * __Islandora object PID__ - A system-generated field holding the PID (Fedora ID) of the object being transcribed.
  * The webform can be modified by only Drupal Administrators (can be changed locally).

### TT User Accounts

  * Doran submits names with email addresses to Peter (an administrator), who then creates Drupal accounts for them and associates that account with the "Submitters" role.
  * The TT uses three user roles:
    * __Submitters__ - These are users whom Doran has authorized to use the Transcription Tool.
    * __Managers__ - These are users authorized to review submissions. They can view, edit and delete anyone's transcription and eventually ingest them into Islandora. However, managers cannot create or modify the webforms themselves.
    * __Administrators__ - Administrators can do everything submitters and managers can do and in addition can create, edit, and delete the webforms themselves.

## Privacy

  * Submitters are instructed in the webform to add their name at the end of the transcription if they want public recognition of their efforts. Otherwise, we do not permanently associate their name or user account with the transcription.

### TT Access

  * We have configured the Transcription Tool to show a link under the essay when that essay is one that is elligible to be transcribed.
  * That link will be displayed only to users who are logged in with an account associated with one of the IW role authorized to submit transcriptions.
  * Anonymous visitors to the APWA website cannot actually submit a transcription without first contacting Doran, but they can experiment with a "demo" Transcription Tool.
  * Anonymous users can submit a transcription by sending the transcription and the Essay Identifier directly to Doran, who may approve it and forward it Peter for ingest into Islandora.

### TT Workflow

  * Any visitor to the APWA website can search for essays that need transcribing.
  * If the user is authorized to submit webforms and is logged in, s/he will see a link below the essay that will launch the TT webform when clicked.
  * The user then fills in the form and when done, clicks "Submit". If more time is needed to finish the transcription, the user can click "Save Draft" and return later to finish it.
  * If a submitter wants to re-edit one of his/her transcriptions, s/he has to navigate to the essay they transcribed and click the link "Submissions" on that page.
  * The submission then goes into a temporary holding area waiting for a manager to approve it.
  * When a transcription has been submitted, a manager is notified by email that a new transcription is waiting to be approved. S/he can then navigate to the holding area and view, edit, delete, or ingest the transcription. Once ingested, the submission should be deleted from the holding area.
  * Once ingested, the transcription gets written to a "TRANSCRIPT_WF" datastream in the associated Islandora Object.[1]
  * Visitors to the essay will then see a "View transcription" link above the essay which will open a page showing the transcription.

## Webform Features not yet implemented
 
  * The IW module, like any Drupal webform, can be configured to allow visitors to upload files, but we have not yet implemented that in the Transcription Tool.[1]

## Sustainability

  * Because the IW module is based on the Drupal 7 Webform module, any webforms built using the IW will no longer work in Drupal 8. A new Drupal Webform module is being developed for D8, but there is no certainty that the IW module will be upgraded to be compatible with D8.

## Documentation

  * [https://www.drupal.org/documentation/modules/webform/faq] (Drupal Webform FAQ
  * [https://www.drupal.org/node/2834425] (Drupal Webform Tutorials)
  * [https://www.drupal.org/node/2834432] (Drupal Webform Code Snippets)
  * [https://www.drupal.org/node/2834436] (Drupal Webform Theming)
  * [https://www.drupal.org/node/1526208] (Drupal Webform Related Projects)
 
## NOTES

[1] I think this is something we should look into, but it might have significant workload issues regarding handling the uploads.  
