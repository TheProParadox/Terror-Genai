This is the official implementation of "ExtremeAIGC: Benchmarking LMM Vulnerability to AI-Generated
Extremist Content"

# Usage
### Installation
```
conda create -n MMJ-Bench python=3.10
conda create MMJ-Bench
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```


### Step 1 - Generate Test Cases
In the first step, jailbreak attack techniques are used to generate test cases with `generate_test_cases.py`.
```
./scripts/generate_test_cases.sh $method_name $behaviors_path $save_dir
```


### Step 2 - Generate Completions
After generating test cases ， we can generate completions for a target model with or without defense techniques.

Without defense methods: 
```
./scripts/generate_completions.sh $model_name $behaviors_path $test_cases_path $save_path $max_new_tokens $incremental_update
```
With defense methods.
```
./scripts/generate_completions_defense.sh $attack_type $target_model $defense_type
```

### Step 3 - Evaluate Completions
After generate completions from a `target_model` from Step 2, We will utilize the classifier provided by HarmBench to label whether each completion is an example of its corresponding behavior.
```
./scripts/evaluate_completions.sh $cls_path $behaviors_path $completions_path $save_path
```

