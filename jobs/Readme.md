# Laminar jobs for building pdf2htmlEX

To control the overal build/test/deploy cycle, I make extensive use of 
chaining Laminar jobs. This is as simple as using a `laminar queue` 
command at the end of a successful build job. 

- `pdf2htmlex.before` A pdf2htmlex project before script to ensure the 
  `REPO` and `PDF2HTMLEX_BRANCH` environment variables are set.

- `pdf2htmlex-build.run` acutally builds, installs and creates an 
  AppImage, Debian archive and a Container image. 

  The `DIST` environment variable is used to control which Ubuntu 
  distribution is used to build pdf2htmlEX. 

  This build job will also test the "locally" compiled version of 
  `pdf2htmlEX`. 

- `pdf2htmlex-test.run` tests all pdf2htmlEX release objects (AppImage, 
  Debian Archive, Container image). 

- `pdf2htmlex-testAppImage.run` tests the pdf2htmlEX AppImage. 

- `pdf2htmlex-testDpkg.run` tests the pdf2htmlEX Debian archive. 

- `pdf2htmlex-testContainer.run` tests the pdf2htmlEX Container image. 

## Testing

We want to run three types of tests on each of the originally compiled 
pdf2htmlEX, as well as the AppImage, Debian archive and Container image 
versions. 

1. pdf2htmlEX/tests/test_output.py (simple tests to determine that the 
   correct output files are created).

2. pdf2htmlEX/tests/test_local_browser.py (image comparison tests on a 
   selected number of accepted html files compared to corresponding html 
   files created with the current version of pdf2htmlEX -- uses the 
   Selenium geckodriver ) . 

3. produce html output from each pdf file in my examples collection for 
   later review by a human using a web-browser.

In each case the results should be left for review in the corresponding 
test's run directory.

**It would be very nice** if the html files accumulated in the 
browser_tests directory during the test_local_browser.py test were also 
browsable by the same tools as used to brwose the results of the human 
review-able tests. 

**Trick:** The test.py script expects to find a `pdf2htmlEX` executable in 
"its" well known place. For each of the different types of pdf2htmlEX 
release, we can write a bash shell wrapper which drives that particular 
release version and place that wrapper script in the location which the 
test.py script is expecting to find `pdf2htmlEX`. 

**Question:** can the Selenium geckodriver be run in parallel? That is can 
we run the tests in parallel in the same $DIST and across all $DISTs at 
potentially the *same* time? 

## Notes:

Most of the bash scripts which these Laminar jobs run, are run inside one 
or other specifically controled OCI container. This allows us to have 
tighter control over the installed environment in which the build script 
runs, compiles, and packages an artifact. 

At the moment, any pdf2htmlEX build script which requires the use of a 
container command, should be split into two parts. One part which *can* be 
run *inside* an OCI container, and the other part which "finishes" the 
action by calling the container command from *outside* of any OCI 
container. 

The pdf2htmlEX build script which creates the container image is 
structured as two parts. One part to be run in the compile environment 
inside an OCI container, and the other part, to finish the creation of the 
container, to be run outside of any OCI container. 
