# CSCICEutils
CSC ICEMAP  utilities. 
Some simple scripts to supplement what CSC provides in terms of monitoring and managing disk usage and file count resources. 

## Disk resource monitoring and management

### On mahti <br>

To access the module: <br>
`module use /projappl/project_2002875/modulefiles/` <br>

To load it: <br>
`module load icemap/utils` <br>

Then you have access to the following scripts: <br>
`count_files /path/to/directory` <br>
`disk_usage /path/to/directory` <br>
`count_files_by_type /path/to/directory` <br>
`delete_vtu /path/to/directory` <br>

These are all recursive, i.e. they process all subdirectories. The first two list subdirectories in order of size. The third lists in order of extension frequency (e.g. to check how many .vtu files you have). The last one is not reversible! Use with caution!

### On LUMI <br>

To access the module: <br>
`module use /projappl/project_462001194/modules/` <br>

Loading it is the same as on mahti. The same commands as on mahti are also available on LUMI. Since LUMI quotas cannot be extended, I also added this one on LUMI, to help us keep below the storage limit over time: <br>
`tbhours_forecast `

## Merging vtu files

Can be used in order to keep the file count down. Also makes downloading vtu files for local analysis slightly simpler.

### On mahti <br>
Load the python data module (more up to date version of python than the default version): <br>
`module load python-data` <br>
You may need to locally install the python vtk module (you should need to do this only once): <br>
`pip install --user vtk` <br>
Then go to the directory in which you want to merge your files and run: <br>
`merge_vtu` <br>

Notes: <br>
Uses the python vtk module. <br>
Creates a premerge directory and stores all the original files there. So you can check the merged files worked before you delete the old ones. <br>
Not recursive: only applies to files in current directory. <br>
You can optionally give a pvtu filename as a command line argument, in which case it will only merge vtu files corresponding to the given pvtu file.

### On LUMI <br>
Run `module load cray-python` instead of `module load python-data` <br>
Apart from that it should function the same as on mahti.
