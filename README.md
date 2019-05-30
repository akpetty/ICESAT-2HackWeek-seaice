# ICESAT-2HackWeek-seaice
ICESat-2 hack week repository for those in the sea ice team


Run the following from the terminal to get the data you need in your repo..
cp Data
aws s3 cp s3://pangeo-data-upload-oregon/icesat2/ATL07-01_20181115003141_07240101_001_01.h5 .

aws s3 cp s3://pangeo-data-upload-oregon/icesat2/ATL03_20181115022655_07250104_001_01.h5 .

To upload the data 

aws s3 cp ATL03_20181115022655_07250104_001_01.h5 s3://pangeo-data-upload-oregon/icesat2/
aws s3 cp ATL07-01_20181115003141_07240101_001_01.h5 s3://pangeo-data-upload-oregon/icesat2/