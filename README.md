📘 Risk Extraction & Knowledge Graphs from Earnings Call Transcripts
This project extracts risk-related statements from earnings call transcripts using an LLM, converts them into structured data, and builds company–risk knowledge graphs to compare pre-subprime (2006) and post-subprime (2008) risk networks.
The workflow combines LLM-based information extraction, data cleaning, graph construction, and network analysis.
1. Problem Overview
Earnings calls contain rich qualitative information about risks that companies face, but these risks are embedded in long, unstructured transcripts.
This project investigates:
What risks firms discussed before vs. after the subprime crisis
Which risks became more central in 2008
How company–risk relations changed
How well LLMs can extract structured risk information from raw text
2. Dataset
The dataset contains earnings call transcripts from:
2006 → before the subprime crisis
2008 → after the crisis
Each transcript includes:
transcript_id
company_name
content (full text)
speaker metadata
Risk statements are extracted via LLM processing.
3. Pipeline Overview
The full processing pipeline is:
Transcript → LLM Extraction → JSON Parsing → DataFrame → NetworkX Graph → Analysis
4. LLM Extraction
A structured prompt instructs the model to return:
transcript_id
company
speaker_role
risk_type
expectations
Post-processing handles:
malformed JSON
duplicate items
quotes, commas, and formatting issues
The result is a consistent, machine-usable dataset.
5. Structured Dataset
After extraction and cleaning, each row contains:
transcript_id | company | speaker_role | risk_type | expectations
This allows aggregations such as:
risk distributions
company–risk pairs
sentiment analysis
year-over-year comparisons
6. Knowledge Graph Construction
Two bipartite graphs are created:
G_2006 (pre-crisis)
G_2008 (post-crisis)
Nodes:
company (type="company")
risk_type (type="risk")
Edges:
company ↔ risk
weight = frequency
year = 2006 or 2008
A combined graph G_combined is created with year-tagged edges, allowing:
blue edges → only 2006
red edges → only 2008
purple edges → appear in both
7. Network Analysis
We compute:
degree centrality → most connected nodes
betweenness centrality → bridging risk categories
centrality changes from 2006 to 2008
risk emergence and disappearance
We identify:
new risk types in 2008
companies whose risk exposure expanded
stable vs. shifting risk structures
8. Key Visualizations
The project produces several figures, including:
Company–Risk Bipartite Graphs for 2006 and 2008
Combined Graph With Year Coloring (blue = 2006, red = 2008, purple = both)
Degree & Betweenness Centrality Rankings
Centrality Change Table
Distribution of Risk Types
Company-Level Risk Profiles
These visualizations highlight how risk structures and corporate concerns evolved between the two periods.
9. Strengths & Limitations of LLM-Based Extraction
Strengths
Fast and flexible extraction
Detects implied risk categories
Converts long text into structured form
Limitations
JSON errors and hallucinations
Difficulty enforcing consistent speaker roles
Sensitive to prompt wording
Requires cleaning and validation
10. Conclusion
This project demonstrates that:
LLMs can extract structured risk information effectively
Knowledge graphs provide a powerful tool for comparing time periods
Post-crisis networks show increased risk complexity
Companies connect to more diverse risk types in 2008
LLMs require careful prompt engineering and validation

My recording can be accessed at the following link:
https://aaudk.sharepoint.com/:v:/s/Solo_gi48db/IQBtzx3tqfAQTqkvDo4g__mpAdmZS2gnjbTWZxuWmcUy9B0?e=DwrQLS
