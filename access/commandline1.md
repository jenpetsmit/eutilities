# Access E-utility APIs Using Command Line

To access E-utility APIs using the command line use Entrez Direct (EDirect), the E-utilities command-line tool.

EDirect runs on Unix, Linux, and Macintosh computers, and under the Cygwin Unix-emulation environment on Windows PCs.

To install the EDirect software: 
1.	Open a terminal window and copy and paste one of the following two commands:
   
  `sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)`

  `sh -c "$(wget -q https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh -O -)`
  
An edirect folder with several scripts and precompiled programs is added to your home directory. 

As a convenience, the installation process offers to run the PATH update command for you. 

  `echo "export PATH=\$HOME/edirect:\$PATH" >> $HOME/.bash_profile`
  
If you want to automaticlly update the export PATH:

2.	Answer **y** and press the **Return** key
3.	If the PATH is already set correctly, or if you prefer to make any editing changes manually, just press **Return**.

Search terms are entered as command-line arguments. Individual operations connect with Unix pipes to construct multi-step queries for you. Selected records can then be retrieved in a variety of formats.
Installation
