# It's Learning dump script

This script was written to export data from the course management system "It's Learning", as no proper method has been supplied for this previously. 

*NOTE:* This script may still contain bugs. It's Learning has a number of edge cases, and I simply can't be sure my script has covered all of them. Since I am relying on page structure to extract data, unexpected differences can cause crashes. This script has been a quick-and-dirty approach, which did the job for me and some other people. I hope it does for you too, but can't give guarantees it will _actually_ do so, nor can I guarantee it catches all your data. Inspect the produced output to make sure everything you need is there.

## What does it do?

The following elements are downloaded by this script. Note that It's Learning has had an overhaul in terms of visual appearance, but did not migrate older courses to the new visual style. As such these had to be implemented separately, and are as such listed separately.

1. Internal messaging - Both the "new" and "old" inboxes are supported.
2. Course bulletins - Both "new" and "old" flavours are downloaded. Includes comments on new-style posts. Old-style text/information widgets are also downloaded.
3. Assignments - Includes submissions by you, and if you teach a course, submissions from students. In both cases, grading, feedback and submitted files are downloaded.
4. Notes, Links, and Pictures - Both old-style and new-style. 
5. Files - Any files published as part of the course.
6. Surveys - Downloads all responses, and the It's Learning generated reports.
7. Discussions - Downloads all threads, including most linked images.

## Running

1. Install Python 3.4 or above (latest at the time of writing is 3.6). Make sure to check the "add to path" and "install pip" boxes in the installer.
2. Install two python packages using pip by running `pip install lxml requests` on the command line.
3. Run the script and let it do its thing by running `python scrape.py`. It will ask you for your username and password when you start it.

You might need to change your It's Learning language to English. Unfortunately I had to rely on written text in places, and those depend on the language setting.

## Configuration

The script contains a section near the top devoted to special settings variables. Some variables of particular interest:

* `skip_to_course_with_index`: As mentioned above, crashes may occur. Use this index to force the script to jump to a particular course, potentially hopping over a problematic one. The index is the same as the one printed out in the terminal (1-indexed).
* `output_folder_name`: Determines the location where output files will be written to. Can be a relative path to the location of the script, or an absolute path. On Windows, I cannot recommend enough to place this directory at the **ROOT** of your hard drive (C:\, D:\, etc.), since the 255 character path name limit is easily surpassed. 
* `output_text_extension`: Determines the extension output text files have. The specific format of the contents of these is different in most cases, but is in most cases plaintext with fragments of HTML. You might want to change this to `.txt` if preferable.
* `enable_checkpoints`: Enabling this will create a small text file which keeps track of where the script left off. If the download takes too long, you can simply quit the script, and it will allow you to catch up to where you left off (it does not catch up to the exact point, but close enough).

## Known Issues

The following issues are known, and will most likely not be fixed:

* Some images downloaded from places such as discussion forums are saved with filenames such as `showimage.aspx`. I have not built in automatic detection of file types, and some URL's do not provide file name information. 
* Attachments from unsent/draft messages in the old messaging system are not downloaded. 
* Comments on old-style bulletins are not saved.
