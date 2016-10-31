Our second ICG CSV Import code sprint was conducted via Go-to-Meeting at 9:00 AM Eastern on 31-Oct-2016. On the call were Mark McFate (organizer), Peter MacDonald, Arianna Schlegel, and Joanna DiPasquale. The agenda was similar to our first code sprint (see https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/code_sprints/CSV%20Import%2024-Oct-2016.md).
Meeting was adjourned at 9:42 AM Eastern. 

## State of the Project

Mark briefly updated all on back-end code progress which involved the introduction of a new icg_csv_import_mods-to-dc variable and subsequent MODS-to-DC transformation.  Patrick Dunleavy had commented last week that this was missing from the back-end process and Mark introduced an issue and code to resolve it.  The presented changes are documented in the latest README.md.

## Assignment of Tasks/Roles

* Mark -
  * Agreed to continue working on the batch processing/back-end issues as they come up, and will be conducting testing this week in perparation for DLF where he and Joanna will try to meet and discuss the project as well.  
* Peter -
  * Will continue developing and conducting tests on the back-end and will introduce new issues with corresponding data files to document progress.
  * Previously engaged oXygen as a tool to help with xpath preparation based on existing MODS records.
* Arianna and Joanna -
  * Will work together to develop and conduct tests as opportunities become available.

## Workflow and Environment
Mark is seeking assistance to review, merge and ultimately accept the pending pull requests in the 'csv' branch of [islandora_vagrant](https://github.com/Islandora-Collaboration-Group/islandora_vagrant).  Once that is done he would like to issue additional pull requests from the 'csv' branch at [islandora_vagrant](https://github.com/DigitalGrinnell/islandora_vagrant). 

## Summary
This was a brief meeting largely intended to bring those who could not attend last week up-to-speed.  See comments in the tasks/roles section for more details.  

## Next Code Sprint
Mark will issue another Doodle poll soon for a mid-November sprint to continue this process.
