We store project files on both the GitHub repo and a Dropbox folder. 

There is one important principle: all files on GitHub and Dropbox must ultimately be either completed (clean, documented, and checked into the system ready for others to use them) or abandoned (all files deleted), but never left indefinitely in a half-finished state. For storing intermediate work and personal files, you could set up a separate Dropbox folder called ProjectName-Personal.

GitHub and Dropbox have different features, which determine which file types we store on them. GitHub cannot store large files, but it keeps complete version histories and makes it easy to roll back to previous versions. Dropbox can store large files, but it may keep incomplete version histories (depending on your Dropbox account) and makes it difficult to comprehensively roll back to previous versions. We thus store all code and final output files on GitHub, while we store large data files and various other project files (e.g., literature and notes), on Dropbox.

### GitHub repository
The GitHub repo has two main folders: code and exhibits. 
* /code contains master.do, and pathnames.do. master.do should run the entire project, including data cleaning, exhibit creation and compilation.
* /code/cleaning contains all data prep code.
* /code/Analysis contains all code to construct tables and figures.
* /code/ado contains project-specific ado files.
* /exhibits contains a .tex file of the currently relevant exhibits, and the compiled pdf (do not save the extra latex files like .aux to Github).

* /exhibits contains /tab and /fig subfolders with tables and figures. Each can contain subfolders by theme (e.g., placebo for placebo checks).

The repo may also include a notes folder for plain text notes that we would like to be versioned.

GitHub likes to keep total storage low, and will not allow users to push files larger than 100MB. If for some reason a code or output file is larger than about 10 MB, then we should store it on Dropbox.

There are two ways of storing something on GitHub: regularly within the repo and in git-lfs ([download git-lfs](https://git-lfs.github.com/) and see [additional info](https://github.com/blog/2079-managing-large-files-with-git-lfs), including GitHub desktop implementation).

The following types of files are the only files that can be stored regularly in the GitHub repository:
* Diffable files (.txt, .csv, .do, etc.) that are under 10 MB.

The following files can be stored in git-lfs:
* Files that are not diffable (binaries, such as: .pdf, .dta, .rds, .ppt, etc.) but are under 10MB (or darn close...)
* Diffable files that are over 10 MB.
All non-diffable files should be added to the git-lfs tracking (e.g., `git lfs track *.pdf`). This will cause git to automatically place these files within git-lfs. Large diffable files should be added to lfs manually (e.g., `git lfs track output/data/somebigfile.txt`).

### Dropbox
Dropbox stores all data files as well as other project documents.
* ~/ProjectName/Data/Raw stores all original data files that are used in the analysis. 
  * The only manipulations that we will generally make within the /Data/Raw folder are: (1) unzipping; and (2) importing into formats readable by Stata, R, etc. When such manipulations are necessary, we should use the following subfolder structure
  * The output from any further manipulations of data should go into dropbox/ProjectName/IntermediateData.
  * All folders containing raw data should have a plain text README file that details the data source and any additional information that is necessary for replication.
* ~/ProjectName/Data/Intermediate stores all intermediate data files, i.e. files created by the code in the GitHub Code folder 
* ~/ProjectName/Data/Clean stores all data files used to create exhibits.
* ~/ProjectName/Admin stores time sheets, data use agreements, etc.
* ~/ProjectName/Literature stores all relevant literature, typically in pdf format. Please use the following format to name files: Authors_ShortTitle_Year.pdf, and when useful arrange in subfolders.
* ~/ProjectName/Notes stores any comments or notes that we want to share between each other that are too long or complicated for a post on slack (e.g. a latex file and associated pdf that works through a proof). Very long notes in plain text format (e.g., long latex proofs) could be done in a Notes folder within the Github repo.

### Code structure
In general, the code in code/cleaning will operate on data from Data/Raw and place it in Data/Intermediate while constructing final data, which will be placed in Data/Clean. Then code in code/analysis/ will take data from Data/Clean and construct figures and tables to be placed in /exhibits. We also want to be able to trace dependencies and keep the folders clean of unused files. Thus, to the extent that is reasonable, the cleaning code, analysis code, and data folders should have parallel structures. For example, data/raw and data/intermediate might both have a subfolder called censusData. Code in code/cleaning/censusData would clean the raw census data in data/raw/censusData and place it in data/intermediate/censusData.



