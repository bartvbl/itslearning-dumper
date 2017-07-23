# It's Learning Complete Backup Tool

-- The NTNU It's Learning site has now shut down. You should consider any data you haven't backed up as gone. If you need a head start to dump the It's Learning site for your institution, I recommend you fork this project. --

This script was written to export data from the course management system "It's Learning", as no proper method has been supplied for this previously. 

I'm writing and supporting this program in my spare time. NTNU does not officially support or authorise this project.

## What does it do?

The following elements are downloaded by this script. Note that It's Learning has had an overhaul in terms of visual appearance, but did not migrate older courses to the new visual style. As such these had to be implemented separately, and are as such listed separately.

To my knowledge, this list covers all major features of It's Learning.

1. Internal messaging - Both the "new" and "old" inboxes are supported.
2. Course bulletins - Both "new" and "old" flavours are downloaded. Includes comments on new-style posts. Old-style text/information widgets are also downloaded.
3. Assignments - Includes submissions by you, and if you teach a course, submissions from students. In both cases, grading, feedback and submitted files are downloaded.
4. Notes, Links, and Pictures - Both old-style and new-style. 
5. Files - Any files published as part of the course.
6. Surveys - Downloads all responses, and the It's Learning generated reports.
7. Discussions - Downloads all threads, including most linked images.
8. Online Tests - Download all answers submitted as a student, or all student submissions as a teacher.
9. Projects - All content is dumped, including project bulletin messages.

## Running

The easiest way of running this script is to head over to the [Releases](https://github.com/bartvbl/itslearning-dumper/releases) page and download a pre-packaged executable.

Alternatively, you can follow the steps below. For detailed step-by-step instructions, see the "Beginner's user guide" section below.

1. Install Python 3.4 or above (latest at the time of writing is 3.6). Make sure to check the "add to path" and "install pip" boxes in the installer.
2. Install two python packages using pip by running `pip install lxml requests` on the command line.
3. Run the script and let it do its thing by running `python scrape.py`. It will ask you for your username and password when you start it.

## Configuration

The script has a number of command line parameters available for configuring the script.

For an overview over all available command line paramters, use `python scrape.py --help` or `dumper_windows.exe --help` if using a build.

* `--output-dir`: Determines the location where output files will be written to. Can be a relative path to the location of the script, or an absolute path. On Windows, I cannot recommend enough to place this directory at the **ROOT** of your hard drive (C:\, D:\, etc.), since the 255 character path name limit is easily surpassed. This parameter is mandatory on a system without a graphical interface.
* `--rate-limit-delay`: The number of seconds the script waits after each request. Ensures requests are not sent at a high rate, reducing the load on the It's Learning servers.
* `--skip-to-course`: As mentioned above, crashes may occur. Use this index to force the script to jump to a particular course, potentially hopping over a problematic one. The index is the same as the one printed out in the terminal (1-indexed). Set to 1 to only skip downloading internal messages.
* `--output-text-extension`: Determines the extension output text files have. The specific format of the contents of these is different in most cases, but is in most cases plaintext with fragments of HTML. You might want to change this to `.txt` if preferable.
* `--enable-checkpoints`: Enabling this will create a small text file in the working directory which keeps track of where the script left off. If the download takes too long, you can simply quit the script, and it will allow you to catch up to where you left off (it restarts the element it left off at, which should be close enough).
* `--institution`: Only dump the content of a single institution site. This value should either be `ntnu` or `hist`.
* `--list`: Don't dump anything, just list all courses and projects for each institution, along with their indices, which can be used as a parameter for `--ship-to-course`.
* `--projects-only`: Only dump projects, nothing else.
* `--courses-only`: Only dump courses, nothing else.
* `--messages-only`: Only dump internal messages, nothing else.

## Beginner's User Guide

If you've never touched Python before, here's how to get the script running on Windows:

1. Go to: https://www.python.org/

2. Hover over the "downloads" item in the top bar of the page. A menu with some links pops out, with two "quick links" on the right. One for Python 2.7.13, and one for Python 3.6.1. Click on the Python 3.6.1 link to download it.

3. Run the installer. On the starting page, check "Add Python 3.6 to PATH", and click "Customize installation"

4. Ensure all checkboxes on this page are checked, and click Next. On the next page, click Install. Let the installer run to completion. Click Close when it's done.

5. Download the source code from the GitHub repository I linked using the green "Clone or Download" button, and clicking on "Download ZIP". 

6. Open the downloaded ZIP file, and find the "scrape.py" file in the "itslearning-dumper-master" folder. Extract this file to a folder of your choice.

7. Navigate to the folder which contains the scrape.py file in Explorer

8. Make sure no file in the folder is selected. Hold Shift, and right click on any place in the file window that is not occupied by a file. In the context menu that pops up, there should be an entry that says "Open command window here". A command prompt comes up.

9. In the command prompt window, write:

        pip install -r requirements.txt

    And press enter. This installs two libraries which the script uses.

10. We're now ready to run the script. In the command prompt window, write:

        python scrape.py
        
Upon starting, it will ask you for your username and password. You should use your FEIDE/NTNU credentials for this. Type them into the command prompt window, and press enter. Note that when typing in your password, the characters are hidden.

And hope for the best. The script will print out what it's doing on the command prompt. It will show a message when it's done.

Good luck!

## Known Issues

The following issues are known, and will most likely not be fixed:

* Some images downloaded from places such as discussion forums are saved with filenames such as `showimage.aspx`. I have not built in automatic detection of file types, and some URL's do not provide file name information. You can rename these files to ones with a correct file extension to view them.
* Attachments from unsent/draft messages in the old messaging system are not downloaded. 
* Files linked or attached to forum posts are not downloaded.
* Comments on old-style bulletins are not saved (I have not yet encountered a single course using these).

## Disclaimer

This script may still contain bugs. It's Learning has a number of edge cases, and I simply can't be sure my script has covered all of them. Since I am relying on page structure to extract data, unexpected differences can cause crashes. I've attempted to avoid these as best as I can, and the script has multiple fallback options. Thus far the script has worked successfully for a large group of people. I hope it does for you too, but can't give guarantees it will _actually_ do so, nor can I guarantee it catches all your data. Inspect the produced output to make sure everything you need is there.

## Contributors

### Original author: 

- Bart van Blokland

### Additional contributions by:

- @sklirg Håkon Solbjørg
