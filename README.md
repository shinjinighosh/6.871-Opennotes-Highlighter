# MedicationExplainer

Final Project for 6.871 Machine Learning for Healthcare, Spring 2021

## Vibha Agarwal, Shinjini Ghosh, Stuti Khandwala, Anil Palepu

Presenting and explaining discharge medications through web-scraping and basic NLP

You will need the following data to run medicineExplainerFinal.ipynb. While the notebook expects this data in the base folder of your google drive, the name and location of files can be customized with minor modification to the notebook.

1) Data.csv. For MIMIC III, this file can be generated with the following SQL query: \\
SELECT p.subject_id, a.hadm_id, p.expire_flag, n.category, n.text\\
FROM physionet-data.mimiciii_clinical.admissions a\\
INNER JOIN physionet-data.mimiciii_clinical.patients p\\
    ON p.subject_id = a.subject_id\\
LEFT JOIN physionet-data.mimiciii_notes.noteevents n \\
    ON n.hadm_id = a.hadm_id \\
WHERE n.category is not null \\
AND p.subject_id &lt; 2000 \\
AND p.expire_flag = 0 \\
AND (n.category = 'Discharge summary' or n.category = 'Discharge Summary') \\
GROUP BY p.subject_id, a.hadm_id, p.expire_flag, n.category, n.text \\
ORDER BY p.subject_id, a.hadm_id

2.  corpus.pickle. Run get_corpora.ipynb

medicineExplainerFinal.ipynb could also be used with discharge summaries from other sources. It only expects two columns: hadm_id and text, which have the patients ID and the text in their discharge summary.\\
get_keywords.ipynb is a separate notebook that may be used in the absence of discharge summaries to get keywords for inputted medication, condition pairs.
