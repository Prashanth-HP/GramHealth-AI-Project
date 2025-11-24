# GramHealth-AI-Project
GramHealth AI is an offline, bilingual (English/Tamil) Streamlit app designed for preliminary health screening. It predicts diseases based on user symptoms and provides immediate first aid advice using a local knowledge base. Key features include secure user authentication, symptom search, and downloadable PDF patient reports.

1. Application Architecture (app.py)
The main application logic handles user authentication, UI rendering, and report generation.

Authentication: The app includes a login and sign-up system. It verifies credentials against a local database (users.json) using SHA-256 hashing.

Bilingual UI: The interface toggles between English and Tamil. It uses a dictionary ui_strings to map labels like "Get Analysis" to "ஆய்வு செய்யவும்".

Symptom Input: Users can select symptoms from a dropdown or type them manually. The dropdown options are populated from processed_dataset.csv and translated using symptom.json.

Prediction Logic: The app attempts to load a machine learning model (gramhealth_ai_model.joblib) to predict disease probabilities based on input symptoms. Note: The .joblib model file was not included in your upload.

PDF Generation: The app generates a downloadable PDF report containing patient details, predicted conditions, and medical advice using the FPDF library.

2. Knowledge Base (knowledge_base.json)
This JSON file acts as the medical logic layer, providing static content for 39 specific conditions.

Content: For each disease (e.g., Dengue Fever, Snake Bite, Anemia), it provides:

Description: Bilingual descriptions of the condition.

First Aid: Actionable steps (e.g., "Hydrate with ORS" for Dengue).

Doctor Advice: Specific triggers for when to seek professional help (e.g., "IMMEDIATELY if bleeding occurs").

3. Data Sources
processed_dataset.csv: This file maps diseases to their associated symptoms. For example, "Dengue Fever" is mapped to symptoms like high fever, severe headache, and pain behind eyes. It is used to populate the symptom selection list in the app.

symptom.json: This is a translation dictionary used to display symptoms in Tamil within the UI (e.g., mapping "abdominal pain" to "வயிற்று வலி").

users.json: A simplistic database storing usernames and their hashed passwords. Currently, it contains users "Hari", "admin", and "ad".

4. Observations & Potential Issues
Based on the code review, here are a few technical points to consider:

Missing Model File: The application relies on gramhealth_ai_model.joblib to perform the actual prediction. Without this file, the app will throw an error upon loading resources.

PDF Character Encoding: The PDF generation function uses latin-1 encoding: symptoms.encode('latin-1', 'ignore'). This effectively strips out non-English characters. Consequently, the Tamil text found in knowledge_base.json will not appear in the generated PDF report.

Data Cleaning: The processed_dataset.csv contains citation artifacts (e.g., ``) inside the text fields. These might appear in the UI dropdowns unless cleaned by the comma_tokenizer function.
