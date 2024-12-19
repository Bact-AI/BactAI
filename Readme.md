# Bact.AI - Functional Prection AI-Agent 🌱🧬

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

## Caveats ⚠️

**Bact.AI** defines functional groups by linking them to specific taxa. These affiliations are primarily based on cultured organisms and peer-reviewed publications. **Bact.AI** assumes that if all cultured members of a clade can perform a particular function, then all members of that clade (including non-cultured species) can perform that function. As more organisms are cultured and new data becomes available, some of these assumptions may need to be revised 🔄.

Additionally, **AI-Agent**'s predictions are based on patterns identified through machine learning models. While these predictions improve over time, they should be verified with experimental data when possible ⚗️.

## License Agreement 📜

------

Copyright (c) 2023, Bact.AI. All rights reserved.

Use and redistribution of the **Bact.AI** database, including any associated software, with or without modification, are permitted provided that the following conditions are met:

- Redistributions must retain the above copyright notice, this list of conditions, and the following disclaimer in the database itself, as well as in documentation and/or other materials provided with the distribution 📚.
- Neither the name of the original author (Stilianos Louca), nor the names of its contributors may be used to endorse or promote products derived from **Bact.AI** without specific prior written permission ✍️.
- If the **Bact.AI** database or any associated software has been modified from its original version, this needs to be clearly indicated in any redistribution and in any publication using the modified version ⚙️.

THE **Bact.AI** DATABASE, INCLUDING ANY ASSOCIATED SOFTWARE, IS PROVIDED "AS IS" WITHOUT WARRANTIES OF ANY KIND. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES ARISING IN ANY WAY OUT OF THE USE OF **Bact.AI**, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE ⚠️.
