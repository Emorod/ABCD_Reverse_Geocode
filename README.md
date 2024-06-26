# ABCD_Reverse_Geocode
Using available data to reverse code ABCD datasets

# ABCD Geocode Log

## Overview

This repository provides a detailed workflow for reverse geocoding using the Social Vulnerability Index (SVI) and other relevant indices to reverse code census tract and block group identifiers. The process consists of four main steps:

### Step One: Using SVI to Reverse Code to Census Tract ID (11-Digit FIPS Code)

1. **Input Data:** ABCD external-linked SVI variables and Downloaded SVI csv for all census tracts in the US (https://www.atsdr.cdc.gov/placeandhealth/svi/data_documentation_download.html). 
2. **Process:** Use the SVI data to match each participant to its corresponding 11-digit FIPS code (Census Tract ID).
3. **Output:** csv file containing subject ID and matched Census Tract IDs.

### Step Two: Reverse Code to Block Group

1. **Input Data:** 1) csv from Step One with Census Tract IDs 2) ABCD-linked walkability and residential density (D1a) 3) downloaded national walkability and residential density (
2. **Process:** 
   - Check for replicate entries.
   - Use the Walkability Index and Residential Density (d1a) along with the 11-digit FIPS code to map addresses to their respective block groups.
3. **Output:** Addresses mapped to Block Group IDs and 10-digit GEOID.

### Step Three: Secondary Matching Using State Code

1. **Input Data:** Participants that did not match in Step Two.
2. **Process:** 
   - Use the first two digits of the FIPS code (State Code) and the two indices (Walkability Index and d1a) to attempt a secondary match.
3. **Output:** Additional matches of addresses to Census Tract IDs.

### Step Four: Tertiary Matching Using Site-Derived State

1. **Input Data:** Participants that did not match in Step Three.
2. **Process:** 
   - Use the site-derived state and the two indices (Walkability Index and d1a) to find the best possible match.
3. **Output:** Final set of matches for addresses to Census Tract IDs.

## Output

The final output will be a comprehensive dataset including the following variables:

- `src_subject_id`: Subject ID.
- `[CensusTractFIPS, State, County, Location]`: From Step One.
- `[GEOID10, BlkGrpID]`: From Step Two.
- `[CensusTractFIPS_y]`: From Steps Three and Four.

## Repository Structure

- `data/`: Directory containing input data files.
- `scripts/`: Directory containing all scripts used for processing and matching.
- `output/`: Directory containing the final output dataset.
- `README.md`: This file.

## Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/YourUsername/ABCD-Geocode-Log.git
   cd ABCD-Geocode-Log
