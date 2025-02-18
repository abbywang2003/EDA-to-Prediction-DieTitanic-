# EDA-to-Prediction-DieTitanic-
# 🚢 Titanic Survival Analysis

A comprehensive analysis of the Titanic dataset using Python, focusing on survival patterns and passenger demographics.

## 📊 Analysis Workflow

```mermaid
graph TD
    A[Data Loading] -->|Read CSV| B[Initial Analysis]
    B --> C[Missing Values Check]
    C --> D[Feature Analysis]
    D --> E[Data Visualization]
    E --> F[Insights Generation]
    
    B --> G[Survival Overview]
    B --> H[Demographic Analysis]
    
    style A fill:#e1f5fe
    style B fill:#e1f5fe
    style C fill:#fff3e0
    style D fill:#e1f5fe
    style E fill:#f3e5f5
    style F fill:#f1f8e9
    style G fill:#e8eaf6
    style H fill:#e8eaf6
```

## 🛠️ Dependencies

```python
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('fivethirtyeight')
```

## 📋 Feature Types

```mermaid
mindmap
    root((Titanic Features))
        Categorical
            Sex
            Embarked
        Ordinal
            Pclass
        Continuous
            Age
        Derived
            Initial(from Name)
```

## 🔍 Analysis Components

### 1. Survival Overview

```mermaid
pie
    title Survival Distribution
    "Did Not Survive" : 61.6
    "Survived" : 38.4
```

```python
f,ax=plt.subplots(1,2,figsize=(18,8))
data['Survived'].value_counts().plot.pie(explode=[0,0.1],autopct='%1.1f%%',ax=ax[0],shadow=True)
```

### 2. Demographic Analysis Pipeline

```mermaid
flowchart LR
    A[Sex Analysis] --> E[Visualizations]
    B[Class Analysis] --> E
    C[Age Analysis] --> E
    D[Embarkation Analysis] --> E
    
    E --> F{Insights}
    F --> G[Sex vs Survival]
    F --> H[Class vs Survival]
    F --> I[Age vs Survival]
    F --> J[Port vs Survival]
    
    style A fill:#f3e5f5
    style B fill:#f3e5f5
    style C fill:#f3e5f5
    style D fill:#f3e5f5
    style E fill:#e1f5fe
    style F fill:#fff3e0
```

## 📈 Key Visualizations

### 1. Gender Analysis
```python
f,ax=plt.subplots(1,2,figsize=(18,8))
data[['Sex','Survived']].groupby(['Sex']).mean().plot.bar()
```

### 2. Class Analysis
```python
pd.crosstab(data.Pclass,data.Survived,margins=True)
```

### 3. Age Distribution
```python
sns.violinplot("Pclass","Age", hue="Survived", data=data,split=True)
```

### 4. Embarkation Analysis
```python
sns.factorplot('Embarked','Survived',data=data)
```

## 🔧 Data Processing Steps

```mermaid
flowchart TD
    A[Raw Data] -->|Extract Initials| B[Name Processing]
    B -->|Replace Values| C[Initial Cleanup]
    C -->|Fill NaN| D[Age Imputation]
    D -->|Handle Missing| E[Embarked Cleanup]
    
    style A fill:#e3f2fd
    style B fill:#e3f2fd
    style C fill:#e3f2fd
    style D fill:#e3f2fd
    style E fill:#e3f2fd
```

### Initial Extraction
```python
data['Initial']=data.Name.str.extract('([A-Za-z]+)\.')
```

### Age Imputation
```python
# Mean age by Initial title
data.groupby('Initial')['Age'].mean()

# Fill missing values
data.loc[(data.Age.isnull())&(data.Initial=='Mr'),'Age']=33
data.loc[(data.Age.isnull())&(data.Initial=='Mrs'),'Age']=36
```

## 📊 Key Findings

```mermaid
graph TD
    A[Survival Rate: 38.4%] --> B[Gender Impact]
    A --> C[Class Impact]
    A --> D[Age Impact]
    A --> E[Port Impact]
    
    B --> F[Female Higher Survival]
    C --> G[1st Class Advantage]
    D --> H[Children Priority]
    E --> I[Port C Highest Rate]
    
    style A fill:#e1f5fe
    style B fill:#e1f5fe
    style C fill:#e1f5fe
    style D fill:#e1f5fe
    style E fill:#e1f5fe
    style F fill:#f3e5f5
    style G fill:#f3e5f5
    style H fill:#f3e5f5
    style I fill:#f3e5f5
```

## 📝 Statistical Highlights

- **Age Range**: 0.42 to 80 years
- **Average Age**: ~29.7 years
- **Class Distribution**: 
  - 1st Class: 24.2%
  - 2nd Class: 20.3%
  - 3rd Class: 55.5%

## 🎯 Usage

1. Install required libraries:
```bash
pip install pandas numpy matplotlib seaborn
```

2. Load and prepare data:
```python
data = pd.read_csv('train.csv')
```

3. Run analysis cells in order:
   - Data cleaning
   - Feature extraction
   - Visualization generation
   - Statistical analysis

## 📌 Notes

- All visualizations use seaborn and matplotlib
- Missing values are handled systematically
- Age imputation is based on passenger title
- Port of embarkation missing values are filled with most common value ('S')

---
*This README uses Mermaid diagrams for visualization. Ensure your Markdown viewer supports Mermaid syntax.*
