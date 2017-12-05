# ICG Hack/Doc @ Williams College (Williamstown, MA)

## Date

May 23-24, 2017

## Agenda

1. Business from [last meeting](https://github.com/Islandora-Collaboration-Group/icg_information/blob/master/hack_docs/meetings/02_Wesleyan_2016.md)
1. Round table updates
  * Report from Islandoracon (hack/doc, ISLE, CLAW, metadata, Migration IG)
1. Hack/Doc Topics:
  * Islandora Multi-Importer (Lead: Mark McFate)
  * Metadata search and replace tool (Lead: Martha Tenney)
  * lunchtime discussion: Simple Exhibit display (Lead: Francesca Livermore)

## Attendees

1. David Keiser-Clark (Williams)
1. Francesca Livermore (Wesleyan)
1. Peter MacDonald (Hamilton)
1. Mark McFate (Grinnell)
1. Helena Warburg (Williams)
1. Lisa Conathan (Williams)
1. Martha Tenney (Barnard)
1. Jessika Drmacich (Williams)
1. Karen Gorss Benko (Williams)
1. Jonathan Leamon (Williams)
1. Steve Young (Hamilton)
1. Christine  Menard (Williams)
1. Noah Smith (Common Media)
1. Pat Dunlavey (Common Media)
1. Gavin Morris (Common Media)
1. Cheryl Handsaker (Williams)

## Next meeting

March 12-13, 2018: "ISLE Hack/Doc (by ICG)" @ METRO (New York, NY)

## Schedule

### Tuesday, May 23 (Location: Sawyer Library, Room 328)

* 8:30am Breakfast (wifi/eduroam and setup help available)
* 9:00-9:15am Housekeeping and Announcements
  * Community note taking
  * Report from Islandoracon (hack/doc, ISLE, CLAW, metadata, Migration IG)
* 9:15-9:30am Ice breaker question: “Name, Institution, General experience with Islandora, Hopes and fears”
* 9:30-10:15am Skillshare on:
  * markdown (Gavin Morris)
  * git + TWIG (Pat Dunlavey)
* 10:15-10:30am Break
* 10:30am Hack/doc begins (overview first)
  * Islandora Multi-Importer (Lead: Mark McFate)
  * Metadata search and replace tool (Lead: Martha Tenney)
  * lunchtime discussion: Simple Exhibit display (Lead: Francesca Livermore)
* 10:45-12:15am Subgroups: Code / Doc Starts
* 12:15-1:00pm Lunch
* 1:00-3pm Coding, documentation, preliminary testing
* 3-3:15pm Bio Break (coffee will be available)
* 3:15-4pm Coding, documentation, preliminary testing
* 4-5pm Preliminary reporting, discussion about what is going right and what isn’t working
* 5:30pm Dinner reservation at the Log’s “Black room”. Williams will pay for all ICG attendees dinners and a drink.

### Wednesday, May 24 (Location: Sawyer Library, Room 328)

* 8:30am Breakfast
* 9:00-10:30am Coding, documentation, testing
* 10:30-10:35am Break
* 10:35am- 12pm Coding, documentation, testing
* 12-1pm Lunch
* 1-3pm Informal presentations on the work accomplished so far, + reflection, what went right and what we could have done better
* 3-3:15pm Break
* 3:15-4:30pm Wrap-up
  * Reflection on what has been accomplished
  * Goal setting for what comes next (i.e. follow-up code sprints)
* Exit


# Notes from the event

## Day 1: Welcome! (May 23, 2017)

### Starting off
* DLF proposal from Martha at Barnard- Panel w/unifying theme is Islandora
* IslandoraCon recap - strong content, good ICG presence, Migration interest group being spun up, extended discussion of metadata migration from Fedora 3 → 4; EOL for current Islandora versions
* Might be worth upgrading membership to have seat on Foundation Board and Roadmap committee, large jump in membership dues ($10k instead of $4k) but might be worth it; could also commit more time to Islandora metadata and migration Interest Groups (IG’s)
* METRO (metropolitan library council of ny) offered to host an ICG hack/doc, provide food + unlimited coffee, and possibly participate
* Colgate, Middlebury, Berklee School of Music, and UCONN have shown interest in collaborating with us

### Introductions, hopes and fears
* Jonathan coined (?) “Islandorian Gray”
* Also, Islandora the Explorer

### Markdown skillshare (thanks Gavin!)
* ["Documentation - Markdown Information"](https://docs.google.com/document/d/1_3-kpKWKWM5ti_dsuTFiBttFBC-s8ga8oqa3qyJ8Qo0/edit)

### Github skillshare (thanks Pat!)

### Islandora Multi-Importer (IMI)
* Lead: Mark McFate
* Goals: Discovery, Document Installation, Configuration and Use
* Diego Pino has asked for written installation documentation that would become available on the public github site
* Pat demonstrated how to use it

# Day 2: Welcome! (May 24, 2017)

### Metadata search and replace tool
* Lead: Martha Tenney
* Goals: Discovery, Document Installation, Configuration and Use
* Discussion about different approaches to the find and replace
  * Elected to enhance existing islandora_find_replace
    * Forked the most recent version of the module: Contacting the developer to confirm primary repository
    * Moved existing issues to the new repository
    * Added new issues identified at the hackdoc

### Islandora Multi-Importer (IMI)
* Creating sample data sets for use with IMI and uploaded to our github branch (for a later pull request on Diego’s core [islandora_multi_importer (IMI) github](https://github.com/mnylc/islandora_multi_importer)

## Action items and updates post-hack/doc

### IMI
* Diego has assigned Mark to work on some of the bug fixes. Mark will create a pull request for his coding changes independently of the ICG group work.
* ICG is working on a documentation pull request that we plan to create for Diego by the end of next week (6/2). Included in this pull request will be:
* Updated README.md (Peter et. al will read through and suggest edits, Francesca edits)
* Updated User_Documentation.md (Francesca, Jessika, Martha, et. al will read through and suggest edits, Karen edits)
* Updated Samples folder (and corresponding removal or update of Templates folder) (David owns)
* Once we are happy with all edits, we will merge branch Installdoc to Master and then issue pull request to Diego’s canonical repo
* We are also storing a more robust installation document on gdrive for ICG folks. Currently lives in the Williams hack/doc folder, under the IMI folder. Probably needs a better home! Maybe in our scripts repo?

### Find and Replace
* Forked the cuhk version of the repo which was a little bit updated from the original
* Started to update documentation
* Created a big issues queue (incl. copying issues over form MitchMac’s version and confirming that these issues are still relevant)
* MitchMac emailed MT to say that he won’t be updating this repo in the forseeable future and thinks we should fork it (we already have)
* We will ask MitchMac to accept a pull request that points folks to our version of the repo
* We will add documentation to our repo explaining what changes we’ve made and asking folks to submit issues to the queue if they’ve got any
* We assume that the current license explains that ppl should use the module at their own risk
* Future hack/doc to actually fix some of the issues!

### Scripts Repo
* We are thinking about a creating a repo for sharing our scripts.
* At this point the thinking is that this repo will basically point out to ppl’s scripts on their own repos maybe with some description of what the script accomplishes.
* No work done on this scripts repo yet.
