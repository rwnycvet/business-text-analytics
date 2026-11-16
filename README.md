# Business Text Analytics with Python

**A reproducible NLP workflow for exploring text, entities, and sentiment.**

Built by Richard Watson Jr.

This project uses NLTK and TextBlob to analyze 12 short passages about
*I, Robot*. It shows how text cleaning, stemming, lemmatization,
part-of-speech tagging, named entity recognition, and sentiment scoring
produce different views of the same text and where their outputs need review.

- **Analysis:** [sba927_analysis.py](sba927_analysis.py)
- **Dataset:** [SBA927.txt](SBA927.txt)
- **Recorded output:** [SBA927_results.txt](SBA927_results.txt)
- **Coursework report:** [docs/coursework/report.docx](docs/coursework/report.docx)

## How it works

1. Loads one passage per line from `SBA927.txt`.
2. Tokenizes and lowercases the text, removes punctuation and stop words,
   and retains `no`, `not`, and `nor`. It expands the dataset's `doesn't`
   to `does not` before filtering.
3. Applies Porter stemming and WordNet lemmatization using its default
   noun setting.
4. Runs POS tagging and named entity recognition on the original text.
5. Prints TextBlob polarity scores for passages 5, 8, and 12.
6. Writes token, stem, lemma, POS, and entity results for all 12 passages
   to `SBA927_results.txt`.

The script runs locally without an API key. The language-model prompt
experiments in the report were performed separately from the Python script.

## Run locally

You need Python 3 with pip and internet access for the initial package and
NLTK resource downloads. Clone or download the repository, then open a
terminal in the repository folder.

### Windows PowerShell

```powershell
git clone https://github.com/rwnycvet/SBA-927-Business-Text-Analytics.git
cd SBA-927-Business-Text-Analytics
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe sba927_analysis.py
```

If Python is available as `py`, use `py -m venv .venv` for environment creation.
The commands call the virtual environment directly, so activation is optional.

### macOS or Linux

```bash
git clone https://github.com/rwnycvet/SBA-927-Business-Text-Analytics.git
cd SBA-927-Business-Text-Analytics
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python sba927_analysis.py
```

The script downloads its NLTK resources as needed. Run it from the repository
root: input and output paths are relative to the current working directory.
Each run replaces `SBA927_results.txt`; sentiment scores appear in the terminal.

## Recorded findings

| Example | Observed result | Why it matters |
|---|---|---|
| Negation | Sonny's passage keeps `not` in the cleaned tokens. | Removing negation can reverse meaning. |
| Stemming | `investigates` becomes `investig`. | Stems group variants but may not be dictionary words. |
| Lemmatization | `serves` becomes `serf`; `leaves` becomes `leaf`. | Treating every token as a noun can select the wrong lemma. |
| Named entities | `Susan Calvin` is labeled `PERSON`; `Sonny` is labeled `GPE` in passage 11. | Entity labels need contextual checks. |
| Sentiment | Passage 5 scores `+0.200` despite its sinister turn. | Positive numeric polarity can conflict with overall meaning. |

The recorded sentiment scores are `+0.200`, `-0.033`, and `0.000` for
passages 5, 8, and 12 respectively. The report explains the comparison with
manual judgments and prompt-based analysis.

## Project structure

| Path | Purpose |
|---|---|
| `sba927_analysis.py` | Python NLP workflow |
| `SBA927.txt` | Twelve supplied passages |
| `SBA927_results.txt` | Recorded per-passage output |
| `requirements.txt` | NLTK and TextBlob dependencies |
| `.gitignore` | Excludes local environments, caches, and credentials |
| `docs/coursework/report.docx` | Original assessment report and results appendix |

## Limitations

- The dataset is a small movie-text example, not a representative customer
  feedback collection. Business applications would need relevant data.
- No reference sentiment labels are supplied. The comparisons are qualitative,
  not benchmark accuracy measurements, and no model was fine-tuned.
- Contraction expansion covers the supplied `doesn't` example rather than
  general English contractions. Alphabetic filtering removes dotted names
  such as V.I.K.I. from cleaned tokens; NER uses the original text.
- Default noun lemmatization and pretrained POS/NER models can make errors,
  including incorrect word senses and inconsistent entity labels.
- Dependency and NLTK resource versions can affect outputs. The committed
  results preserve the assessment run.

## Troubleshooting

- **Dataset not found:** run from the repository root and keep the filename
  exactly `SBA927.txt`.
- **Missing module:** install `requirements.txt` with the interpreter used to
  run the script.
- **NLTK resource unavailable:** check the download connection and rerun.
- **Report preview unavailable:** download the Word document to read it.

## Background and AI assistance

This project began as Per Scholas SBA 927. The original coursework report is
retained under `docs/coursework`, and the repository URL is retained for the
submitted assignment. I used ChatGPT (OpenAI) for explanations, code examples,
debugging guidance, report preparation, and repository documentation. I ran the
script locally and reviewed its outputs during the assessment.
