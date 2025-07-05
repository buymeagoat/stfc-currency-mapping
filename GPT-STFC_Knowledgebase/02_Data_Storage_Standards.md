### **STFC Knowledgebase Data Storage & Classification Standards - Updated**

---

## **1️⃣ Purpose of this Document**
This document outlines how data should be **stored, classified, and retrieved** within the STFC Knowledgebase AI. The goal is to ensure **structured, accurate, and scalable knowledge management** while maintaining a **clear source tracking system**.

---

## **2️⃣ Core Data Storage Structure**
To maintain consistency, all STFC knowledge should be stored in a **file-based structured format** that allows easy indexing and future migration to a database.

📂 **STFC Knowledgebase (Root Folder)**  
├── `01_Deployment_Training_Guide.md` *(Operational guidelines and role definitions)*  
├── `02_Data_Storage_Standards.md` *(Data structuring rules, classifications, and best practices)*  
├── `03_Testing_Quality_Control.md` *(Protocols for system testing and validation)*  
├── `04_User_Interaction_Guide.md` *(Instructions for user interactions and role-based access control)*  
├── `05_Initial_Knowledgebase_Seed.md` *(Base dataset and foundational game information)*  
├── `06_Game_Mechanics.json` *(Core mechanics, ship stats, economy systems, officer abilities, and combat formulas)*  
├── `07_Faction_Stores.json` *(Faction store inventories, refresh timers, and resource costs)*  
├── `08_Game_Events.json` *(Recurring event structures, milestones, and reward tables)*  
├── `09_Meta_Analysis_Notes.md` *(Strategic insights and evolving gameplay trends)*  
├── `10_Data_Ingestion_Logs.json` *(Source tracking and raw extracted data from external sources)*  
├── `11_Session_Storage_Template.json` *(Temporary user session tracking for fleet, officer progress, and resources)*  
├── `12_Validation_Logs.json` *(AI-detected contradictions, data flagging, and review notes)*  
├── `13_System_Updates.json` *(Change logs and version tracking for AI knowledge updates)*  
├── `14_Conflicts_Log.json` *(Records of knowledgebase conflicts and resolution statuses, including priority ranking for sources)*  
├── `15_Manual_Overrides.json` *(System Architect-approved manual changes to data)*  
├── `16_Last_Ingestion_Timestamp.json` *(Tracks last update for external data sources, now including metadata updates tracking)*  
├── `17_GPT_Required_Files.md` *(Lists all required files GPT must have before answering queries)*  
├── `18_User_Profile_Template.json` *(Template for tracking user game progress and relevant account details)*  
├── `19_Fleet_Progress_Template.json` *(User fleet strength, upgrades, and ship development tracking)*  
└── `20_Officer_Shard_Tracking_Template.json` *(Officer promotion progress, shard tracking, and upgrade timelines, now including deprecated data handling)*  

---

## **3️⃣ Data Classification & Metadata Requirements**
Every stored piece of knowledge should have **metadata attached** for traceability and validation.

✅ **Essential Metadata Fields**  
Each entry within structured knowledge files must include:
- **`category`**: *(Ships, Officers, Events, Refinery, Economy, Combat Mechanics, etc.)*
- **`source`**: *(Official Patch Notes, Developer AMA, Content Creator Video, Community Testing, Reddit Analysis, User Report)*
- **`date_collected`**: *(YYYY-MM-DD of when data was obtained)*
- **`confidence_level`**: *(High - Confirmed, Medium - Community Verified, Low - Unverified)*
- **`cross_references`**: *(Links to related knowledge entries for context validation)*
- **`status`**: *(Current, Deprecated, Pending Verification)*
- **`change_history`**: *(Log of all updates applied to the data entry)*

✅ **New Feature: Dynamic Metadata Expansion**
- AI now **detects missing metadata fields** and dynamically generates placeholders.
- AI logs all newly introduced metadata fields into `16_Last_Ingestion_Timestamp.json`.
- AI flags missing metadata categories for System Trainer review in `12_Validation_Logs.json`.

✅ **New Feature: Deprecated Metadata Handling**
- Instead of deleting outdated knowledge, deprecated entries should include:
```json
{
  "name": "Old Officer Ability",
  "status": "deprecated",
  "deprecated_reason": "Reworked in Patch 2025.03",
  "last_verified": "2025-02-18"
}
```
- AI should no longer use deprecated data for active recommendations.
- Deprecated metadata is stored for **historical reference and system transparency**.

---

## **4️⃣ Handling Missing Files & Conflict Resolution**
To ensure the AI does not provide inaccurate responses due to missing knowledge files or conflicting data, the following protocols must be followed:

✅ **Knowledgebase File Availability Check**
1️⃣ AI must verify that all required files are available before generating responses.
2️⃣ If a required file is missing, AI must **halt processing** and request reattachment before continuing.
3️⃣ System Trainers receive an **automated alert** when a critical file is unavailable.

✅ **Conflict Resolution Priority Rules**
- AI must prioritize data sources as follows:
  - **Highest Trust:** Official Patch Notes, Developer Announcements
  - **Medium Trust:** Community Reports (Verified via multiple sources)
  - **Lowest Trust:** Unverified Data (Flagged for manual review)
- If contradictions exist, AI must defer to the highest trust source.
- All conflicts must be logged in `14_Conflicts_Log.json` for manual validation.

---

## **5️⃣ Knowledge Retrieval & Answer Generation**

✅ **How AI Answers Queries Based on Knowledgebase**
1️⃣ **AI scans structured files** for the most relevant knowledge entry.
2️⃣ **Confidence-based filtering** ensures higher-trust data is prioritized.
3️⃣ **Cross-referencing rules** allow the AI to provide deeper insights.
4️⃣ **Sources are always cited** in responses to ensure transparency.

✅ **New Feature: AI Metadata Logging for Responses**
- AI now **logs metadata sources for each response** in a structured format in `17_GPT_Required_Files.md`.
- Trainers can audit past AI responses to refine metadata quality and prevent incorrect answers.

---

## **🚀 Next Steps: Expanding Metadata Automation & Audits**
✅ Improve AI self-learning for metadata gaps (if frequently missing, AI should propose a standard addition).  
✅ Implement automated metadata audits via `12_Validation_Logs.json` every week.  
✅ Expand deprecated metadata handling to all files ensuring outdated knowledge is archived, not removed.  

By implementing structured metadata expansion, integrity audits, and deprecated knowledge tracking, the STFC Knowledgebase remains **adaptable, accurate, and optimized for long-term reliability.** 🚀

