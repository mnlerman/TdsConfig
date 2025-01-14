This directory contains the pqact files needed to serve data from the IDD.

Because the TDS currently relies on the perl-decoders to handel observational
data coming across the IDD, the necessary perl decoder scripts, cdl files,
and table files are included in this repository.

For perl decoders to work properly, need to install netCDF-4.0.1, and make a symlink to
ncgen in the ldm ~/util directory. w00t. This repo assume netCDF-4.0.1 is installed to
/opt/netcdf-for-perl, which is the situation on the new motherlode machine

Some files in this directory should be symlinked to the LDM etc/ directory.
Unidata has the following directory layout:

-----------------------------------------
- symlinks in the LDM etc/TDS directory -
-----------------------------------------

* make symlinks to the pqacts files, for example:
    <LDM_HOME>/etc/TDS/pqact.forecastModels -> <TDS_CONTENT_ROOT>/thredds/pqacts/pqact.forecastModels
    <LDM_HOME>/etc/TDS/pqact.forecastProdsAndAna -> <TDS_CONTENT_ROOT>/thredds/pqacts/pqact.forecastProdsAndAna
    <LDM_HOME>/etc/TDS/pqact.obsData -> <TDS_CONTENT_ROOT>/thredds/pqacts/pqact.obsData
    <LDM_HOME>/etc/TDS/pqact.radars -> <TDS_CONTENT_ROOT>/thredds/pqacts/pqact.radars
    <LDM_HOME>/etc/TDS/pqact.satellite -> <TDS_CONTENT_ROOT>/thredds/pqacts/pqact.satellite

* make symlinks to util, decoders, and cdl directories
    <LDM_HOME>/etc/TDS/decoders -> <TDS_CONTENT_ROOT>/thredds/pqacts/decoders
    <LDM_HOME>/etc/TDS/cdl -> <TDS_CONTENT_ROOT>/thredds/pqacts/cdl
    <LDM_HOME>/etc/TDS/util -> <TDS_CONTENT_ROOT>/thredds/pqacts/util

<LDM_HOME>/etc.
* make symlinks to the .tbl files tables directory
    <LDM_HOME>/etc/snstns.tbl-> <TDS_CONTENT_ROOT>/thredds/pqacts/snstns.tbl
    <LDM_HOME>/etc/snstns.tbl-> <TDS_CONTENT_ROOT>/thredds/pqacts/snstns.tbl

Remember, you will need to add the symlinked pqacts to the LDMs
pqact.conf file. For example:

---------------------
- ldmd.conf snippet -
---------------------


#
# THREDDS processing
#
EXEC    "pqact -f NGRID|CONDUIT|HRS|FNMOC etc/TDS/pqact.forecastModels"
EXEC    "pqact -f NGRID|CONDUIT|HDS etc/TDS/pqact.forecastProdsAndAna"
EXEC    "pqact -f HRS|NIMAGE|NOTHER etc/TDS/pqact.satellite"
EXEC    "pqact -f HRS|FNEXRAD|NNEXRAD|CRAFT etc/TDS/pqact.radars"
EXEC    "pqact -f HRS|IDS|DDPLUS etc/TDS/pqact.obsData"

