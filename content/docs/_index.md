---
linkTitle: Task
title: TREC 2025 Biomedical Generative Retrieval (BioGen) Track
---

## Introduction
With the advancement of large language models (LLMs), the biomedical domain has seen significant progress and improvement in multiple tasks such as biomedical question answering, lay language summarization of the biomedical literature, clinical note summation, etc. However, hallucinations or confabulations remain one of the key challenges when using LLMs in the biomedical domain. Inaccuracies may be particularly harmful in high-risk situations, such as making clinical decisions or appraising biomedical research. Towards this, in our pilot task organized at TREC 2024, we introduced the task of reference attribution as a means to mitigate the generation of false statements by LLMs toward answering the biomedical question. 



We propose to continue this task with an additional task of grounding the answer in the BioGen track at TREC 2025. The goal of the TREC 2025 BioGen task will be to cite references to support the text of the sentences and the overall answer from LLM output for each topic.

<!--more-->

<!-- This site is a demo of the Hugo Blox Documentation theme. For the full documentation on how to use this template, refer to the [Hugo Blox Documentation](https://docs.hugoblox.com/). -->


## Timeline

**Dataset Release:** May 22, 2025  
**Baseline Release:** May 29, 2025  
**Results Submission Deadline:** August 15, 2025  
**Evaluation Results Release:** Late September, 2025  
**Notebook Paper Due:** Late October, 2025  
**TREC 2025 Conference:** November 17-21


## Task Description
**Task A (Grounding Answer):** Given a biomedical question, a stable version of PubMed documents, and an answer to the question, the task is to ground each sentence of the answer with appropriate PubMed documents by providing their PMIDs. For each answer sentence, you will also be provided with slightly outdated supporting PMIDs. The system-generated PMIDs should include additional relevant documents. Since identifying contradictory references is also crucial in the biomedical domain, the system is also expected to provide PMIDs that contradict the assertions made in each answer sentence. This task serves as a foundational step, preparing participants to effectively tackle the more complex task of Reference Attribution (Task B).

For each answer sentence, the provided PMIDs should meet the following requirements:
- The supporting PMIDs should be addition to the existing supported PMIDs already provided with each answer sentence.
- There should be no more than three PMIDs per answer sentence for both supporting and contradicting assertions.
- The PMIDs must be selected only from the valid set of PMIDs released with the dataset.

One submission (run) should be a UTF-8-encoded JSONL file, with each line being a JSON object for a question-answer pair. Participants should follow this format and submit their runs to NIST via <a href="https://ir.nist.gov/evalbase/" target="_blank">Evalbase</a>.
```json
{
  "metadata": {
    "team_id": "organizers",
    "run_id": "organizers-run-example", 
    "qa_id": "biogen_2024_1",
    "question": "question",
    "existing_supported_citations": [
    "PMID1",
    "PMID2"
    ]
  },
  "answer": [
    {
      "text": "This is the first sentence.",
      "supported_citations": [
        "PMID3",
        "PMID4",
      ],
      "contradicted_citations": [
        "PMID5",
        "PMID6",
      ]
    },
    {
      "text": "This is the second sentence.",
       "supported_citations": [],
       "contradicted_citations": [
        "PMID7",
        "PMID8",
      ]
   }
  ]
}
```
Above is an example line from the final JSONL run file, with the following fields:
- **metadata**: Metadata for this run.
- **team_id**: Unique identifier for the team.
- **run_id**: Unique identifier for the run, specifying both the team and the method used. Each run must have a different **run_id**, and all **run_ids** submitted by the same team should share a common prefix to associate them with the team.
- **qa_id**: The **id** of the question-answer pair.
- **question**: The **question** of the question-answer pair.
- **existing_supported_citations**: A list containing all the existing supported citations.
- **answer**: A list of objects, each representing an answer sentence with:
  - **text**: An answer sentence in plaintext. 
  - **supported_citations**: A list of up to 3 PMIDs (should not be in the  **existing_supported_citations**) that support this answer sentence.
  - **contradicted_citations**: A list of up to 3 PMIDs that contradict this answer sentence.



**Task B (Reference Attribution):**  Given a biomedical topic (question) and a stable version of PubMed documents. The task will be to generate answers containing LLM output that also has attributions (cited references from PubMed) for each sentence (assertion) made.

The generated answer must meet the following requirements:
- The total length of the generated answer should be **within 250 words**.
- There should be no more than three PMIDs per answer sentence.
- The PMIDs must be selected only from the valid set of PMIDs released with the dataset.

One submission (run) should be a UTF-8-encoded JSONL file, with each line being a JSON object for a topic. Participants should follow this format and submit their runs to NIST via <a href="https://ir.nist.gov/evalbase/" target="_blank">Evalbase</a>.
```json
{
  "metadata": {
    "team_id": "organizers",
    "run_id": "organizers-run-example", 
    "topic_id": "biogen_2025_1"
  },
  "responses": [
    {
      "text": "This is the first sentence.",
      "citations": [
        "PMID1",
        "PMID2",
        "PMID3",
      ]
    },
    {
      "text": "This is the second sentence.",
       "citations": [
          "PMID4",
          "PMID5",
       ]
   }
  ]
}
```
Above is an example line from the final JSONL run file, with the following fields:
- **metadata**: Metadata for this run.
- **team_id**: Unique identifier for the team.
- **run_id**: Unique identifier for the run, specifying both the team and the method used. Each run must have a different **run_id**, and all **run_id** submitted by the same team should share a common prefix to associate them with the team.
- **topic_id**: The **id** of the topic.
- **responses**: A list of objects, each representing a generated answer sentence with:
  - **text**: One generated answer sentence in plaintext.. 
  - **citations**: A list of up to 3 PMIDs that support this answer sentence. The citations for a sentence may be empty, and their order does not matter.


## Datasets
The latest PubMed baseline, question-answer pairs (Task A), and topics (Task B) will be available from the [TREC Active Participants Site](https://trec.nist.gov/act_part/act_part.html). The participant can use the [BioGen 2024 assessment](https://pages.nist.gov/trec-browser/trec33/biogen/data/) to develop their systems.

## Participation
Please follow the TREC 2025 registration guidelines from their <a href="https://trec.nist.gov/cfp.html" target="_blank">Call for Participation</a>. 

## Communication
Once you complete the NIST registration process, you should receive an invitation to NIST’s workspace and be granted access to our Slack channel: <a href="https://nistgov.slack.com/archives/C08BU4AF3HB" target="_blank">#trec-biogen-2025</a>. You can also join our Google group [here](https://groups.google.com/g/trec-biogen).


## Evaluation
1. **Task A:**
TBA

2. **Task B (Reference Attribution):**
We will follow the evaluation approach used in BioGen 2024. More details can be found [here](https://arxiv.org/abs/2411.18069)



## Organizers
- [**Deepak Gupta**](https://deepaknlp.github.io/) - National Library of Medicine, NIH
- [**Dina Demner-Fushman**](https://www.nlm.nih.gov/research/researchstaff/DemnerFushmanDina.html) - National Library of Medicine, NIH
- [**Bill Hersh**](https://www.ohsu.edu/people/william-r-hersh-md) - Oregon Health & Science University
- [**Steven Bedrick**](https://www.ohsu.edu/people/steven-d-bedrick-phd) - Oregon Health & Science University
- [**Kirk Roberts**](https://sbmi.uth.edu/center-translational-ai/people/kirk-roberts.htm) - University of Texas Houston

## Other RAG-related Tracks in TREC 2025
There are other tracks in TREC 2025 that feature RAG tasks, with a similar submission format to encourage cross-participation. Participants are welcome to adapt their RAG systems for those tracks to explore their performance across diverse scenarios.
- <a href="https://trec-rag.github.io/" target="_blank">TREC 2025 Retrieval-Augmented Generation Track</a>
- <a href="https://trec-ragtime.github.io/" target="_blank">TREC 2025 RAGTIME Track</a>
- <a href="https://www.trecikat.com/" target="_blank">TREC 2025 Interactive Knowledge Assistance Track (iKAT)</a>
- <a href="https://trec-dragun.github.io/" target="_blank">TREC 2025 DRAGUN Track (DRAGUN)</a>