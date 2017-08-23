# pressure-logger

Reads, displays, and logs the pressure measured by two VG (now EpiMAX) PVCi ion gauge controllers of an Omicron LT STM/AFM microscope.
Communication with the controllers uses MODBUS over RS232, the logfile is in HDF5 format.

Needs
* NI Modbus Library  
https://forums.ni.com/t5/NI-Labs-Toolkits/LabVIEW-Modbus-API/ta-p/3524019  
tested with version 1.1.5.39

* H5labview HDF5 bindings for LabVIEW  
http://h5labview.sf.net/  
tested with version 2.13.4.143

* HDF5 library  
https://www.hdfgroup.org  
tested with version 1.8.19

Writes
* a monthly logfile in HDF5 format;
* a text file with errors and start/stop times.

It is reboot-tolerant, performing a clean quit if LabVIEW exits.

## Usage
Before running `main-pressure-logger.vi`, edit its source code to set:
* serial port parameters;
* MODBUS unit IDs;
* path to the folder containing the logfiles.

## Typical errors
In our setup we sporadically get the following error codes:

* 538172  
*frequency:* 2.3 errors/hour or 1 error every 7.8k MODBUS reads;  
*description:* MODBUS function data mismatch, the response doesn't match the request;  
See [here](https://forums.ni.com/t5/NI-Labs-Discussions/NI-LabVIEW-Modbus-API-Discussion/m-p/3373117#M49).

* 538170  
*frequency:* 1.6 errors/day or 1 error every 270k MODBUS reads;  
*description:* MODBUS function code mismatch, the returned function code does not match the requested data.

* 56  
*frequency:* 0.5 errors/day or 1 error every 860k MODBUS reads;  
*description:* time out or CRC error.