# AI Safety Agent – Work Permit Cross-Checker for Power Grid Field Work

Building AI course project

Summary

AI Safety Agent reads three safety documents prepared for the same power line job – the site survey report, the work permit and the construction method plan – and automatically flags inconsistencies (wrong location, missing earthing points, mismatched crew or titles) before workers go on site.

Background

In electrical distribution companies, every job on or near live equipment requires a set of safety documents:

Site survey report – what the crew found on site: hazards, equipment, earthing positions
Work permit – who works where, when, and which safety measures are applied
Construction method plan – how the job is done step by step and how risks are controlled

These three documents must be consistent with each other. In practice, safety inspectors often find problems such as:

the work location in the permit differs from the survey report
earthing points or isolation measures listed in the plan are missing from the permit
crew members or their safety titles differ between documents
the risk assessment is copied from older jobs and does not match the actual site

Hundreds of permits are issued every month across many district units, and inspectors can only check a sample by hand. A mismatch that is missed can lead to someone working on the wrong line section or without proper earthing – one of the most serious causes of electrical accidents.

Personal motivation: I work as Deputy Head of the Safety Department at a regional power company in Vietnam. Checking these documents is part of my daily work, and I want a tool that lets inspectors spend their time on the high-risk cases instead of reading every page manually.

How is it used?
A team leader or safety officer uploads the three PDF documents for one job.
The agent extracts the key fields from each document: job location, line/feeder name, equipment IDs, isolation and earthing points, crew list and titles, dates and times, identified hazards.
It compares the fields across documents and produces a report with three levels:
Red – critical mismatch, the job should not start (e.g. different location, missing earthing)
Yellow – incomplete or unclear information to be corrected
Green – consistent
The safety inspector reviews the report and makes the final decision.

Users:

Safety inspectors at company level – screening many permits quickly
Team leaders and permit issuers at district units – self-checking before submission
Field workers – indirectly, by receiving safer and more accurate permits

The tool runs as a small desktop program on Windows and as a single HTML page that works in a phone or tablet browser without installation, so it can also be used in the field.

Data sources and AI methods
Item	Description
Data	Real PDF work permits, survey reports and method plans from the company's safety management workflow (used internally, not published)
Text extraction	PDF text extraction; OCR for scanned pages
Field extraction	Rule-based patterns combined with a large language model (LLM) to read semi-structured Vietnamese text
Comparison	Normalisation of names and IDs, then fuzzy matching and rule checks against company safety regulations
Future learning	A classifier trained on documents labelled by inspectors to predict which permits are high-risk and should be checked first (supervised learning)

Because the documents contain internal and personal information, only anonymised examples would be shared publicly.

Challenges
The tool does not replace the inspector. It flags issues; responsibility and final decisions remain with qualified people.
Data quality: scanned, handwritten or poorly formatted documents reduce extraction accuracy.
False confidence: a "green" result does not guarantee the site is safe – conditions on site can differ from what is written.
Privacy: documents contain names of workers; data must stay inside the company and be handled according to its rules.
Changing regulations: the rule set must be updated whenever safety regulations change.
LLM errors: language models can misread or invent details, so every red/yellow flag shows the original text it is based on.
What next?
Add the photo check: verify that the required site photos are present and show the right equipment
Connect directly to the company's safety management software instead of uploading PDFs
Collect inspector feedback on each flag to measure precision and recall, and to train a risk-ranking model
Extend the checks to contractors' documents and to daily safety briefing records
Needed: help from software developers for integration, and from colleagues to build a labelled dataset
Acknowledgments
Elements of AI and Building AI courses by the University of Helsinki and MinnaLearn
Safety regulations of the Vietnamese Ministry of Industry and Trade and of the power corporation, which define the consistency rules
Colleagues in the safety department whose inspection experience defined the most common errors
Prototype developed with the help of the AI assistant Claude (Anthropic)
