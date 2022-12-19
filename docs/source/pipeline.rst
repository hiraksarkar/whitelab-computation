Main Computational Resources
========
Person of contact
-------------------
To receive an account needed for accessing the whitelab servers within Rutgers, one needs to contact the 
following persons for setting up an account,

Wenping Yang yangw3@cinj.rutgers.edu

Adrian Rodriguez alr252@cinj.rutgers.edu

Prices:
-----------------
Quotes (Virtual Machines within CINJ)::

        Per CPU: $4.29
        Per 8 GB RAM:  $4.95
        Per GB Drive Space:  $0.0594
        Per GB NetBackup: $0.08613


Our Resources
------------------
We have 2 different servers with the following configuration 

**Machine 1** 
- RAM : 128 GB - Space : 2 TB (extendable) ~ $950 per year

**Machine 2**
- RAM : 64 GB - Space : 6 TB (extendable) ~ $500 per year


Logging in
------------------
using command prompt within mac terminal::

        $ssh <NetID>@amarel.rutgers.edu
        $tmux new -s <screen name>
        $tmix a -t <screen>

Copying data from remote
---------------------------
Using rsync::

        rsync -av --progress <NetID>@amarel.rutgers.edu:<path_to_dir_to_copy> <your_local_dir>

Copying data to remote 
-------------------------
Using rsync::

        rsync -av --progress <your_local_dir> <NetID>@amarel.rutgers.edu:<path_to_dir_to_copy> 


Single Cell Data
-----------------

**Tools**

- `Scanpy <https://broadinstitute.github.io/picard/>`_
- `Seurat <https://github.com/broadinstitute/Drop-seq/tree/v2.5.1>`_
- `Differential Expression Analysis <https://github.com/alexdobin/STAR>`_


Spatial transcriptomics Data
-------------------------------


Before going into the installation procedure. We should go over the actual input format. 
The input folder contains the raw sequencing reads. 

The operation starts from the ``BASECALLS_DIR``, that contains the actual intensities and the 
``bcl`` files. For example the basic structure of such file will be 

::

        ➜slide-seq-pipeline git:(main) ls /home/hsarkar/code/slide-seq-data/P25255/220329_A00689_0513_BHYK23DRXY/
        Config            InterOp                 Recipe           RunInfo.xml        SequenceComplete.txt
        CopyComplete.txt  Logs                    RTA3.cfg         runParameters.xml  Thumbnail_Images
        Data              P25255_SampleSheet.txt  RTAComplete.txt  RunParameters.xml


The ``bcl`` files are present in ``Data/Intensities/BaseCalls/``.  The ``RunInfo.xml`` used to be the file
that has the information that is to be parsed before writing down the information.

Use the existing `package <https://github.com/MacoskoLab/slideseq-tools>`_ so that we can import existing structures 
from the ``slideseq-tools``. 

Install existing ``slideseq-tools`` package 
::

        >git clone https://github.com/MacoskoLab/slideseq-tools.git

Create a spread-sheet that contains some of the following fields that we need to feel. An example spread-sheet
is provided in `spreadsheet` folder of the repo. 

::

        Index(['library', 'date', 'flowcell', 'run_name', 'bclpath', 'lane',
        'sample_barcode', 'bead_structure', 'reference', 'run_barcodematching',
        'locus_function_list', 'start_sequence', 'base_quality',
        'min_transcripts_per_cell', 'email', 'puckcaller_path', 'bead_type',
        'gen_read1_plot', 'gen_downsampling'],
        dtype='object')


**Desctiption**


library: Name of the library (Each puck will have a specic name)
puckcaller_path: A location containing the files from the image analysis pipeline, ``BeasBarcodes.txt`` and ``BeadLocations.txt``
run_name: Depends on how many different runs we are having
BCLPath: Actual location to the BCL files
sample_barcod: It's a 8bp barcode that can be obtained from  ``RunInfo.xml`` file with the column name ``index`` (I am not sure about this yet)
reference: The actual reference file I used ``GRCh38.fasta``
bead_structure: Determines the actual length of the cell barcode and the corresponding UMI

**Cosntruction**


The construction of the dataframe with the help of the ``RunInfo.xml`` is depicted in the
next embedded notebook.