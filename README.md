# eval-MCG-COLING-2025

<p align="center">
<a href="https://sites.google.com/view/multilang-counterspeech-gen/shared-task?authuser=0">
      <img alt="Web Page" src="https://img.shields.io/badge/Shared%20Task-Visit%20Here-blue">
    </a>
<a href="https://sites.google.com/view/multilang-counterspeech-gen/home?authuser=0">
      <img alt="Web Page" src="https://img.shields.io/badge/Workshop-Visit%20Here-red">
</a>
<a href="https://github.com/hitz-zentroa/cn-eval/blob/main/LICENSE">
        <img alt="GitHub license" src="https://img.shields.io/github/license/hitz-zentroa/cn-eval">
</a>
</p>

This repository contains the evaluation files for the MCG-COLING-2025 shared task. It provides two methods of evaluation: 
- **Traditional Metrics**: Evaluation using ROUGE-L (Lin, 2024), BLEU (Papineni et al., 2002), BERTScore (Zhang et al., 2020) and Novelty (Wang and Wan, 2013).
- **LLM evaluator**: Evaluation using the JudgeLM model as decribed in Zubiaga et al. (2024). 

Once the evaluations are performed, the results can be analyzed using the provided Python notebook to rank the models based on their performance.

## Repository Structure

- **/data**
  - `ML_MTCONAN_KN_Train_Set.csv`: Train set. This file is needed to compute the Novelty metric.

- **/evaluation**
  - /automatic_evaluation: Folder where traditional metrics will be stored. There is a sample file for reference.
  - /bash: Contains the bash scripts to execute the evaluations.
    - `compute_traditional_metrics.sh`: Executes the evaluation based on traditional metrics.
    - `judge_full_pipeline.sh`: Runs the evaluation using the JudgeLM model.
  - /JudgeLM-main: A clone of [JudgeLM](https://github.com/baaivision/JudgeLM).
  - /judgements: Folder where model judgements will be stored. It contains several sample files for reference. Among these, `7_ilv_results.csv` is the key file that aggregates all the evaluations considered during the process.
  - /scripts: Folder with the files needed to format data and compute the metrics.
  - `Rank_models.ipynb`: Python notebook for analyzing the evaluation results and ranking models.

    
- **/generate**: This folder contains the generated output files for evaluation.
  - `system1.csv`: Example of the file format for evaluation.
  - `system2.csv`: Example of the file format for evaluation.
  
## Instructions for Use

### Step 1: Prepare Generated Files
Ensure your generated files are placed in the `generate` folder. These files should follow the CSV format as demonstrated in `system1.csv` and `system2.csv`.

### Step 2: Execute Evaluations

1. **Run Traditional Metrics Evaluation**  
  Run the following command to execute traditional metrics evaluation:
   ```bash
   ./evaluation/bash/traditional_metrics.sh

In this file, only the first line of the code should be edited. Specifically, modify the line `source ./.venv/bin/activate` to point to the path of your own environment.

params=7
   
2. **LLM Evaluator**  
   For JudgeLM model evaluation, execute the following command:
   ```bash
   ./evaluation/bash/judge_full_pipeline.sh
  
Once again, only the first line of the code should be edited. Specifically, modify the line `source ./.venv/bin/activate` to point to the path of your own environment. 

Additionally, you can change the variable `params` to adjust the size of the JudgeLM model. There are three available options: `7`, `13`, or `33`, referring to how many billion parameters the model has. Please note that each size will require a different amount of GPU memory.

### Step 3: Analyze Results
Once the evaluations are complete, open the `Rank_models.ipynb` file in Jupyter Notebook. This notebook allows you to visualize the results and rank the models based on their performance.

## Dependencies

This project requires the following dependencies:

- JudgeLM's dependencies are outlined in the [JudgeLM GitHub repository](https://github.com/baaivision/JudgeLM).

Additionally, you should install the following Python packages:

```bash
pip install numpy pandas json os plotly tqdm itertools
```

## References

```bibtex
@inproceedings{zubiaga2024llmbasedrankingmethodevaluation,
      title={A LLM-Based Ranking Method for the Evaluation of Automatic Counter-Narrative Generation}, 
      author={Irune Zubiaga and Aitor Soroa and Rodrigo Agerri},
      year={2024},
      booktitle={Findings of EMNLP} 
}

@inproceedings{ijcai2018p618,
  title     = {SentiGAN: Generating Sentimental Texts via Mixture Adversarial Networks},
  author    = {Ke Wang and Xiaojun Wan},
  booktitle = {Proceedings of the Twenty-Seventh International Joint Conference on
               Artificial Intelligence, {IJCAI-18}},
  publisher = {International Joint Conferences on Artificial Intelligence Organization},
  pages     = {4446--4452},
  year      = {2018},
  month     = {7},
  doi       = {10.24963/ijcai.2018/618},
  url       = {https://doi.org/10.24963/ijcai.2018/618},
}

@misc{zhang2020bertscore,
      title={BERTScore: Evaluating Text Generation with BERT}, 
      author={Tianyi Zhang and Varsha Kishore and Felix Wu and Kilian Q. Weinberger and Yoav Artzi},
      year={2020},
      eprint={1904.09675},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
@inproceedings{papineni-etal-2002-bleu,
    title = "{B}leu: a Method for Automatic Evaluation of Machine Translation",
    author = "Papineni, Kishore  and
      Roukos, Salim  and
      Ward, Todd  and
      Zhu, Wei-Jing",
    editor = "Isabelle, Pierre  and
      Charniak, Eugene  and
      Lin, Dekang",
    booktitle = "Proceedings of the 40th Annual Meeting of the Association for Computational Linguistics",
    month = jul,
    year = "2002",
    address = "Philadelphia, Pennsylvania, USA",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/P02-1040",
    doi = "10.3115/1073083.1073135",
    pages = "311--318",
}
@inproceedings{lin-2004-rouge,
    title = "{ROUGE}: A Package for Automatic Evaluation of Summaries",
    author = "Lin, Chin-Yew",
    booktitle = "Text Summarization Branches Out",
    month = jul,
    year = "2004",
    address = "Barcelona, Spain",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/W04-1013",
    pages = "74--81",
}
```