# transitions

# harp

### Summary of HARP

There is a scientific consensus emerging that developmental exposures to social adversity can promote drug use vulnerabilities through cumulative effects on neurobiological and peripheral systems.

The Health and Resilience Project (HARP) is an NIH-funded P50 Center research program that aims to investigate how chronic stress exposure, experienced through social adversity, affects the biological and psychological development of children and young adults. HARP aims at investigating how this toll manifests in escalating rates of addictive behavior, including drug use and unhealthy eating.

The African American populations on whom the P50 Center and Research Project 2 (RP2) focus are disproportionately exposed to such social adversities. The proposed P50 continues and expands the pioneering work of the Center for Translational and Prevention Science (CTAPS) through two avenues:

    (a) Biological and Neurobiological - Investigating the biological and neurobiological contributors to addictive behaviors that drive many drug use and health disparities African Americans experience.

    Here we ask: How does chronic stress get under the skin to heighten vulnerability to addictive behaviors, including drug use and unhealthy eating, and the cardiometabolic health conditions that such behaviors generate? To begin to address this question, CTAPS scientists proposed a neuroimmune network (NIN) model highlighting bidirectional signaling between the brain and immune system in the pathophysiology of addictive behaviors.

    (b) Family-centered Prevention Programming - Conducting studies that illuminate the potential of family-centered prevention programming to ameliorate the pernicious and persistent influence of growing up in chronically stressful contexts.


The mechanisms and processes investigated in the P50 are not limited to African American populations; we expect them to have broad applicability in furthering scientific understanding of the etiology and prevention of addictive behavior among other US populations exposed to chronic stress.


### HARP Research Projects

To address these objectives, HARP comprises two complementary research projects:

**TRANSITIONS (RP1) — Emerging Adulthood (Ages 18–20 at baseline):** Examines how chronic stress exposure influences neuroimmune functioning and vulnerability to addictive behaviors during the transition to adulthood, with a focus on the biological pathways linking social adversity to adverse health outcomes.

**FOUNDATIONS (RP2) — Childhood and Early Adolescence (Age 11 at baseline):** Investigates how chronic stress exposure affects neuroimmune development and whether family-centered prevention programming can mitigate these effects and reduce vulnerability to addictive behaviors.

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



