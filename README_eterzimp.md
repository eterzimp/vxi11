vxi11_transfer branch

Changes:
1. Added a few programs in utils folder which handle separately: connection to an oscilloscope (osci), checking for read-timeout, transferring and deleting txt files
2. Added the line 'CC=g++' in the Makefile both in folders 'utils' and 'library' in order to compile in C++.


Programs:

'vxi11_setup' : Resets the Osci and recalls a screen setup from the file ‘VMM_noise.lss’

'vxi11_5mV' : Resets the Osci and recalls a screen setup from the file ‘VMM_noise_5mv.lss’ (vertical range set to 5mV). 

'vxi11_5mV_trig' : Resets the Osci and recalls a screen setup from the file ‘VMM_noise_5mv_trig.lss’ (vertical range set to 5mV, higher trigger). 

'vxi11_20mV' : Resets the Osci and recalls a screen setup from the file ‘VMM_noise_20mv.lss’ (vertical range set to 20mV). 

'vxi11_50mV' : Resets the Osci and recalls a screen setup from the file ‘VMM_noise_50mv.lss’ (vertical range set to 50mV). 

'vxi11_transfer' : This script stores the waveform into 10 files in the oscilloscope and transfers the content of these files in files located in the laptop. The files will be created in the folder in which the script’s executable is. Careful: If you run this script once, you should always run one of the setup scripts above before running it again. This is because, the Osci uses a filename tracker to store files in the osci. That is, if file ‘C4test_data00000.txt’ exists, next waveform will be stored in file ‘C4test_data00001.txt’ and so on. The problem is, even if you command the Osci remotely to delete these files (which is also done in the transfer script), the filename counter stills “thinks” they are there. There is no way to control this remotely, only to “reset” the Osci and so the counter resets, which is what the setup scripts do. The transfer-file command needs a specific file name, so the vxi11_transfer script is specifically designed to read from file  ‘C4test_data00000.txt’ to file ‘C4test_data00009.txt’. 

'vxi11_transfer20' : This script is the same as the one right above, only it reads from file ‘C4test_data00010.txt’ to file ‘C4test_data00019.txt’.

'vxi11_delete' : Deletes files from ‘C4test_data00020.txt’ to ‘C4test_data00039.txt’ in the Osci in case they got created accidentally. 

'vxi11_check' : This script was only written to be used in an automatic calibration process. Basically, after receiving a reset command, the Osci has a dead response time of 15 seconds. In that time, any sent query command will result in a read timeout error. So this script basically “waits out” this time in a while loop. 
