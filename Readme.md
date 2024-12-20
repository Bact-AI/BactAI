# Bact.AI - Functional Prection AI-Agent 🌱🧬
<p align="center">
  <img alt="BactAI_logo" src="img/banner.jpg">
</p>

**Bact.AI** is an advanced AI-powered platform 🤖 designed to map prokaryotic clades (e.g., genera, species, or subspecies) to a variety of metabolic or other ecologically relevant functions. Leveraging cutting-edge artificial intelligence and machine learning algorithms, **Bact.AI** not only provides functional annotations based on current literature 📚 but also delivers intelligent predictions and insights 💡 based on user-specific microbial community data.

This agent includes a powerful database and AI-driven tools that allow users to convert microbial taxonomic profiles (e.g., OTU tables) into functional profiles, using the taxa identified in the sample. The AI engine, **AI-Agent**, enhances the accuracy of functional predictions and provides deeper insights into microbial ecosystems 🌍.

## Features 🌟

- **Bact.AI Database** (`Bact_AI.txt`): A comprehensive file containing functional annotations for prokaryotic clades, derived from current peer-reviewed literature 📖.
- **AI-Agent**: An AI-powered analysis engine integrated within **Bact.AI**, capable of predicting missing functional annotations and offering recommendations for new, potential functions based on patterns in the data 🔮.
- **Python Script** (`Bact_AI.py`): This script allows you to transform taxonomic tables (e.g., BIOM format) into functional tables, linking OTUs with their corresponding functions in **Bact.AI** 🔄.
- **Intelligent Predictions**: **AI-Agent** leverages machine learning models 🤖 to suggest potential functions for uncharacterized taxa, even when the associated literature is sparse or incomplete 🔍.

## Getting Started 🚀

To get started with **Bact.AI**, follow these steps:

1. Prepare your microbial community taxonomic profile (usually in BIOM or TSV format) 📝.
2. Download and configure the **Bact.AI** database (`Bact_AI.txt`) 📥.
3. Use the **Bact_AI.py** script to transform taxonomic data into functional data, enhanced by the AI model ⚙️.

### Example Usage

To convert an OTU table in **BIOM** format into a functional table:

```bash
./Bact_AI.py -i otu_table.biom -o functional_table.biom -g Bact_AI.txt
```

This assumes that the OTU table contains full taxon names (e.g., from SILVA or Greengenes format) 🔠.

If your OTU table uses OTU numbers and taxonomic annotations are stored as metadata, use the following command:

```bash
./Bact_AI.py -i otu_table.biom -o functional_table.biom -g Bact_AI.txt --Bact_by_metadata 'taxonomy'
```

**AI-Agent** will automatically analyze the output data and suggest possible unannotated functional groups based on patterns found within the taxonomic data 🔍. You can view these predictions by running:

```bash
./Bact_AI.py -i otu_table.biom -o functional_table_with_predictions.biom -g Bact_AI.txt --use_ai_predictions
```

To convert a classical table (e.g., TSV format), consult the help menu by running:

```bash
./Bact_AI.py -h
```

For more detailed instructions and resources, visit the official **Bact.AI** website: [Bact.ai]() 🌐

## Key Features of **Bact.AI** 🔑

- **Taxa-to-function Mapping**: Functional groups are assigned based on taxa identified in the sample, enabling a comprehensive understanding of microbial functions in diverse environments 🌿.
- **AI-Driven Predictions**: The integrated **AI-Agent** engine provides real-time functional predictions for unannotated or novel taxa, improving the robustness of functional analysis 🤖.
- **Peer-Reviewed Database**: The functional annotations in **Bact.AI** are based on published research of cultured organisms and relevant ecological studies 📚.
- **Customizable and Scalable**: As more data is gathered, **Bact.AI** can be updated with new functional annotations. **AI-Agent** can learn from new datasets, continuously improving its prediction accuracy 📈.


# Function.py:Protein Structure Prediction Combine Bact.AI with AlphaFold 🧬

## Overview 🌟

This Function.py script allows for the processing of protein sequence data and predicts their three-dimensional structures using **AlphaFold**. The script is designed to take a dataset of protein sequences (in CSV or TSV format), run AlphaFold for structure prediction, and then merge the results (e.g., PDB file paths and prediction confidence) with the original dataset. The output includes both the updated dataset and the predicted PDB files.

