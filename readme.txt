Angelo Peronio
2017-07-14

Reads and logs the pressure from the PVCi ion gauge controllers of the Omicron microscope
Needs:
    * NI Modbus library
    * H5labview HDF5 library

Writes
    * a monthly log in hdf5 format
    * a text file with errors and start/stop times

It is reboot-tolerant: performs a clean quit if LabVIEW exits.

Typical error codes:

538172
frequency: 2.8e-4
function data mismatch, the response doesn't match the request
xx72 is bad <whatever I decided was worth checking>--this is usually just whatever feedback I get from the slave. For example the master writes "set x03 to x55" and the slave responds with "set x03 to x22" or "set x55 to x03" then error xx72 is thrown

538170
frequency: rare
function code mismatch, the function code is invalid
xx70 is a bad function code
The returned function code does not match the requested data." as indicated by the help) means exactly what it says--the function code you sent does not match the one returned

56
frequency: rare
time out or CRC error