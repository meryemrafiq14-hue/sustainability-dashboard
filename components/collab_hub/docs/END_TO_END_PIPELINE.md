# End-to-End Pipeline: From University CSV to Power BI MVP

> **Complete documentation of the data journey from original university publications data to the Collaboration Hub Power BI dashboard**

---

## 🎯 **End Goal: Sustainability Research Impact**

**Mission**: Enable the university to accelerate sustainability research by:
- **Discovering** existing expertise across departments
- **Connecting** researchers with complementary skills
- **Visualizing** research coverage and gaps across 17 UN SDGs
- **Facilitating** interdisciplinary collaboration

**Collaboration Hub Role**: A **supplementary tool** that provides compatibility scores to help researchers find potential collaborators. It's a "nice-to-have" enhancement, not a core dependency—the Sustainability Dashboard, Research Coverage Analysis, and Impact Engine work independently.

---

## 📊 **Complete Data Pipeline**

```
┌─────────────────────────────────────────────────────────────────┐
│  STEP 0: Original University Data                               │
│  ─────────────────────────────────────────────────────────────  │
│  File: for distribution case competition filtered_publications.csv│
│  Type: Real publication metadata from university                 │
│  Rows: ~X,XXX publications                                       │
│  Fields: name, department, publication_year, keywords, SDGs, etc.│
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  STEP 1: Data Cleaning & Validation                             │
│  ─────────────────────────────────────────────────────────────  │
│  Script: build_collab_hub_from_scratch.py (Lines 23-39)         │
│  Actions:                                                        │
│  • Validate publication years (1900-2026)                        │
│  • Clean SDG columns (must be 1-17)                             │
│  • Convert is_sustain to boolean                                 │
│  Output: Cleaned publications dataframe                         │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  STEP 2: Researcher Profile Construction                        │
│  ─────────────────────────────────────────────────────────────  │
│  Script: build_collab_hub_from_scratch.py (Lines 42-159)        │
│  Process: Aggregate all publications per person_uuid            │
│                                                                  │
│  REAL DATA (from original CSV):                                  │
│  ✓ Researcher names                                              │
│  ✓ Departments                                                   │
│  ✓ Total publications count                                      │
│  ✓ Publication years (first, last)                                │
│  ✓ Keywords (aggregated from all publications)                   │
│  ✓ SDGs (from top 1, top 2, top 3 columns)                      │
│                                                                  │
│  INFERRED/CALCULATED:                                            │
│  • Career stage (calculated from years_since_first)              │
│  • Primary SDG (most frequent across publications)              │
│  • Primary method (inferred from keywords + abstracts)           │
│  • Top keywords (frequency-ranked)                               │
│                                                                  │
│  Output: Researcher_Profiles_For_PowerBI.csv                    │
│  Rows: One per researcher                                        │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  STEP 3: Compatibility Score Calculation                        │
│  ─────────────────────────────────────────────────────────────  │
│  Script: build_collab_hub_from_scratch.py (Lines 164-280)      │
│  Process: Calculate pairwise compatibility for all researchers  │
│                                                                  │
│  Scoring Formula:                                                │
│  CCS_Total = (Topic × 50%) + (Method × 35%) + (Career × 15%)    │
│                                                                  │
│  Sub-scores:                                                     │
│  • Topic Score: SDG alignment (70%) + keyword overlap (30%)     │
│  • Method Score: Complementarity matrix (different = higher)    │
│  • Career Score: Mentorship/peer opportunities                  │
│                                                                  │
│  Output: Collab_Matches_For_PowerBI.csv                        │
│  Rows: All pairwise combinations with scores                    │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  STEP 4: Demo Data Generation (Optional - for Presentation)    │
│  ─────────────────────────────────────────────────────────────  │
│  Script: generate_ccs_demo_data.py                              │
│  Purpose: Create controlled demo dataset for Power BI           │
│                                                                  │
│  REAL DATA USED:                                                 │
│  ✓ All researcher names (from profiles)                        │
│  ✓ All departments                                              │
│  ✓ All matched researcher attributes (SDG, method, stage)       │
│  ✓ Top keywords (for explanations)                              │
│                                                                  │
│  SIMULATED/VARIED:                                               │
│  ⚠️ User_SDG: 30% varied to show different search scenarios    │
│  ⚠️ User_Method: 40% varied to show different search scenarios │
│  ✓ All scores: Calculated using same algorithm as real data    │
│  ✓ Explanations: Generated using real keywords + calculated     │
│                                                                  │
│  Output: CCS_Demo_Data.csv                                      │
│  Rows: ~46 curated matches for presentation                     │
└─────────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────────┐
│  STEP 5: Power BI Dashboard Integration                         │
│  ─────────────────────────────────────────────────────────────  │
│  Platform: Microsoft Power BI                                  │
│  Data Source: CCS_Demo_Data.csv (for demo) OR                  │
│               Collab_Matches_For_PowerBI.csv (for full data)    │
│                                                                  │
│  Visualizations:                                                │
│  • Match ranking table (sorted by CCS_Total)                    │
│  • Score breakdown (Topic, Method, Career)                      │
│  • Filter by department, SDG, method, career stage              │
│  • Explanation text for each match                              │
│                                                                  │
│  Integration:                                                    │
│  • Links to Sustainability Dashboard (SDG context)              │
│  • Links to Research Coverage (gap identification)             │
│  • Links to Impact Engine (collaboration outcomes)              │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📋 **What Each Script Does**

### **Script 1: `build_collab_hub_from_scratch.py`**

**Purpose**: Core pipeline that transforms raw publications into researcher profiles and compatibility scores.

**Input**: 
- `for distribution case competition filtered_publications.csv` (original university data)

**Process**:
1. **Data Cleaning** (Lines 23-39)
   - Validates publication years
   - Cleans SDG columns
   - Converts data types

2. **Profile Construction** (Lines 42-159)
   - Groups publications by `person_uuid`
   - Aggregates metrics (total pubs, years active, etc.)
   - Infers career stage from publication history
   - Infers research method from keywords/abstracts
   - Aggregates SDGs and keywords

3. **Compatibility Scoring** (Lines 164-280)
   - Calculates pairwise compatibility for all researcher pairs
   - Applies scoring formula (50/35/15 weights)
   - Generates explanations

**Output**:
- `Researcher_Profiles_For_PowerBI.csv` - One row per researcher
- `Collab_Matches_For_PowerBI.csv` - All pairwise matches with scores

**Key Point**: This script uses **100% real data** from the original CSV. No simulation.

---

### **Script 2: `generate_ccs_demo_data.py`**

**Purpose**: Creates a curated demo dataset for Power BI presentation.

**Input**: 
- `Researcher_Profiles_For_PowerBI.csv` (from Script 1)

**Process**:
1. **Filter Top Researchers** (Lines 25-69)
   - Selects researchers with ≥5 publications
   - Ensures variety across career stages
   - Selects 15 "user" researchers

2. **Generate Matches** (Lines 200-280)
   - For each user, finds potential matches
   - **70% use actual primary_sdg** for user, **30% vary** (to show different scenarios)
   - **60% use actual primary_method** for user, **40% vary**
   - **100% use actual career_stage** for user
   - **100% use actual data** for all matched researchers
   - Calculates scores using same algorithm as Script 1

3. **Generate Explanations** (Lines 161-195)
   - Uses real keywords from matched researcher
   - Generates text based on calculated scores

**Output**:
- `CCS_Demo_Data.csv` - ~46 curated matches for presentation

**Key Point**: Demo data uses **real researcher profiles** but varies some user inputs to show diverse scenarios. All matched researcher data is real.

---

## 🔍 **What's Real vs. Simulated**

### ✅ **100% Real (From Original CSV)**

| Data Element | Source | Used In |
|--------------|--------|---------|
| Researcher names | `name` column | All outputs |
| Departments | `department` column | All outputs |
| Publication counts | Aggregated from rows | Researcher profiles |
| Publication years | `publication_year` column | Career stage calculation |
| Keywords | `keywords` column | Profile aggregation, explanations |
| SDGs | `top 1`, `top 2`, `top 3` columns | Profile aggregation, scoring |
| Abstracts | `abstract` or `abstract_text` | Method inference |

### 🧮 **Calculated/Inferred (Based on Real Data)**

| Data Element | How It's Derived | Used In |
|--------------|------------------|---------|
| Career stage | Years since first publication | Scoring, profiles |
| Primary SDG | Most frequent SDG across publications | Scoring, profiles |
| Primary method | Keyword matching in abstracts/keywords | Scoring, profiles |
| Top keywords | Frequency ranking | Explanations |
| Compatibility scores | Algorithm (50/35/15 formula) | All outputs |

### ⚠️ **Simulated (Only in Demo Data)**

| Data Element | Why Simulated | Used In |
|--------------|---------------|---------|
| User_SDG (30% varied) | Show different search scenarios | Demo data only |
| User_Method (40% varied) | Show different search scenarios | Demo data only |
| Explanation text | Generated from scores + keywords | Demo data only |

**Important**: The full pipeline (`Collab_Matches_For_PowerBI.csv`) uses **100% real data** with no simulation.

---

## 🎨 **Power BI MVP Setup**

### **Data Connection**

1. **For Demo Dashboard** (recommended for presentation):
   - Connect to `CCS_Demo_Data.csv`
   - Shows curated examples with clear explanations

2. **For Full Dashboard** (production):
   - Connect to `Collab_Matches_For_PowerBI.csv`
   - Shows all possible matches

### **Key Visualizations**

1. **Match Ranking Table**
   - Sortable by CCS_Total
   - Shows: User Name, Match Name, Scores, Explanation
   - Filters: Department, SDG, Method, Career Stage

2. **Score Breakdown**
   - Bar chart: Topic, Method, Career scores
   - Shows why each match scored as it did

3. **Integration Points**
   - **Sustainability Dashboard**: Click SDG → see research coverage
   - **Research Coverage**: Click gap → see potential collaborators
   - **Impact Engine**: See collaboration outcomes

### **DAX Measures** (if needed)

See `DAX_Measures.txt` for calculated fields like:
- `Total Publications`
- `Sustainable Publications %`
- `Publications by SDG`
- `Impact Story`

---

## 🔗 **How Collaboration Hub Fits with Other Components**

### **Platform Architecture**

```
┌─────────────────────────────────────────────────────────────┐
│         Illinois Sustainability Impact Engine                │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────┐  ┌──────────────────┐                  │
│  │ Sustainability   │  │   Research       │                  │
│  │   Dashboard      │  │   Coverage       │                  │
│  │                  │  │   Analysis       │                  │
│  │ • SDG Wheel      │  │                  │                  │
│  │ • Coverage Map   │  │ • Gap Analysis  │                  │
│  │ • Trends         │  │ • Department     │                  │
│  └──────────────────┘  └──────────────────┘                  │
│                                                               │
│  ┌──────────────────┐  ┌──────────────────┐                 │
│  │   Impact         │  │   Collaboration  │                 │
│  │   Engine         │  │   Hub            │                 │
│  │                  │  │                  │                 │
│  │ • Impact Scores  │  │ • CCS Scores     │                 │
│  │ • Outcomes       │  │ • Match Ranking  │                 │
│  └──────────────────┘  └──────────────────┘                 │
│                                                               │
│  ┌──────────────────┐                                       │
│  │   AI Prototype   │                                       │
│  │                  │                                       │
│  │ • NLP Queries    │                                       │
│  └──────────────────┘                                       │
└─────────────────────────────────────────────────────────────┘
```

### **Component Relationships**

1. **Sustainability Dashboard** (Core)
   - **Primary function**: Visualize research coverage across 17 SDGs
   - **SDG Wheel**: Interactive visualization showing coverage
   - **Standalone**: Works independently
   - **Integration**: Collaboration Hub can link to specific SDGs

2. **Research Coverage Analysis** (Core)
   - **Primary function**: Identify gaps and strengths
   - **Standalone**: Works independently
   - **Integration**: Collaboration Hub can suggest collaborators for under-researched SDGs

3. **Impact Engine** (Core)
   - **Primary function**: Measure research impact
   - **Standalone**: Works independently
   - **Integration**: Can measure impact of collaborations suggested by Hub

4. **Collaboration Hub** (Supplementary)
   - **Primary function**: Provide compatibility scores for finding collaborators
   - **Role**: "Nice-to-have" enhancement, not core dependency
   - **Value**: Adds a compatibility scoring layer on top of discovery
   - **Integration**: Enhances other components but doesn't block them

5. **AI Prototype** (Supplementary)
   - **Primary function**: Natural language queries
   - **Role**: Experimental interface
   - **Integration**: Can query Collaboration Hub results

### **Key Positioning**

**Collaboration Hub is NOT**:
- ❌ A core dependency (other components work without it)
- ❌ A replacement for manual networking
- ❌ A predictive AI system

**Collaboration Hub IS**:
- ✅ A supplementary tool that provides compatibility scores
- ✅ A "nice-to-have" enhancement for finding collaborators
- ✅ A transparent, explainable scoring system
- ✅ An optional layer on top of discovery tools

---

## 📈 **Value Proposition**

### **For Researchers**
- **Discover** potential collaborators with complementary skills
- **Understand** why a match is recommended (transparent scoring)
- **Save time** by getting ranked suggestions instead of manual search

### **For University Leadership**
- **Accelerate** sustainability research through better collaboration
- **Identify** collaboration opportunities across departments
- **Measure** impact of interdisciplinary partnerships

### **For the Platform**
- **Enhances** discovery tools (Dashboard, Coverage Analysis)
- **Adds** a compatibility scoring layer
- **Complements** (doesn't replace) existing networking

---

## 🎯 **How to Sell the Idea**

### **Elevator Pitch**

"The Collaboration Hub is a supplementary tool that adds a compatibility scoring layer to help researchers find potential collaborators. It's not a core dependency—the Sustainability Dashboard and Research Coverage Analysis work independently. But when researchers want to find collaborators, the Hub provides transparent, explainable scores based on topic alignment, method complementarity, and career stage fit."

### **Key Selling Points**

1. **Transparency**: Every score is explainable (not a black box)
2. **Innovation**: Rewards complementary methods, not just similarity
3. **Supplementary**: Enhances but doesn't block other components
4. **Real Data**: Uses actual university publication data
5. **Actionable**: Provides ranked suggestions with explanations

### **For Judges**

- **What it does**: Provides compatibility scores for collaboration recommendations
- **How it works**: Rule-based scoring (50% topic, 35% method, 15% career)
- **What's real**: All researcher data from original CSV
- **What's simulated**: Only user search inputs in demo data (30-40% variation)
- **Integration**: Works with other components but is supplementary

---

## ✅ **Summary**

**End-to-End Flow**:
1. Original CSV → Data cleaning → Researcher profiles → Compatibility scores → Power BI

**What's Real**:
- All researcher data (names, departments, publications, SDGs, keywords)

**What's Calculated**:
- Career stage, primary SDG, primary method, compatibility scores

**What's Simulated** (demo only):
- 30-40% of user search inputs (to show variety)

**Positioning**:
- Supplementary tool, not core dependency
- "Nice-to-have" enhancement for finding collaborators
- Works with other components but doesn't block them

**Value**:
- Transparent, explainable compatibility scores
- Saves time in finding collaborators
- Accelerates sustainability research through better connections