## Features 🚀

- **Input Format**: Accepts protein sequence data in CSV or TSV format. 📊
- **AlphaFold Integration**: Leverages AlphaFold for protein structure prediction. 🤖
- **Parallel Processing**: Uses threading to handle large datasets efficiently. ⚡
- **Results Output**: Combines predicted structures and other relevant data into an updated CSV file and saves the predicted structures as PDB files. 📑🔬

## Prerequisites 🛠️

Before using this script, make sure the following prerequisites are met:

### Python Requirements 🐍

- Python 3.6+
- Required Python libraries:
  - `numpy`
  - `pandas`
  - `argparse`
  - `concurrent.futures`
  - `shutil`
  - `time`
  - `os`
  - `biopython` (if working with biological sequence data)

You can install the necessary Python packages using the following:

```bash
pip install numpy pandas biopython
```

### AlphaFold Environment 🧬

- **AlphaFold**: The script assumes that you have access to a working AlphaFold environment. Follow the official [AlphaFold installation guide](https://github.com/deepmind/alphafold) to set up AlphaFold on your machine or a cloud environment.
- **GPU**: Running AlphaFold on a machine with a GPU is recommended for faster predictions, although CPU is also supported.

### Optional: PDB File Processing Tools 🔍

If you plan to manipulate or visualize the generated PDB files, tools such as **PyMOL** or **Chimera** are recommended.

## Usage 💻

### Command-Line Arguments 📋

The script requires three arguments:

- `input_file`: Path to the input protein sequence file (CSV or TSV).
- `output_file`: Path to the output file where the results (including the protein sequence and predicted structure data) will be saved.
- `output_dir`: Directory where the PDB files will be saved.

Example command to run the script:

```bash
python batch_predict.py input_data.tsv output_results.csv /path/to/output_dir
```

This command will:

1. Read the `input_data.tsv` file, which should contain protein sequences in one of the columns (e.g., named `sequence`).
2. Perform structure predictions using AlphaFold.
3. Save the output results in `output_results.csv`, with additional columns like `predicted_pdb` and `confidence`.
4. Save the predicted PDB files in the directory `/path/to/output_dir`.

### Input File Format 📝

The input file should be a CSV or TSV file with the following format:

| Protein ID | Sequence      | Function      |
| ---------- | ------------- | ------------- |
| P001       | MKTAYIAKQR... | Kinase        |
| P002       | MEKGYYVLLA... | Transcription |

- `Protein ID`: A unique identifier for each protein.
- `Sequence`: The amino acid sequence of the protein.
- `Function` (optional): A column for any functional annotations or additional metadata.

### Output File Format 📂

The output file will be a CSV file with the following format:

| Protein ID | Sequence      | Function      | Predicted PDB Path      | Confidence |
| ---------- | ------------- | ------------- | ----------------------- | ---------- |
| P001       | MKTAYIAKQR... | Kinase        | /path/to/output_dir/... | 0.87       |
| P002       | MEKGYYVLLA... | Transcription | /path/to/output_dir/... | 0.91       |

- `Predicted PDB Path`: The path to the predicted PDB file for the protein structure.
- `Confidence`: The confidence score of the prediction (between 0 and 1).

The script will also save the PDB files in the specified `output_dir`.

## Script Breakdown 🛠️

### 1. **Load Input Data** 📥:

The `load_protein_data(file_path)` function reads the input CSV/TSV file and loads the protein sequences into a pandas DataFrame.

### 2. **Run AlphaFold for Structure Prediction** 🤖:

The `predict_structure(protein_sequence)` function is a placeholder for AlphaFold's structure prediction. You need to replace it with the actual call to AlphaFold's API or model for structure prediction.

### 3. **Parallel Structure Prediction** 🔄:

The `process_protein_data_parallel(data, output_dir, max_workers)` function uses Python’s `ThreadPoolExecutor` to handle large datasets efficiently by performing parallel processing of protein sequences. Each sequence is processed concurrently to generate predictions faster.

### 4. **Save Structure Files** 💾:

The `save_structure_file(structure_data, output_dir, protein_sequence)` function saves the predicted PDB files to the specified directory.

### 5. **Merge Results and Output** 🔗:

The `update_table_with_structure(data, structure_data)` function merges the predicted structures and their associated metadata back into the original dataset. The result is saved as a CSV file, and the corresponding PDB files are stored in the provided directory.

## Example Workflow 🛠️

1. **Prepare your input file** (e.g., `input_data.tsv`) with the protein sequences.

2. Run the script

    using the following command:

   ```bash
   python batch_predict.py input_data.tsv output_results.csv /path/to/output_dir
   ```

3. The script will:

   - Process the sequences.
   - Predict the structures using AlphaFold (replace the simulated function with real AlphaFold prediction).
   - Save the predicted PDB files and the updated dataset containing PDB file paths and confidence scores.

## Troubleshooting ⚠️

### 1. AlphaFold is not running correctly 🔧

- Ensure that your AlphaFold environment is set up properly and that all dependencies are installed.
- Refer to the [AlphaFold repository](https://github.com/deepmind/alphafold) for setup instructions.

### 2. PDB files are not being saved 💾

- Check if the `output_dir` directory exists and is writable. Ensure you have permission to write files in that location.

### 3. Performance issues with large datasets 🏃‍♂️

- The script uses threading to parallelize the structure prediction process. If the dataset is very large, you may need to adjust the `max_workers` parameter to control the number of concurrent threads.
- Running the script on a machine with a GPU will significantly speed up the AlphaFold predictions.


# Function1.py:Protein Functional Annotation Combine Bact.AI InterProScan 🔬

## Overview 🧬

This Python script allows you to annotate protein sequences with functional domains and families using **InterProScan**. After annotating the sequences, the script visualizes the distribution of protein families in your dataset using a **pie chart**. This is useful for understanding the functional composition of a protein dataset and for exploring domain and family annotations.

## Features 🚀

- **Input Format**: Accepts protein sequence data in CSV or TSV format. 📊
- **InterProScan Integration**: Annotates protein sequences with domains and functional families. 🔍
- **Parallel Processing**: Uses threading to speed up the annotation process. ⚡
- **Data Visualization**: Generates a pie chart showing the distribution of protein families. 🍰
- **Results Output**: Saves the annotated sequences along with their functional annotations into a CSV file. 📑

## Prerequisites 🛠️

Before running this script, make sure the following prerequisites are met:

### Python Requirements 🐍

- Python 3.6+
- Required Python libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `argparse`
  - `concurrent.futures`

You can install the necessary Python packages using:

```bash
pip install numpy pandas matplotlib
```

### InterProScan 🧬

- **InterProScan**: The script integrates **InterProScan**, a tool for protein sequence annotation. You will need to have InterProScan installed and available on your system to actually annotate the sequences. You can download and install it from the official [InterProScan website](https://www.ebi.ac.uk/interpro/interproscan.html).

  **Note**: If you're running this code in a simulation mode (like for testing), you can replace the function `run_interproscan()` with real InterProScan calls.

### Optional: PDB File Processing Tools 🔍

If you wish to visualize or manipulate the predicted structures (or other related data), you may need visualization tools like **PyMOL** or **Chimera**.

## Usage 💻

### Command-Line Arguments 📋

The script accepts two arguments:

- `input_file`: Path to the input file (CSV or TSV) containing protein sequences.
- `output_file`: Path to the output file where the annotated results will be saved.

Example command to run the script:

```bash
python annotate_protein.py input_data.tsv output_results.csv
```

### Input File Format 📝

Your input file should be a CSV or TSV file with at least one column containing the protein sequences. For example:

| Protein ID | Sequence      |
| ---------- | ------------- |
| P001       | MKTAYIAKQR... |
| P002       | MEKGYYVLLA... |

- `Protein ID`: A unique identifier for each protein.
- `Sequence`: The amino acid sequence of the protein.

### Output File Format 📂

The output file will be a CSV file with the following format:

| Protein ID | Sequence      | Domains                        | Family         |
| ---------- | ------------- | ------------------------------ | -------------- |
| P001       | MKTAYIAKQR... | ['Kinase', 'ATPase']           | Protein Kinase |
| P002       | MEKGYYVLLA... | ['Zinc finger', 'Phosphatase'] | Phosphatase    |

- `Domains`: A list of functional domains found in the protein.
- `Family`: The predicted protein family based on functional annotations.

Additionally, a pie chart will be displayed, visualizing the **protein family distribution**.

## Script Breakdown 🛠️

### 1. **Load Input Data** 📥

The `load_protein_data(file_path)` function reads the input CSV or TSV file and loads the protein sequences into a pandas DataFrame.

### 2. **Run InterProScan for Annotation** 🔬

The `run_interproscan(protein_sequence)` function simulates running **InterProScan** on the protein sequence. It returns a dictionary with the identified protein domains and family. Replace this function with an actual call to **InterProScan** when running in production.

### 3. **Parallel Processing** ⚡

The `process_protein_data_parallel(data, max_workers)` function processes the protein sequences in parallel using threading. This allows the script to handle large datasets efficiently by performing multiple annotations simultaneously.

### 4. **Data Visualization** 📊

The `visualize_family_distribution(data)` function generates a **pie chart** that shows the distribution of protein families in the dataset. This gives you a quick overview of the functional composition of your protein data.

### 5. **Results Output** 💾

The `save_results_to_file(data, output_file)` function saves the annotated results, including protein domains and families, to a new CSV file.

## Example Workflow 🛠️

1. **Prepare your input file** (`input_data.tsv`) with the protein sequences.

2. **Run the script** using the following command:

   ```bash
   python annotate_protein.py input_data.tsv output_results.csv
   ```

   - This will process the sequences, annotate them using InterProScan (replace the simulated function with real InterProScan calls), generate a pie chart of protein family distribution, and save the annotated data to `output_results.csv`.

3. **Visualize Protein Family Distribution** 🍰: After processing, the script will display a pie chart showing the distribution of protein families in your dataset.

### Example Output:

The output CSV file might look like this:

| Protein ID | Sequence      | Domains                        | Family         |
| ---------- | ------------- | ------------------------------ | -------------- |
| P001       | MKTAYIAKQR... | ['Kinase', 'ATPase']           | Protein Kinase |
| P002       | MEKGYYVLLA... | ['Zinc finger', 'Phosphatase'] | Phosphatase    |

Additionally, the pie chart will show the percentage distribution of the protein families such as **Protein Kinase**, **Phosphatase**, etc.

## Troubleshooting ⚠️

### 1. InterProScan is not running correctly 🔧

- Ensure that your InterProScan environment is set up correctly and that the tool is executable from the command line. If using an external tool, make sure you have specified the correct path to the InterProScan installation.
- Refer to the [InterProScan installation guide](https://www.ebi.ac.uk/interpro/interproscan.html) for detailed setup instructions.

### 2. Pie chart is not displaying correctly 📊

- If you're running the script in a non-GUI environment (like a server), the pie chart may not display. You can save the chart to a file by adding `plt.savefig('output_chart.png')` after the `plt.show()` line in the `visualize_family_distribution` function.

### 3. Performance issues with large datasets 🏃‍♂️

- The script uses threading to parallelize the process, but very large datasets may still take time to process. Consider reducing the number of threads in the `max_workers` parameter or running the script on a machine with more CPU resources.




## Caveats ⚠️

**Bact.AI** defines functional groups by linking them to specific taxa. These affiliations are primarily based on cultured organisms and peer-reviewed publications. **Bact.AI** assumes that if all cultured members of a clade can perform a particular function, then all members of that clade (including non-cultured species) can perform that function. As more organisms are cultured and new data becomes available, some of these assumptions may need to be revised 🔄.

Additionally, **AI-Agent**'s predictions are based on patterns identified through machine learning models. While these predictions improve over time, they should be verified with experimental data when possible ⚗️.

## License Agreement 📜

------

Copyright (c) 2024, Bact.AI. All rights reserved.

Use and redistribution of the **Bact.AI** database, including any associated software, with or without modification, are permitted provided that the following conditions are met:

- Redistributions must retain the above copyright notice, this list of conditions, and the following disclaimer in the database itself, as well as in documentation and/or other materials provided with the distribution 📚.
- Neither the name of the original author (Stilianos Louca), nor the names of its contributors may be used to endorse or promote products derived from **Bact.AI** without specific prior written permission ✍️.
- If the **Bact.AI** database or any associated software has been modified from its original version, this needs to be clearly indicated in any redistribution and in any publication using the modified version ⚙️.

THE **Bact.AI** DATABASE, INCLUDING ANY ASSOCIATED SOFTWARE, IS PROVIDED "AS IS" WITHOUT WARRANTIES OF ANY KIND. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES ARISING IN ANY WAY OUT OF THE USE OF **Bact.AI**, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE ⚠️.
