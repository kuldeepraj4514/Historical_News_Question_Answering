# Historical News Question Answering

***Project Status:** Completed (academic project 2025)*

## Project overview
The goal of this project is to develop a specialized search engine capable of retrieving and ranking historical newspaper passages from the *Chronicling America* digitized archive (1800-1920). The system is designed to answer factoid natural language questions by navigating the complexities of historical data, such as archaic language and temporal ambiguity.

A key focus of the study was evaluating the **"OCR gap"** (the performance degradation caused by noisy Optical Character Recognition) and implementing a multi-stage pipeline to boost retrieval accuracy through neural re-ranking and metadata analysis.

## Technologies and Tools
* **Language:** Python (google Colab environment)
* **Libraries:** PyTerrier, sentence-transformers
* **Techniques:** BM25, TF-IDF, neural cross-encoders (ms-marco-MiniLM-L-6-v2).


## Methodology

### 1. Indexing and baseline (Phase I)
We built a custom index to ensure reproducibility and control. We compared two primary lexical retrievers: 
* **BM25 vs TF-IDF:** evaluated as strong baselines for initial document retrieval
* **Data quality impact:** a comparative analysis was conducted between raw OCR text and corrected text to quantify the impact of transcription noise on retrieval effectiveness.


### 2. Advanced re-ranking systems (Phase II)
To move beyond simple keyword matching, we implemented two sophisticated re-ranking strategies:
* **Neural re-ranking (E1):** utilizing a croos-encoder architecture to predict semantic similarity between the query and the top 10 documents retrieved by BM25.
* **Temporal and Entity-based re-ranking (E2):** a custom heuristic function that boosts document scores based on the proximity of their publication_date to the query's temporal focus and the presence of identified Named Entities (using en_core_web_sm).
 

### 3. Evaluation setup
The systems were evaluated using 8 different metrics, including ***P@1, MAP and nDCG***, to ensure a comprehensive assessment of ranking quality.

## Results
The evaluation demonstrated that while lexical models are robust, neural re-ranking provides a significant edge in semantic understanding.

*Results E1:*
<img width="956" height="210" alt="image" src="https://github.com/user-attachments/assets/2db08c18-d021-4ec8-92c7-6b4cadc0026f" />

*Results E2:*
<img width="967" height="217" alt="image" src="https://github.com/user-attachments/assets/771e84c0-ed9a-4e54-b8af-f34bd838beeb" />


**Key insights:** transitioning from raw OCR to clean text improved performance by ~ 32%. The neural cross-encoder achieved the highest precision (P@1:  0.678), successfully identifying the correct answer even when keyword overlap was minimal.


## Issues Encountered

The primary challenge was the hardware constraint of the standard google Colab environment. The neural re-ranker is computationally intensive, forcing us to restrict re-ranking to a "shallow pool" (top 10 results). We also faced technical hurdles with library dependencies (specifically pyterrier_transformers), which required implementing a custom Transformer class to handle RAM saturation and ensure stable execution.


## Project Recap

In summary, our project involved indexing over 130,000 historical records, analyzing the impact of OCR noise and designing a multi-stage retrieval pipeline. We successfully integrated traditional lexical search with modern NLP techniques like rross-encoders and Named Entity Recognition to handle the specific challenges of 19th-century English.

## Final Conclusion

The investigation proved that BM25 is an exceptionally resilient baseline for historical data. However, for high-precision tasks like question answering, a hybrid approach (layering neural semantic understanding over lexical retrieval) is essential. This project provided us with deep practical experience in building modular IR systems and managing the end-to-end pipeline from raw, noisy data to ranked results.

*For a detailed analysis, please refer to the full project report.*

## Contributing

If you have suggestions for improving the re-ranking heuristics or wish to test different neural architectures (like Dense Passage Retrieval), feel free to open an issue or submit a pull request. Let’s continue improving this project together!


## Credits
* Developed by ***Tsuhuy Ecaterina***, ***Colombo Giacomo*** and ***Goatelli Lorenzo*** for the "Information Retrieval and Recommender Systems" course.
* The dataset used for this project was provided by **Library Congress** *(Chronicling America collection)*.

