#Summary of Steps for Creating an Islandora Webform
(updated 2015-09-09, pjm)

This Summary of Steps skips giving you the actual values to put in the settings -- it just says which settings I use for webform for DHi at Hamilton. YMMV. For full details see the page Islandora Webform module. (Peter)

##1. Create the New Webform
  * Content > Add content > Webform
    * Fill out "Create Webform" page
      * Title, Publishing options
    * Save
##2. Add Components
  * Content > Webforms > find your webform > Components
    * Create components: Label, Type, Required
    * Add
    * Fill in "Edit component" page
      * Description: (optional, I leave it blank)
      * Display: Placeholder (used sometimes), Disabled (used sometimes)
      * Save Component
    * Repeat until all your components are created.
    * Save (again)
##3. Configure Islandora Settings
  * Content > Webforms > find your webform > Components > Islandora settings
    * Islandora Options: Enable, Content model filter, Collection filter, PID search string, Add a link to..., Link text, Link help text
    * Islandora Ingest: Enabled, Ingest destination, Relationship to current object, Namespace of new object
    * Save configuration
##4. Configure Ingest Mapping for each Component
  * Content > Webforms > find your webform > Components
    * Select a component > Edit
      * Islandora Ingest Mapping: Ingest?, DataStream, Field
      * Save component
##5. Configure Confirmation Page
  * Content > Webforms > find your webform > Components > Form settings
    * Submission Settings: Confirmation message, Text format, No redirect
    * Inline Islandora Webform: AJAX
    * Submission Access: [select roles]
    * Save configuration
