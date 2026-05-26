# CSCICEutils
ICEMAP CSC utils

Some simple bash scripts intended to be used on CSC machines to help manage project resources between members.

To access the module on mahti and LUMI respectively: <br>
module use /projappl/project_2002875/modulefiles/ <br>
module use /projappl/project_462001194/modules/ <br>

Then load it and use it to count files and disk usage by directory: <br>
module load icemap/utils <br>
count_files /path/to/directory <br>
disk_usage /path/to/directory <br>
count_files_by_type /path/to/directory <br>
delete_vtu /path/to/directory <br>

The first two list subdirectories in order of size. The third lists in order of extension frequency (e.g. to check how many .vtu files you have). The last one is not reversible! Use with caution!

Since LUMI quotas cannot be extended, I also added this one on LUMI, to help us keep below the storage limit over time: <br>
tbhours_forecast 

