# HARP - Transitions

### Summary of HARP

The HARP Project is an NIH-funded P50 Center grant in collaboration with the Center for Family Research at the University of Georgia. It is designed to transform scientific understanding regarding the causes and prevention of addictive behaviors by investigating (a) the biological and neurocognitive contributors to addictive behaviors that drive many drug use and health disparities African Americans’ experience and (b) the potential of family-centered prevention programming to ameliorate the influence of growing up in chronically stressful contexts. Our neuroimmune network (NIN) model specifies stress-induced alterations in the transactions between peripheral inflammation and neurocognitive systems that subserve emotion regulation in the development of addictive behavior vulnerability. RP1 (Transitions) provides an in-depth assessment on neural activity and inflammation and comprises a “deep dive” into mechanistic hypotheses suggested by the NIN model through a two-wave study spanning 2.5 years of African American emerging adults, ages 18-20 at baseline. 

Data collection includes bioimaging of NIN-related neural systems, assay of peripheral inflammation, and measures of stress exposure and addictive behaviors. RP2 (Foundations) conducts a pioneering longitudinal, two-year experimental trial that includes baseline and follow-up assessments with fMRI, inflammatory, and behavioral data with 300 African American youth at age 11 and their primary caregivers. This study will be able to examine empirically the underlying biological mechanisms for the multi-level benefits of family-centered prevention programming. You can learn more about the projects here.

## TRANSITIONS: Neuroimaging Data Processing Workflow

The TRANSITIONS repository contains scripts used to organize, prepare, and preprocess neuroimaging data collected as part of Research Project 1 (RP1) of HARP.

The repository contains scripts for the following components of the neuroimaging processing workflow:

### 1. DICOM Data Extraction and Preparation

Extracting raw MRI data and examining acquisition metadata before conversion into NIfTI format.

- `scripts/bidsprocessing/unzip_dicoms.py` — Extracts compressed DICOM archives into participant-specific directories.

- `scripts/bidsprocessing/python_caller.sh` — Submits the DICOM extraction script as a Slurm job.

- `scripts/bidsprocessing/tabulate_dicom_headers.py` — Extracts MRI acquisition parameters from DICOM headers and organizes them into a CSV file.


### 2. MRI Data Conversion and BIDS Organization

Converting raw MRI data into NIfTI format and organizing the resulting files according to BIDS conventions.

- `scripts/bidsprocessing/dirs_to_nifti.sh` — Converts DICOM files from MRI scan directories into NIfTI format using dcm2niix.

- `scripts/bidsprocessing/dicom_to_bids.py` — Converts DICOM scans into NIfTI format, identifies imaging modalities, and organizes the resulting files into BIDS-style directories.

- `scripts/bidskit.sh` — Runs BIDSkit to support the organization of neuroimaging data according to BIDS conventions.

- `scripts/to_studies_dir.py` — Copies organized imaging and behavioral data from the legacy Georgia study directories into the TRANSITIONS study directories.


### 3. De-identification and Data Preparation

Removing identifying information from imaging files, preparing anatomical images, and updating metadata required for BIDS organization.

- `scripts/harp_pih_remover.py` — Renames and organizes imaging files into BIDS-style directories, removing participant names from filenames.

- `scripts/bidsprocessing/harp_pih_remover_single.py` — Performs participant-specific file renaming and BIDS organization.

- `scripts/bidsprocessing/deface.sh` — Runs defacing on T1-weighted anatomical MRI images to remove facial features.

- `scripts/bidsprocessing/add_intended_for.py` — Updates field-map JSON files with IntendedFor metadata linking field maps to their corresponding functional images.

- `scripts/bidsprocessing/add_task_name.py` — An additional metadata-editing script that requires review before use.


### 4. BIDS Validation and MRI Quality Control (MRIQC)

Validating the organization of neuroimaging data and assessing the quality of structural and functional MRI data to identify potential imaging artifacts and data quality concerns.

- `scripts/bidsprocessing/bidsvalidatetransitions.sh` — Runs the BIDS Validator to identify potential errors in the organization and metadata of the TRANSITIONS dataset.

- `scripts/transitions_mriqc.sh` — Runs MRIQC for an individual participant to generate imaging quality metrics and reports.

- `scripts/mriqc/` — A linked MRIQC repository containing additional quality-control resources.


### 5. fMRI Preprocessing (fMRIPrep)

Preparing functional MRI data for subsequent statistical analysis through preprocessing procedures, including motion correction, anatomical-functional registration, and spatial normalization.

- `scripts/fmriprep/fmripreploop.sh` — Reads a participant list and submits individual fMRIPrep processing jobs.

- `scripts/fmriprep/fmriprepsinglepartic.sh` — Executes fMRIPrep for an individual participant.

The repository also contains alternative fMRIPrep scripts:

- `scripts/fmriprep/Kat_fmriprepsinglepartic.sh`
- `scripts/fmriprep/Kat_fmriprepsinglepartic21.sh`
- `scripts/fmriprep/Kat_fmriprepsinglepartic_bids.sh`
- `scripts/fmriprep/Zach_fmriprepsinglepartic.sh`



