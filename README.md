import os
import pathlib
import shutil

fileFormat = {
    "Web": [".html5", ".html", ".htm", ".xhtml"],
    "Picture": [".jpeg", ".jpg", ".tiff", ".gif", ".bmp", ".png", ".bpg", "svg", ".heif", ".psd"],
    "Video": [".avi", ".mkv", ".flv", ".wav", ".mov", ".mp4", "webm", ".vob", ".mng", "at", ".mpg", ".mpeg", ".3gp"],
    "Document": [".oxps", ".epub", "pages", ".docx", ".txt", ".pdf", ".doc", ".fdf", ".ods", ".odt", ".pwi", ".xsn", ".xps", ".dotx", ".doce", ".dox", ".rvg", ".rtf", ".rtfd", ".wpd", ".xls", ".xlsx", ".ppt", "pptx"],
    "Compressed": [".a", ".ar", ".cpio", ".iso", ".tar", ".gz", ".rz", ".7z", ".dmg", ".rar", ".xar", ".zip"],
    "Audio": [".aac", ".aa", ".aac", ".dvf", ".m4a", ".m4b", ".m4p", ".mp3", ".msv", "ogg", "oga", ".raw", ".vox", ".wav", ".wma"],
}

fileTypes = list(fileFormat.keys())
fileFormat = list(fileFormat.values())

source_folder ="C:\\Users\\HP\\Downloads"
base_dest_folder = "Vishal"
if not os.path.exists(base_dest_folder):
    os.makedirs(base_dest_folder)

for file in os.scandir(source_folder):
    if file.is_file():
        filename = pathlib.Path(file.name)
        fileExtension = filename.suffix.lower()

        src = file.path
        dest = base_dest_folder

        if fileExtension == "":
            print(f"{src} has no file format.")
        else:
            moved = False
            for formats in fileFormat:
                if fileExtension in formats:
                    folder_name = fileTypes[fileFormat.index(formats)]
                    category_folder = os.path.join(base_dest_folder, folder_name)

                    if not os.path.exists(category_folder):
                        os.makedirs(category_folder)

                    dest = category_folder
                    moved = True
                    break

            if not moved:
                print(f"{src} could not be categorized into a specific format, staying in {base_dest_folder}.")
        
        print(f"{src} moved to {dest}!")
        shutil.move(src, dest)

print("File organizer completed!")
input("\nPress enter to EXIT")
