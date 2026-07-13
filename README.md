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

### On roihu-cpu <br>

To access the module: <br>
`module use /projappl/project_2000881/Modules` <br>


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

## Extracting a subset from a PVTU dataset

Motivation for this: The whole Antarctic mesh is enormous. I wanted a couple of regions that I could extract and download separately for a quicker way of checking sanity of outputs.

This is currently done by a list of partitions. These were selected interactively in Paraview and are specific to the 1020 partition mesh provided by Chen. As they are extracted by partition they are not following catchment boundaries. It is very quick to do: we're basically just taking a copy of the pvtu file and removing some lines from it. So very quick and easy to do.

Currently available regions: <br>
WAIS_PT    (WAIS PIG and Thwaites) <br>
TAM        (Transantartic Mountains; along the edge of the Ross ice shelf)

Example usage: <br> 
`subset_pvtu TAM hotrans_t0001.pvtu`

Optionally you can then run `merge_vtu`.

### Setting up more regions for subsetting

Very roughly: Use partition_centroids to create a dataset of just partition centroids. Overlay this with the full dataset in Paraview for context. Use Find Data and selection tools in combination with spreadsheet view. Save spreadsheet as csv and add it to this repo.

Future options: It would be nice to have a script that divides the dataset up by catchment boundaries. This would be a heavier operation as it would require loading all partitions and accessing also a catchment definition dataset. It should be possible to automate this, but it would require a lot of memory and access to data processing such as the paraview.simple module.

