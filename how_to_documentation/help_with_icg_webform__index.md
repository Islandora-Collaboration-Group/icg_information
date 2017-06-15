# The Islandora Webform module

## Index

1. [How to Install the Islandora Webform module](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/how_to_documentation/help_with_icg_webform_installation.md)
2. [Summary of Steps for Creating an Islandora Webform](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/how_to_documentation/help_with_icg_webform_steps.md)
3. [How to Create a Webform using the Islandora Webform Module](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/how_to_documentation/help_with_icg_webform_creation.md)
4. [How to Use an Islandora Webform - For End Users](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/how_to_documentation/help_with_icg_webform_for_users.md)
5. [Islandora Webform for Transcriptions: DHi@Hamilton College Use Case](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/how_to_documentation/help_with_icg_webform_transcriptions.md)

## Description

* The Islandora Webform (IW) module uses the capabilities of the standard Drupal Webform module to enable users to submit comments (captions, tags, transcriptions, etc.) on digital objects in an Islandora repository.
* In Islandora, a link to the webform appears on the page of qualifying repository objects. When clicked by an authorized visitor, the link launches the webform that gathers data from the user and puts the submitted data into a queue waiting for approval by a webform manager.
* When the submission is approved, the form values are ingested either 1) into the MODS (or another specific datastream) of the Fedora object being commented on, or 2) into a completely new Fedora object. If 2) is used, a relationship statement is placed in the RELS-EXT datastream connecting the submission Fedora object to the original Fedora object.
* All the submissions for a specific object can then be displayed along with the original object using a dedicated Drupal block.

## Credits

* The Islandora Webform module was conceived by the Islandora Collaboration Group (ICG)
  * https://github.com/Islandora-Collaboration-Group
* The module development was coordinated by the Digital Humanities Initiative (DHi) at Hamilton College (http://dhinitiative.org/) and supported by funds from an Andrew W. Mellon Foundation grant to DHi.
* The development was performed by Common Media (Patrick Dunlavey, developer)
  * http://commonmedia.com
* Beta testing was first performed by the DHi Collection Development Team and reviewed by other members of the ICG.
