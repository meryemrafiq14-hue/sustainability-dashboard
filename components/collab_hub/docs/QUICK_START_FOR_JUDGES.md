# Quick Start Guide for Judges

> **Everything you need to understand the Collaboration Hub in 5 minutes**

---

## 🎯 **What Is This?**

The **Collaboration Hub** is a supplementary compatibility scoring tool that helps researchers find potential collaborators. It's part of the Illinois Sustainability Impact Engine, a 5-component platform for sustainability research.

**Key Point**: It's a "nice-to-have" enhancement, not a core dependency. The Sustainability Dashboard, Research Coverage Analysis, and Impact Engine work independently.

---

## 📊 **End-to-End Process**

### **Step 1: Original Data**
- **Input**: University publications CSV (`for distribution case competition filtered_publications.csv`)
- **Contains**: Real publication metadata (names, departments, keywords, SDGs, publication years)

### **Step 2: Script 1 - Build Profiles**
- **Script**: `build_collab_hub_from_scratch.py`
- **Does**: Aggregates publications per researcher, infers career stage and method, calculates compatibility scores
- **Output**: `Researcher_Profiles_For_PowerBI.csv` + `Collab_Matches_For_PowerBI.csv`
- **Data**: 100% real (no simulation)

### **Step 3: Script 2 - Generate Demo Data** (Optional)
- **Script**: `generate_ccs_demo_data.py`
- **Does**: Creates curated demo dataset for Power BI presentation
- **Output**: `CCS_Demo_Data.csv`
- **Data**: Real researcher profiles, but 30-40% of user search inputs are varied to show different scenarios

### **Step 4: Power BI Dashboard**
- **Visualization**: Match ranking, score breakdown, filters
- **Integration**: Links to Sustainability Dashboard (SDG wheel), Research Coverage, Impact Engine

---

## ✅ **What's Real vs. Simulated**

### **100% Real** (From Original CSV)
- ✅ All researcher names
- ✅ All departments
- ✅ All publication counts and years
- ✅ All keywords and SDGs
- ✅ All matched researcher data (in demo)

### **Calculated** (Based on Real Data)
- 🧮 Career stage (from years since first publication)
- 🧮 Primary SDG (most frequent)
- 🧮 Primary method (inferred from keywords/abstracts)
- 🧮 Compatibility scores (algorithm: 50% topic, 35% method, 15% career)

### **Simulated** (Demo Data Only)
- ⚠️ User_SDG: 30% varied (to show different search scenarios)
- ⚠️ User_Method: 40% varied (to show different search scenarios)
- ⚠️ Explanation text: Generated from scores + keywords

**Note**: The full pipeline (`Collab_Matches_For_PowerBI.csv`) uses 100% real data with no simulation.

---

## 🔗 **How It Fits with Other Components**

### **Core Components** (Work Independently)
1. **Sustainability Dashboard** - SDG wheel visualization, coverage overview
2. **Research Coverage Analysis** - Gap identification, department-level analysis
3. **Impact Engine** - Impact scores and outcomes

### **Supplementary Components**
4. **Collaboration Hub** ⭐ - Compatibility scoring (this component)
5. **AI Prototype** - Natural language queries

**Integration**: Collaboration Hub enhances discovery tools by adding compatibility scores. For example:
- Researcher discovers SDG coverage in Dashboard → Uses Hub to find collaborators
- Researcher identifies gap in Coverage Analysis → Uses Hub to find researchers who can fill it

**Key Point**: The platform works without Collaboration Hub, but it adds value when researchers want to find collaborators.

---

## 💡 **Value Proposition**

### **For Researchers**
- Save time finding collaborators
- Discover opportunities across departments
- Understand why matches are recommended (transparent scoring)

### **For University Leadership**
- Accelerate research formation
- Identify collaboration opportunities
- Strategic planning with data-driven insights

### **For the Platform**
- Enhances discovery tools
- Adds compatibility scoring layer
- Complements (doesn't replace) existing networking

---

## 🎤 **Elevator Pitch**

> "The Collaboration Hub is a supplementary tool that adds a compatibility scoring layer to help researchers find potential collaborators. It's not a core dependency—the Sustainability Dashboard and Research Coverage Analysis work independently. But when researchers want to find collaborators, the Hub provides transparent, explainable scores based on topic alignment, method complementarity, and career stage fit. It's a 'nice-to-have' enhancement that saves time and accelerates research formation."

---

## 📚 **Where to Learn More**

1. **`END_TO_END_PIPELINE.md`** - Complete data journey, what each script does
2. **`VALUE_PROPOSITION_AND_POSITIONING.md`** - How to sell the idea, positioning
3. **`methodology.md`** - Step-by-step methodology
4. **`judge_qa.md`** - Answers to common questions

---

## ✅ **Key Takeaways**

1. **Supplementary Tool**: Enhances but doesn't block other components
2. **Real Data**: Uses actual university publication data
3. **Transparent**: Rule-based scoring, not predictive AI
4. **Innovation**: Rewards complementary methods, not just similarity
5. **Actionable**: Provides ranked suggestions with explanations

---

**Questions?** See `judge_qa.md` for detailed answers.
