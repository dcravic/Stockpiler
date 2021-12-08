# Stockpiler
A Foxhole logi companion app for quickly reading and transcribing stockpile contents

Stockpiler aims to simplify tracking the contents of stockpiles by automating the process and exporting a spreadsheet with the stockpile's contents.

Constructive criticism is welcome, but keep in mind **I DO NOT CODE FOR A LIVING**.  Thanks. :)

Current Features:
- Hotkey (F3) to read and transcribe contents of any stockpile/BB/Town Base/etc from the Map.
- App is threaded, so you can initiate a new scan while previous scan(s) are still processing.
- Most items can be read, other than those with missing icons as noted in Missing.csv
- Ability to set a filter to ignore unwanted items
- Toggles to turn on/off faction-specific items and entire categories of items in filter
- Filter can be saved and is automatically loaded at launch
- Choose which exports you want, save this setting and it will load automatically in the future

# To use:
1. Launch Foxhole and Deploy
2. Launch Stockpiler
3. Open your Map
4. Hover your cursor over the Stockpile/Bunker Base/Town Hall/etc you wish to transcribe **on the map**
- Remember you can tab while hovering over a Seaport/Storage Depot where you have multiple private stockpiles
5. Press the **F3** key

If the stockpile is a named stockpile that Stockpiler has never seen before:
- Stockpiler will display an image of the stockpile name and ask you to enter the name
- The stockpile's contents will be exported to ../Stockpiles folder as:
- XLSX (Excel Spreadsheet) of the contents
- CSV TXT file of contents
- Image of the stockpile title
- A copy of the stockpile image grabbed by Stockpiler

If the stockpile is a named stockpile that Stockpile has seen before:
- Stockpiler will overwrite any existing (previous) export of the stockpile contents as:
- XLSX (Excel Spreadsheet) of the contents
- CSV TXT file of contents
- A copy of the stockpile image grabbed by Stockpiler

# Google Spreadsheet export
To export the data to a Google Spreadsheet, Stockpiler is using the library gspread (https://docs.gspread.org/en/latest/index.html). It requires a Google API key (JSON file), which content should be place in the "google_api_key.json" file (do not overwrite the file itself). To do so, please follow these steps:
 - Enable API Access:
 	- Head to Google Developers Console (https://console.developers.google.com/) and create a new project
 	- Once the project is created, click on the button "+ ENABLE APIS AND SERVICES"
 	- Search for "Google Drive API", and enable it. This is to allow access to the spreadsheet.
 	- Search for "Google Sheets API" and enable it. This is to read and write on the spreadsheet.
 - Go to “APIs & Services > Credentials” and choose “Create credentials > Service account key”.
 - Fill out the form
 - Click “Create” and “Done”.
 - Press “Manage service accounts” above Service Accounts.
 - Press on ⋮ near recently created service account and select “Manage keys” and then click on “ADD KEY > Create new key”.
 - Select JSON key type and press “Create”.

The "google_api_key.json" on the project contains 2 custom variables, if erased please add them again:
 - "owner_email": "username@gmail.com",
 - "allow_afterinit_edit": false

"owner_email": allows the user with that email to gain ownership of the spreadsheet during it's first initialization.
"allow_afterinit_edit": To set to 'true' or 'false'. Stockpiler allows to filter items detected. If some items are filter during the creation of the spreadsheet (or later manually deleted), if the filtered item is detected while using Stockpiler, and if set to 'true' a new row will be added for the missing item.  



Stockpiler runs each stockpile "grab" as a separate thread, so you do not have to wait for one to complete before initiating the next


Currently, pressing the F2 key will grab an image of the stockpile/BB/Relic Base contents you are hovering over and save it to the root folder.  If you are willing to help contribute missing items so that Stockpiler can properly tally them, these are the images that are needed.  Please message me on Discord if you're interested in helping get the remaining missing item images added.
My Discord is ruttiger#6198

Special thanks to **Catalinuru** and **AceAstra** for their help testing and hunting down missing icons.

Compiled versions compiled to EXE using Nuitka

Nuitka was a giant pain in the butt to get working the first time around and I honestly don't remember all the steps I took to get it to where I have it now.  If you're able to work your way through that, you can use either compile string below.

Compile string (without console window) is:
python -m nuitka --mingw64 --plugin-enable=tk-inter --plugin-enable=numpy --standalone --windows-disable-console --follow-imports --show-progress Stockpiler.py

Compile string (with console window):
python -m nuitka --mingw64 --plugin-enable=tk-inter --plugin-enable=numpy --standalone --follow-imports --show-progress Stockpiler.py


Code can also be compiled (more easily) with auto-py-to-exe

auto-py-to-exe settings:

Onefile - One Directory

Console Window - Console Based (helpful for troubleshooting, please submit any errors you get as Issues here on GitHub)

Additional Files - Add Folder - add the CheckImages, Stockpiles and UI folders

Additional Files - Add Files - add the Filter.csv and ItemNumbering.csv files

Advanced - collect-all - pynput
