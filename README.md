import pandas as pd
from datetime import datetime

# Load the dataset
df = pd.read_csv("C:/path/to/your/HRDataset_v14.csv")

# Convert hire and termination dates to datetime
df['DateofHire'] = pd.to_datetime(df['DateofHire'], errors='coerce')
df['DateofTermination'] = pd.to_datetime(df['DateofTermination'], errors='coerce')

# Calculate tenure (in years)
df['Tenure_Years'] = (pd.to_datetime('today') - df['DateofHire']).dt.days / 365
df['Tenure_Years'] = df['Tenure_Years'].round(2)

# Fill NaN termination dates with 'Active'
df['DateofTermination'].fillna('Active', inplace=True)

# Clean or fill other columns if needed (example: satisfaction)
df['EmpSatisfaction'] = df['EmpSatisfaction'].fillna(df['EmpSatisfaction'].mean())

# Output for Power BI
df
