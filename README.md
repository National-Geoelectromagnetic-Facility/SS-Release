# SS-SSM

The SS and SSM programs are Matlab programs for evaluating and setting up the 
processing of NIMS 1 Hz and 8 Hz, currently unverified to work with 8 Hz, data 
files.  These are wrapper programs to evaluate the data and convert it to 
processing programs dnff and tranmtlr.  These processing programs are Fortran 
programs written by Dr. Gary Egbert and can be found here:

http://www.mtnet.info/programs/egbert.html

SS reads in raw data files, tries to correct data gaps, and displays the 
appropriate information to evaluate the time series in preparation to convert
time series to apparent resistivity and phase plots through dnff and tranmtlr.
SS needs the Matlab Runtime Environment for Matlab version R2019b.  It also 
requires a folder structure as seen below.

SSM is similar to SS, except it reads a Matlab mat file instead of a raw bin 
file.  While it is faster to read the data in a mat file, it does not display
the temperature variation and uncorrected time series graphs.  Otherwise, it is
the same as SS.


Installing the NIMS processing software:


Step 1) Download EMTF from Gary Egbert's website above.

Step 2) Compile dnff located in the 'D' directory under 'EMTF' directory via a 
        Fortran compiler such as gfortran.

Step 3) Compile tranmtlr located in the 'T' directory under 'EMTF' directory via
        a Fortran compiler such as gfortran. 

        * Currently, there is an error in the source code when compiling
          tranmtlr with gfortran.  By changing line 103 from

          cfac(i) = 4*ldf(ib)*ldf(ib)/(idf(ib)*2*(2*rdf(i,ib)-2*idf(ib)))

          to

          cfac(i)=4*ldf(ib)*ldf(ib)/(idf(ib)*2*(2*rdf(i,ib)-2*idf(ib)))

          will solve the compiling error.

Step 4) SS requires a specific folder structure to operate correctly.  
        -Copy executable dnff, tranmtlr from 'D' and 'T' directories into the 
         'bin' directory.
        -Copy the 'CF' directory from the 'EMTF/CF' directory into 'Earthscope'.
        -Copy the 'wmm' directory into the 'MT' directory.
        -All other directories are empty directories that must be present.

Required Folder Structure:

    /Users/%User%/MT
                    /bin
                        /dnff
                        /tranmtlr
                    /surveys/
                            /Earthscope
                            /Earthscope/original
                            /Earthscope/CF
                                          /bs_1HzNIMS.cfg
                                          /decset_1hz.cfg
                                          /options_1hz_SS.cfg
                                          /options_SS.cfg
                                          /paths.cfg
                                          /pwset_1hz.cfg
                    /wmm
                        /WMM.COF
                        /WMM2000.COF
                        /WMM2005.COF
                        /WMM2010.COF
                        /WMM2015v2.COF
                        /WMM2020.COF

Step 5) Run the SS and SSM installer.


SS/SSM Source Code:

Matlab Toolboxes Needed:
    -Aerospace Toolbox
    -Signal Processing Toolbox
