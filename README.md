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

## Beginner's User Guide

If you've never touched Python before, here's how to get the script running on Windows:

1. Go to: https://www.python.org/

2. Hover over the "downloads" item in the top bar of the page. A menu with some links pops out, with two "quick links" on the right. One for Python 2.7.13, and one for Python 3.6.1. Click on the Python 3.6.1 link to download it.

3. Run the installer. On the starting page, check "Add Python 3.6 to PATH", and click "Customize installation"

4. Ensure all checkboxes on this page are checked, and click Next. On the next page, click Install. Let the installer run to completion. Click Close when it's done.

5. Download the source code from the GitHub repository I linked using the green "Clone or Download" button, and clicking on "Download ZIP". 

6. Open the downloaded ZIP file, and find the "scrape.py" file in the "itslearning-dumper-master" folder. Extract this file to a folder of your choice.

7. (Optional) Open up the scrape.py file in a text editor (not Word, something like Notepad or Notepad++). We'll have to make a few edits before we can get started.

8. (Optional) Find the line in the scrape.py file saying:

        output_folder_name = 'dump/'

9. (Optional) If you look in Computer, it shows the available hard drives. Windows always has a drive named "C", but there may be others too. If so, find one which has a decent amount of space available (some GB worth at least). Pick a drive and note its drive letter. This should preferably be a drive that is not "C" and has available space as I mentioned previously, but if you don't have anything else, fall back on to "C".

10. (Optional) Change the line mentioned in step 10 to the line shown below, where you replace "{drive letter}" with the drive letter you picked. 

        output_folder_name = '{drive letter}:/dump/'

    For example, if you picked the "D" drive, you'd end up with this:

        output_folder_name = 'D:/dump/'

11. (Optional) Save the file. Close the editor.

12. Navigate to the folder which contains the scrape.py file in Explorer

13. Make sure no file in the folder is selected. Hold Shift, and right click on any place in the file window that is not occupied by a file. In the context menu that pops up, there should be an entry that says "Open command window here". A command prompt comes up.

14. In the command prompt window, write:

        pip install requests lxml

    And press enter. This installs two libraries which the script uses.

15. We're now ready to run the script. In the command prompt window, write:

        python scrape.py
        
Upon starting, it will ask you for your username and password. You should use your FEIDE/NTNU credentials for this. Type them into the command prompt window, and press enter. Note that when typing in your password, the characters are hidden.

And hope for the best. The script will print out what it's doing on the command prompt. It will show a message when it's done.

Good luck!

## Known Issues

The following issues are known, and will most likely not be fixed:

* Some images downloaded from places such as discussion forums are saved with filenames such as `showimage.aspx`. I have not built in automatic detection of file types, and some URL's do not provide file name information. 
* Attachments from unsent/draft messages in the old messaging system are not downloaded. 
* Comments on old-style bulletins are not saved.
