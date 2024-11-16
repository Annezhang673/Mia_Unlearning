## About 

The project aims to study the effects of unlearning on the memorized training data by the LLM. There are various methods to audit an LLM for memorization such as jailbreaking, prompt engineering as well as membership inference attacks (MIA). In this project, we aim to use MIA which are one of the popular methods for auditing LLMs. 

The MIA under consideration are as follows:
- Likelihood Ratio Attack (LiRA)
- Loss attack
- Zlib entropy attack
- Min-K attack

For our experiments, we use Llama2-7B model and Llama2-7b-WhoIsHarryPotter as our base model and unlearned model, respectively. The unlearned model is derived from the base model by unlearning all the knowledge about the Harry Potter books using the technique described [here](https://arxiv.org/abs/2310.02238). For the experiments, we required the forgotten data, the harry potter books, and a non-member dataset which wasn't part of the base model's training data. In order to determine the non-member dataset, we calculated the perplexity scores using the base model over a couple of datasets such as Xsum, enron, etc. We found out that Xsum had the highest perplexity indicating its lowest likelihood of being part of the original training data.

Once the datasets were prepared, we generated the MIA scores from all the attacks mentioned above and plotted them to analyze the effect of unlearning. We were able to infer that there is a significant distribution shift in the MIA scores due to unlearning. This trend can make it easier to infer the membership of data as well as show that unlearning can be a good base for building stronger membership attacks.

## Instructions to run the code

In order to run the code, we need to follow the following steps:

- Create a conda environment with python 3.10 using the following command: **conda create -n <environment_name> python=3.10.13**
- Activate the environment: **conda activate <environment_name>**
- Install dependencies: **pip install -r requirements.txt**
- Running *attack.py* to generate data
  
  **CUDA_VISIBLE_DEVICES=0,1,2,3 python attacks.py --output_dir <path_to_output_dir> --target_model <target_model_path> --member1 <forgotten_data_path> --key1 <text_column_name> --member2 <member2_data_path> --key2 <text_column_name> --nonmember <nonmember_data_path> --key <text_column_name> --max_length <max_sequence_length> --ref_model <reference_model_path> --seed <integer_value> --recompute**

- Run *analysis.ipynb* with kernel set to *<environment_name>*
