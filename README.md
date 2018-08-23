# ColabModules
Useful Python modules for Google Colab

File List
1. gdrive_io.py   *learn how to add button to skip down

Information
1.  gdrive_io.py: 
    Module with functions to simplify reading/writing to files in Google Drive from Google Colab. Based on PyDrive. 

    Note: Only tested for .txt files and uses string methods; some functions may not work for files in other formats.

Available functions:

    Write(filename, text, [overwrite (default=True)], [trash (default=False)], [replace])
      - Creates a new file or overwrites existing file contents
      - Using overwrite=False will create a new file with iterated filename instead of overwriting if file exists
      - Using trash=True will put a copy of the original in the trash before overwriting
      - Using replace='existing_str' will write 'text' over 'existing_str' instead of overwriting all file contents
      - Returns file ID
    
    NewOnly(filename, text)
      - Equivalent to Write(filename, text, overwrite=False)
    
    WriteNewFile(filename, text)
      - Creates new files without checking if filename exists in Drive. This is the default Drive behavior.
      - Will create files with duplicate names, differentiated only by ID
      - Returns file ID
    
    NonDupName(filename)
      - Adds iterand onto filename base (filename1.txt, filename2.txt, etc) until doesn't match an existing filename in Drive
      - Returns unique filename
    
    GetID(filename)
      - Returns file ID from filename. Does not check for uniqueness.
    
    DeleteFile(id, [trash (default=True)]
      - Deletes file by file ID. trash=True leaves a copy in the trash; trash=False permanently deletes file.
    
    OpenFile(id)
      - Opens file by ID and returns content
      
    FileContents(filename)
      - Opens file by name and returns content
    
    DriveFileDict()
      - Returns dictionary of all files in Google Drive in format {'title':id)
      - Includes files and folders in main drive; files inside folders are not available
    
Install Instructions:

    1) Upload gdrive_io.py to main Drive
    2) Right click & copy the ID from "Get shareable link"
    3) Add the following to project file:
      #! pip install pydrive (un-comment if need to install)
      from pydrive.auth import GoogleAuth
      from pydrive.drive import GoogleDrive
      from google.colab import auth
      from oauth2client.client import GoogleCredentials

      auth.authenticate_user()
      gauth = GoogleAuth()
      gauth.credentials = GoogleCredentials.get_application_default()
      drive = GoogleDrive(gauth)

      module_gdrive_id = 'paste_copied_id_here'  # just the part after 'https://drive.google.com/open?id='
      gdrive_io = drive.CreateFile({'id':module_gdrive_id})
      gdrive_io.GetContentFile('gdrive_io.py')
      import gdrive_io as gd
      
 
