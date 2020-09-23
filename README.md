# docker-Sen2cor
## step 1: building docker image
  go to the repository dir (where you can find the Dockerfile) and run:
  docker build -t sen2cor_2.8.0 .

## step 2: downloading auxiliarie files
  download from http://maps.elie.ucl.ac.be/CCI/viewer/download.php (fill info on the right and download "ESACCI-LC for Sen2Cor data package")
  extract the downloaded file and the files within. It will contain two files and one directory:

  Example on Ubuntu (Linux) installation:
  $ ls home/user/sen2cor/CCI4SEN2COR
  ESACCI-LC-L4-LCCS-Map-300m-P1Y-2015-v2.0.7.tif
  ESACCI-LC-L4-Snow-Cond-500m-P13Y7D-2000-2012-v2.0
  ESACCI-LC-L4-WB-Map-150m-P13Y-2000-v4.0.tif

  More info can be found on Sen2Cor Configuration and User Manual ( http://step.esa.int/thirdparties/sen2cor/2.8.0/docs/S2-PDGS-MPC-L2A-SUM-V2.8.pdf )

## step 3: run sen2cor from outside docker:
  docker run --rm -v /path/to/CCI4SEN2COR:/home/lib/python2.7/site-packages/sen2cor/aux_data -v /path/to/folder/containing/.SAFEfile:/app sen2cor_2.8.0 yourFile.SAFE

  Example: 
    docker run --rm -v /home/user/sen2cor/CCI4SEN2COR:/home/lib/python2.7/site-packages/sen2cor/aux_data -v /home/user/Downloads:/app sen2cor S2B_MSIL1C_20200604T142729_N0209_R053_T20MMT_20200604T161053.SAFE

## step 3 (alternative): run sen2cor from inside docker:
  docker run --rm -it --entrypoint="" -v /path/to/CCI4SEN2COR:/home/lib/python2.7/site-packages/sen2cor/aux_data -v /path/to/folder/containing/.SAFEfile:/app sen2cor_2.8.0 bash

  cd /app

  L2A_Process --resolution 10 /app/file.SAFE

  Example:
    docker run --rm -it --entrypoint='' -v /user/sen2cor/CCI4SEN2COR:/home/lib/python2.7/site-packages/sen2cor/aux_data -v /home/user/Downloads:/app sen2cor bash
