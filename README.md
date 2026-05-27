# CSCICEutils
CSC ICEMAP  utilities. 
Some simple scripts to supplement what CSC provides in terms of monitoring and managing disk usage and file count resources. 

## Disk resource monitoring and management

Some simple bash scripts intended to be used on CSC machines to help manage project resources between members.

To access the module on mahti and LUMI respectively: <br>
`module use /projappl/project_2002875/modulefiles/` <br>
`module use /projappl/project_462001194/modules/` <br>

To load it: <br>
`module load icemap/utils` <br>

Then you have access to the following scripts: <br>
`count_files /path/to/directory` <br>
`disk_usage /path/to/directory` <br>
`count_files_by_type /path/to/directory` <br>
`delete_vtu /path/to/directory` <br>

These are all recursive, i.e. they process all subdirectories. The first two list subdirectories in order of size. The third lists in order of extension frequency (e.g. to check how many .vtu files you have). The last one is not reversible! Use with caution!

Since LUMI quotas cannot be extended, I also added this one on LUMI, to help us keep below the storage limit over time: <br>
`tbhours_forecast `

## Merging vtu files

On mahti: <br>
Load the python data module (more up to date version of python than the default version) <br>
`module load python-data` <br>
You may need to locally install the python vtk module (you should need to do this only once) <br>
`pip install --user vtk` <br>
Then go to the directory in which you want to merge your files and run: <br>
`merge_vtu` <br>
Notes: <br>
Creates a premerge directory and stores all the original files there. So you can check the merged files worked before you delete the old ones. <br>
Not recursive: only applies to files in current directory. <br>
Uses the python vtk module.

On LUMI: <br>
not yet available; file system problems...
