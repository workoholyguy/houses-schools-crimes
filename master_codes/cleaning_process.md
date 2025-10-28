# School Quality Analysis Project

## Project Overview
This repository contains tools for processing, integrating, and evaluating school quality metrics from multiple data sources. The project enables objective comparison of schools based on standardized metrics across academic performance, resources, equity, environment, and outcomes.

## Contents
- [Data Sources](#data-sources)
- [Data Processing Pipeline](#data-processing-pipeline)
- [Quality Metrics Framework](#quality-metrics-framework)
- [Usage Instructions](#usage-instructions)

## Data Sources

The analysis integrates data from several educational sources [data/raw/...]:

| File | Description | Metrics |
|------|-------------|---------|
| zipcodes.csv | Target geographic areas (84 rows × 5 columns) | ZIP codes, cities, states, distances |
| ELSI_NCES_GA_school_data.csv | NCES foundation data for Georgia schools | Core school information, demographics, facility details |
| AP_2023-24_2025-01-15_15_03_20.csv | Advanced Placement results | College-level coursework performance |
| EOC_2023-24__GA_TST_AGGR_2025-01-14_16_19_30.csv | End-of-Course assessments | Subject-specific achievement metrics |
| EOG_2023-24__GA_TST_AGGR_2025-01-14_16_19_30.csv | End-of-Grade tests | Grade-level proficiency metrics |
| HS_Completer_Credentials_2023-24_2025-01-14_16_45_56.csv | High school completion data | Graduation outcomes, certifications |
| School_FESR_FY24_for_Display.csv | Financial Efficiency Star Ratings | Resource allocation effectiveness |

## Data Processing Pipeline

### 1. Initial Filtering (`enhanced_filter_schools.py`)
- Loads target ZIP codes from `zipcodes.csv`
- Uses intelligent CSV parsing (auto-detection of delimiters and encodings)
- Filters schools to include only those in target ZIP codes
- Outputs `data/cleaned/filtered_nces_schools.csv`

### 2. Data Integration (`merge-school-metrics.py`)
- Creates standardized school identifiers (clean name + ZIP)
- Applies fuzzy matching with 85% similarity threshold
- Uses NCES data as foundation dataset
- Properly merges data from multiple sources using school IDs
- Handles multi-valued metrics with column generation
- Prevents column conflicts with source prefixes
- Outputs `data/aggregated/merged_school_data.csv` (663 schools × 144 metrics)

### 3. Quality Evaluation (`school_quality_metrics_evaluator.py`)
- Analyzes integrated dataset for quality indicators
- Normalizes metrics to allow fair comparison
- Calculates weighted scores across key dimensions
- Assigns distribution-based letter grades (A-F)
- Identifies school-specific strengths and improvement areas
- Outputs `data/aggregated/school_quality_ratings.csv`

## Quality Metrics Framework

The evaluation system uses a weighted model incorporating five dimensions:

### 1. Academic Performance (35% of overall score)
**Raw data**: Proficiency rates, achievement levels, standardized test scores
- `PROFICIENT_PCT` - Students meeting standards
- `DISTINGUISHED_PCT` - Students exceeding standards
- Subject-specific performance indicators

### 2. Resources (15% of overall score)
**Raw data**: Funding metrics, expenditures, teacher-student ratios
- `PPE_Avg` - Per-pupil expenditure
- `Federal_Amt_*` and `State_Local_Amt_*` - Funding allocations
- `Pupil/Teacher Ratio` - Classroom resources

### 3. Equity (15% of overall score)
**Raw data**: Demographic achievement gaps, economically disadvantaged performance
- Free/reduced lunch student metrics
- Direct certification statistics
- Achievement gaps between subgroups

### 4. Environment (10% of overall score)
**Raw data**: School climate, engagement, safety, attendance
- Attendance statistics
- Discipline metrics
- Climate indicators

### 5. Outcomes (10% of overall score)
**Raw data**: Long-term success indicators
- `FESR` - Financial Efficiency Star Rating
- Graduation rates
- College/career readiness metrics

### Scoring Methodology
1. **Normalization**: All metrics converted to 0-100 scale
2. **Weighting**: Category scores weighted by importance percentages
3. **Distribution-Based Grading**:
   - **A**: Top 20% of schools
   - **B**: 60-80th percentile
   - **C**: 40-60th percentile
   - **D**: 20-40th percentile
   - **F**: Bottom 20% of schools

## Usage Instructions

### Data Integration
1. Place all source files in the `/data` directory
2. Run initial filtering:
   ```
   python enhanced_filter_schools.py
   ```
3. Execute the data integration:
   ```
   python proper-merge-school-data.py
   ```

### Quality Evaluation
Run the metrics evaluator on the integrated data:
```
python school-quality-evaluator.py
```

### Output
The final quality ratings are available in `school_quality_ratings.csv`, containing:
- School Name
- ZIP Code
- Quality Score (0-100)
- Letter Grade (A-F)
- Category Scores
- Strengths and Areas for Improvement

---
*This framework provides an objective, data-driven approach to school quality evaluation that adapts to available metrics while maintaining comparability across institutions.*