# Laminar jobs for building pdf2htmlEX

To control the overal build/test/deploy cycle, I make extensive use of 
chaining Laminar jobs. This is as simple as using a `laminar queue` 
command at the end of a successful build job. 

- `buildPdf2htmlEX.run` acutally builds, installs and creates an AppImage, 
  Debian archive and a Docker image. 

  The `DIST` environment variable is used to control which Ubuntu 
  distribution is used to build pdf2htmlEX. 

- `testPdf2htmlEX.run` tests a given version of pdf2htmlEX

## Notes:

Most of these scripts run inside one or other specifically controled 
docker image (the script which actually finishes the pdf2htmlEX docker 
image MUST be run *outside* of docker). 
