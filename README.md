📘 README.md
Risk Extraction & Knowledge Graphs from Earnings Call Transcripts
This project extracts risk-related statements from earnings call transcripts using an LLM, converts them into structured data, and builds company–risk knowledge graphs to compare pre-subprime (2006) and post-subprime (2008) risk networks.
The workflow combines LLM-based information extraction, data cleaning, graph construction, and network analysis.
🔍 1. Problem Overview
Earnings calls contain rich qualitative information about risks that companies face.
However, these risks are embedded in long, unstructured transcripts.
This project answers:
What risks did firms talk about before and after the subprime crisis?
Which companies or risk types were most central?
How did risk networks change from 2006 to 2008?
📂 2. Dataset
The dataset consists of:
2006 transcripts (pre-subprime crisis)
2008 transcripts (post-crisis)
Each transcript includes:
Transcript ID
Company name
Speaker roles
Full transcript text
Risk statements are extracted automatically using an LLM.
🤖 3. Pipeline Overview
Transcript → LLM Extraction → JSON Parsing → Pandas DataFrame → NetworkX Graph → Analysis
Step 1 — LLM Extraction
A custom prompt instructs the model to return only valid JSON with:
transcript_id
company
speaker_role
risk_type
expectations
JSON cleaning and fallbacks handle malformed model outputs.
Step 2 — Structured Data
Outputs are parsed into a clean DataFrame:
company | risk_type | speaker_role | expectations | transcript_id
Missing values are dropped or cleaned.
Step 3 — Graph Construction
Using NetworkX:
Company nodes
Risk type nodes
Edges = company ↔ risk mention
Attributes = weight (frequency), year
We build:
G_2006 — pre-crisis network
G_2008 — post-crisis network
G_combined — unified graph with year-tagged edges
Step 4 — Network Analysis
We compute:
Degree centrality
Betweenness centrality
Centrality changes from 2006 → 2008
Emerging or disappearing risks
Visualizations include:
Company–risk bipartite graphs
Year-colored edges
Centrality comparison tables
📊 4. Key Results
Certain risk types became more central in 2008, indicating a shift in corporate concerns after the crisis.
Some companies showed increased risk diversity, connecting to more risk categories post-crisis.
Betweenness centrality revealed bridge risk categories linking different parts of the network.
The combined graph visually highlights emerging (red), disappearing (blue), and persistent (purple) risks.
🧠 5. Strengths & Limitations of LLM Extraction
⭐ Strengths
Fast extraction from thousands of sentences
Can infer risk type even when not explicitly stated
Flexible and domain-adaptable
⚠️ Limitations
Occasional JSON format errors
Sometimes outputs speaker names instead of roles
Struggles with long transcripts unless chunked
Requires post-processing (regex, heuristics)
Potential future fixes:
JSON schema enforcement
Role-to-speaker mapping
Transcript chunking with context windows
📦 6. Repository Structure
├── data/                  # Transcripts + extracted CSVs
├── notebooks/             # Jupyter notebooks for extraction + graph analysis
├── graphs/                # Saved graph visualizations
├── README.md              # This file
└── requirements.txt       # Dependencies
▶️ 7. How to Run
Install dependencies:
pip install -r requirements.txt
Run extraction:
python extract_risks.py
Build graphs and run analysis in Jupyter:
jupyter notebook
🖼 8. Outputs
Cleaned CSV with risk statements
Network graphs (PNG)
Centrality change tables
Pre/post-crisis comparison plots
🎥 9. Slide Deck + Video
Slide deck (≤10 slides) includes:
Problem
Dataset
Pipeline
Extraction examples
Knowledge graph
Network analysis
Temporal changes
Key insights
Limitations
Conclusions
Video (≤10 minutes): walkthrough of pipeline, graphs, and findings.
📌 10. Conclusions
The study demonstrates:
LLMs can extract meaningful risk information from financial text
Graph representations reveal changes in corporate risk exposure
Post-crisis networks show increased complexity and emerging risks
LLMs are powerful but require careful validation and cleaning
