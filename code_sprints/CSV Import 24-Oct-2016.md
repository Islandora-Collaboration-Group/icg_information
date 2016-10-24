Our first ICG CSV Import code sprint was conducted via Go-to-Meeting at 9:00 AM Eastern on 24-Oct-2016.  On the call were Mark McFate (organizer), Peter MacDonald, and Ben Rosner.  The agenda was intended to include:

Sprint Call Structure (2 hour call)
~30 minutes for each of the following topics:
- Briefly discuss the state of the project and identify remaining tasks, and 
- Assign tasks/roles to willing individuals.
- Assist all participants to establish a workflow and environment to build in.
- Q&A, followed by start of collaboration!

Ben had to depart after about 30 minutes so we dedicated significant time to the first topic leaving Mark and Peter to engage in the remaining agenda topics.  Meeting was adjourned at 10:15 AM.

## State of the Project
* Mark presented the latest development in the batch/back-end processing.  The presented changes are documented in [README.md](https://github.com/Islandora-Collaboration-Group/icg_csv_import/blob/master/README.md). 
* Ben presented the latest developmnt in the new UI which currently is housed in [https://github.com/br2490/icg_csv_import_ui](https://github.com/br2490/icg_csv_import_ui). 

## Assignment of Tasks/Roles
* Mark - 
  * Agreed to continue working on the batch processing/back-end and introduced a new [issue](https://github.com/Islandora-Collaboration-Group/icg_csv_import/issues) to address integration of the new UI with the back-end. 
  * Will address new and old issues found in [the issue queue](https://github.com/Islandora-Collaboration-Group/icg_csv_import/issues).
* Peter - 
  * Agreed to develop and conduct tests on the back-end and will introduce new issues with corresponding data files to document progress.
  * Will test/evaluate using oXygen to extract all possible xpaths from existing MODS records.
* Ben -
  * Will continue to refine the new UI and possibly develop the ability to complete an import of data apart from engaging the existing back-end.
  * Look at capturing the user's mapping so that ingest of additional data with the same CSV structure can be accomodated without having to repeat the mapping process or engage the back-end xpath-dependent code.

## Workflow and Environment
Mark is seeking assistance to review, merge and ultimately accept the pending pull requests in the 'csv' branch of [islandora_vagrant](https://github.com/Islandora-Collaboration-Group/islandora_vagrant).  Once that is done he would like to issue additional pull requests from the 'csv' branch at [islandora_vagrant](https://github.com/DigitalGrinnell/islandora_vagrant). 

All developers are encouraged to use the appripriate Issue queues to propose or define work, and to document resolution of issues as they are addressed, with corresponding data files when necessary.

## Summary 
Mark and Peter expressed interest in the UI work that Ben has done, with some reservations.  

The new UI looks good as a means of conveniently mapping CSV data into defined XML metadata form structure, and that mapping should be able to drive the existing batch/back-end processing, AND/OR provide the ability to ingest data directly without engaging the back-end.  However, they are concerned that without the back-end, the 'direct' ingest of data becomes a 'one-off' proposition.  In other words, a user would presumably have to re-map the data each time they want to ingest new objects, and there is no 're-ingest' mechanism for making changes to existing objects.  The workflows at both Grinnell and Hamilton typically involve several iterations, or stages, of ingest.  A small collection of 1000 objects, for example, might be ingested in 10 iterations of 100 objects each.  'Direct' ingest through the UI would conceivably require mapping the same CSV data in an XML form repeatedly, and if the mapping is not done consistently the resulting objects would be inconsistent from each other.  

Mark and Peter would like to see development continue on BOTH of fronts:  
1. Have the UI generate xpaths to drive the batch/back-end processing, and 
2. Have the UI perform a 'direct' or 'one-off' ingest of data.  This could be useful both for small data sets, or as a means of testing ingest before running additional iterations via the back-end processing.

## Next Code Sprint
Mark will issue another Doodle poll soon (target is before the end of October) to continue this process.

