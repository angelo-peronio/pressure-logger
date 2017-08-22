# Omicron pressure logger

Reads and logs the pressure from the VG (now EpiMAX) PVCi ion gauge controllers of an Omicron LT STM/AFM microscope

Needs:
    * NI Modbus library (tested with ersion 1.1.5.39)
    * H5labview HDF5 bindings (tested with version 2.13.4.143)
	* HDF5 library (tested with version 1.8.19)

Writes:
    * a monthly logfile in hdf5 format
    * a text file with errors and start/stop times

It is reboot-tolerant, performing a clean quit if LabVIEW exits.

## typical MODBUS errors

### 538172
*frequency:* 2.3 errors/hour or 1 error every 7800 MODBUS reads
*description:* MODBUS function data mismatch, the response doesn't match the request
xx72 is bad <whatever I decided was worth checking>--this is usually just whatever feedback I get from the slave. For example the master writes "set x03 to x55" and the slave responds with "set x03 to x22" or "set x55 to x03" then error xx72 is thrown

### 538170
*frequency:* 1.6 errors/day or 1 error every 270000 MODBUS reads
*description:* MODBUS function code mismatch, the function code is invalid
xx70 is a bad function code
The returned function code does not match the requested data." as indicated by the help) means exactly what it says--the function code you sent does not match the one returned

### 56
*frequency:* 0.5 errors/hr or 1 error every 860000 MODBUS reads
*description:* time out or CRC error