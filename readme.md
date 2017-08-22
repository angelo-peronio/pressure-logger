# Omicron pressure logger

Reads and logs the pressure from two VG (now EpiMAX) PVCi ion gauge controllers of an Omicron LT STM/AFM microscope

Needs
* NI Modbus library (tested with version 1.1.5.39)
* H5labview HDF5 bindings (tested with version 2.13.4.143)
* HDF5 library (tested with version 1.8.19)

Writes
* a monthly logfile in hdf5 format;
* a text file with errors and start/stop times.

It is reboot-tolerant, performing a clean quit if LabVIEW exits.

## Typical errors
In our setup we sporadically get the following error codes.

* 538172  
*frequency:* 2.3 errors/hour or 1 error every 7800 MODBUS reads;  
*description:* MODBUS function data mismatch, the response doesn't match the request;  
See https://forums.ni.com/t5/NI-Labs-Discussions/NI-LabVIEW-Modbus-API-Discussion/m-p/3373117#M49 .

* 538170  
*frequency:* 1.6 errors/day or 1 error every 270000 MODBUS reads;  
*description:* MODBUS function code mismatch, the returned function code does not match the requested data.

* 56  
*frequency:* 0.5 errors/hour or 1 error every 860000 MODBUS reads;  
*description:* time out or CRC error.