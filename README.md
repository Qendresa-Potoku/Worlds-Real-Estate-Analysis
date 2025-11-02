# World Real Estate Data Preprocessing Project

## Overview

This project focuses on preparing and transforming a real estate dataset to enable country-level price comparison and gain insight into international property market trends. It involves comprehensive data cleaning, feature transformation, and quality assurance using real-world listings sourced from multiple global regions.


---

## Dataset Summary

We used the [World's Real Estate Data (147k)](https://www.kaggle.com/datasets/toriqulstu/worlds-real-estate-data147k) from Kaggle, originally collected from [REALTING.com](https://realting.com/), a global property platform.

- **Rows**: 147,000+ listings  
- **Columns**: 14+ attributes

This dataset provides a rich context for evaluating pricing patterns, property characteristics, and regional differences in housing markets.


### Dataset Attributes


| Column                     | Type      | Description                                                                 |
|----------------------------|-----------|-----------------------------------------------------------------------------|
| `title`                   | String    | Name of the property listing.                                         |
| `country`                 | Category  | Country where the property is located.        |
| `location`                | Category  | Specific location within the country.              |
| `building_construction_year` | Integer   | Year when the building was constructed.            |
| `building_total_floors`  | Integer   | Total number of floors in the building.            |
| `apartment_floor`        | Integer   | The floor level the apartment is on.                |
| `apartment_rooms`        | Integer   | Number of total rooms in the apartment.            |
| `apartment_bedrooms`     | Integer   | Number of bedrooms.                                      |
| `apartment_bathrooms`    | Integer   | Number of bathrooms.                                |
| `apartment_total_area`   | Float     | Total area in square meters.                                    |
| `apartment_living_area`  | Float     | Living area (m²).                              |
| `price_in_USD`           | Float     | Property price in USD.                                                      |
| `image`                  | URL       | Link to a preview image of the property.                                    |
| `url`                    | URL       | Link to the original listing on REALTING.com.                               |



---

## Preprocessing Workflow Summary

The following preprocessing steps were applied to clean and prepare the real estate dataset for analysis:

1. **Data Loading & Quality Check**
   - Loaded dataset (~147k rows)
   - Inspected structure, types, and value distributions
   - Checked for duplicates and missing values

2. **Data Type Conversion**
   - Converted area fields from string (e.g., `"100 m²"`) to numeric
   - Standardized decimal formats and removed non-numeric characters
   - Categorical encoding for repeated nominal fields (e.g., country, location)
   - Applied nullable integer types to numeric columns with missing values

3. **Handling Missing Values**
   - Inferred missing `bedrooms` and `rooms` from title text
   - Filled remaining missing values with median-based imputation
   - Ensured all retained rows had sufficient information for analysis

4. ** Feature Extraction**
   - Parsed `title` to extract `property_type` (e.g., apartment, house, villa)

5. **Dimension Reduction**
   - Performed optional PCA for reducing dimensionality

6. **Feature Engineering**
   - Created `price_per_m2` and capped extreme values
   - Added binary `is_new_building` feature based on construction year
   - Log-transformed `price_per_m2` to normalize distribution

7. **Discretization**
   - Categorized listings into `Low`, `Medium`, and `High` price tiers using `pd.qcut`

8. **Binarization**
   - Converted building age to binary: `1` = new (≤10 years), `0` = old

9. **Transformation**
   - Applied `log1p` to `price_per_m2` to reduce skew and support modeling

10. **Sampling**
    - Random 10% sampling by country
    - Verified sample representativeness using mean price comparison

11. **Export**
    - Selected final cleaned features
    - Saved processed dataset to CSV for further analysis and visualization

---

## Project Structure

- **data/** 
  - **world_real_estate_data.csv** 
  - **cleaned_world_real_estate_data.csv** 
- **data_preprocessing.ipynb**
- **README.md** 

---

## Technologies Used

- **Python**
- **Jupyter Notebook**
- **Pandas**
- **NumPy**
- **Matplotlib** / **Seaborn**

---

