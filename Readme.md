# Laminar scripts for the pdf2htmlEX project

This repository contains a collection of 
[Laminar](https://laminar.ohwg.net/) scripts and jobs which I use to build 
/ test / deploy the [pdf2htmlEX](https://github.com/pdf2htmlEX/pdf2htmlEX) 
project (using my personal [development 
fork](https://github.com/stephengaito/pdf2htmlEX)). It assumes that the
'sister' [laminar-scripts](https://github.com/stephengaito/laminar-scripts)
project has already been installed. This project also, incedentally, 
provides another example of one developer's use of Laminar. 

Again, the bash scripts used to control the over all build can be found in 
the `bin` directory. The Laminar jobs, can be found in the `jobs` 
directory. Any 'Tips and Tricks' can be found in the `doc` directory. 

The standard `setup` command, copies all of these scripts into the correct 
laminar `tasks/cfg/jobs` location. 

## Installing the pdf2htmlEX-laminar-scripts project

In the same directory which contains the `laminar-scripts` project, type: 

```
  git clone https://github.com/stephengaito/pdf2htmlex-laminar-scripts.git
  cd pdf2htmlex-laminar-scripts
  ./setup
```

