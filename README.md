Customer Call List Data Cleaning with Python and pandas

## Project Overview

This project demonstrates how Python's **pandas** library can be used to clean and prepare customer contact data for reliable analysis and business use.

Using an Excel customer call list containing 21 rows and 8 original columns, I investigated data-quality issues, removed duplicate records, standardized customer information, cleaned phone-number formats, separated address components, and documented errors encountered during the cleaning process.

The project also includes an improved cleaning workflow designed to prevent data loss and preserve the original meaning of customer contact preferences.

## Business Problem

Customer contact lists often contain inconsistent formats, duplicate records, missing values, and poorly structured fields. These issues can affect customer communication, reporting accuracy, and the reliability of downstream analysis.

The objective of this project was to transform an inconsistent customer call list into a more structured and usable dataset using Python.

## Dataset Overview

The original dataset contained 21 rows and 8 columns:

- `CustomerID`
- `First_Name`
- `Last_Name`
- `Phone_Number`
- `Address`
- `Paying Customer`
- `Do_Not_Contact`
- `Not_Useful_Column`

After removing the duplicate record, the dataset contained 20 unique customer records.

## Data Quality Issues Identified

The initial inspection revealed several problems:

- **Duplicate records:** Customer ID 1020 appeared twice.
- **Irrelevant column:** `Not_Useful_Column` contained no useful information.
- **Inconsistent names:** Some last names contained stray characters, such as `/White`, `...Potter`, and `Flenderson_`.
- **Inconsistent phone formats:** Phone numbers contained hyphens, slashes, vertical bars, or no separators.
- **Missing phone numbers:** Some entries contained `NaN` or `N/a`.
- **Unstructured addresses:** Street address, state, and ZIP code were stored in a single column.
- **Inconsistent categorical values:** Customer flags used variations such as `Yes`, `No`, `Y`, `N`, and missing-value placeholders.
- **Missing-value inconsistencies:** Empty values appeared as `NaN`, `None`, and `N/a`.

## Tools and Technologies

- Python
- pandas
- Excel
- Jupyter Notebook
- Regular expressions (regex)

## Analytical and Cleaning Workflow

### 1. Importing pandas and loading the dataset

I imported pandas and used `read_excel()` to load the Excel workbook into a DataFrame for inspection and transformation.

<img width="731" height="370" alt="Pandas 1" src="https://github.com/user-attachments/assets/8e98205d-1d0b-46fc-8f04-e78873af292c" />


### 2. Removing duplicate records

I applied `drop_duplicates()` to remove the repeated row, reducing the dataset from 21 rows to 20.

### 3. Removing irrelevant columns

I dropped `Not_Useful_Column` because it did not contribute meaningful information to the analysis.

### 4. Cleaning customer names

I used pandas string methods, including `str.strip()`, to remove unwanted characters from the beginning and end of affected last names.

### 5. Standardizing customer flags

I investigated how to standardize `Paying Customer` and `Do_Not_Contact` values using consistent `Y` and `N` labels.

During this step, I identified a column-reference error in the original notebook that overwrote the do-not-contact values with values from the paying-customer column.

### 6. Cleaning phone numbers

I explored regular expressions to remove unwanted phone-number separators and standardize valid 10-digit numbers into the `XXX-XXX-XXXX` format.

I also identified a data-type issue: pandas string methods do not reliably process numeric values as strings. Converting values to text without handling missing values and numeric representations can create additional problems.

### 7. Splitting address components

I used `str.split(',', n=2, expand=True)` to separate the original address into:

- `street_Address`
- `State`
- `zip_code`

I also identified the need to remove leading and trailing spaces after splitting.

### 8. Handling missing values

I examined how pandas represents missing values and compared replacing them with blank strings against retaining proper missing-value markers.

For the improved workflow, missing values should be handled deliberately rather than indiscriminately replaced with spaces.

### 9. Validating the cleaned dataset

The final validation should confirm that:

- Duplicate records have been removed.
- Required customer fields are retained.
- Phone numbers are correctly formatted where valid.
- Original do-not-contact preferences remain intact.
- Address components are separated correctly.
- Missing values are handled consistently.
- The cleaned output is saved to a new Excel file.

## Key Findings and Lessons Learned

**1. Data types matter.** Numeric phone values require careful conversion before string operations. Incorrect handling can cause valid contact numbers to disappear.

**2. Column references matter.** Referencing the wrong DataFrame column can silently overwrite important customer information.

**3. Regex requires explicit handling.** In current pandas versions, `regex=True` should be specified when a regular expression is intended.

**4. Missing values need a deliberate strategy.** A blank string or a string containing a space is not equivalent to a genuine missing value.

**5. Data cleaning requires validation.** A successful command does not guarantee a correct dataset. The output must be checked against the original records and the intended business rules.

## Recommended Improvements

- Normalize phone numbers using a function that handles missing values and numeric Excel representations safely.
- Standardize `Yes` and `No` using exact-value mappings rather than unrestricted text replacement.
- Preserve `Do_Not_Contact` independently from `Paying Customer`.
- Trim whitespace from all address components.
- Retain missing values where their absence carries analytical meaning.
- Check customer IDs for duplicates and investigate conflicting records before deleting them.
- Save the cleaned dataset separately to preserve the original source file.

## Project Outcome

The project established a cleaning workflow for a 20-record customer contact list and documented the key corrections needed to make the process more reliable.

The recommended workflow improves data consistency while reducing the risk of losing phone numbers or overwriting customer contact preferences.

## Conclusion

This project strengthened my practical understanding of data cleaning with pandas, including duplicate removal, string manipulation, regular expressions, address parsing, missing-value handling, and data validation.

It also reinforced an important principle of data analytics: cleaning is not complete merely because the code runs. The resulting dataset must remain accurate, consistent, and fit for its intended purpose.

**Skills demonstrated:** Python | pandas | Data Cleaning | Excel Data Import | String Manipulation | Regular Expressions | Missing-Value Handling | Data Validation

Customer Call List Data Cleaning
