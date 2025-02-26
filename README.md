# IMDb TV Series Rating Analysis with PandasAI and Local LLM

## Overview

This project demonstrates the usage of [PandasAI](https://docs.pandas-ai.com/) with LLM locally through [Ollama](https://ollama.com/) to analyze a dataset of IMDb TV Series Ratings. The analysis includes verifying outputs generated by PandasAI with manually generated results. The dataset used can be found [here](https://www.kaggle.com/datasets/khushikhushikhushi/imdb-top-rated-tv-series-dataset).

## Prerequisites
1. **Python 3.x**: Download and install from [python.org](https://www.python.org/).
2. **Ollama**: Download and install from [ollama.com](https://ollama.com/).

## Setup
1. **Setting up local LLM**
    * Download a llm according to your system specifications
        ```bash
        ollama pull phi3
        ``` 
        This will install phi3 model in `users_dir\.ollama\models\blobs`
    * **[ OPTIONAL ]** if you want to install models in different location then change the environment variable
        * **[ CHOOSE ANY ONE ]** Windows:
            * CMD
                ```bash
                set OLLAMA_MODELS=your_path_to_model
                ```
            * Powershell
                ```bash
                $env:OLLAMA_MODELS="your_path_to_model"
                ```
        * Unix or MacOS:
            ```bash
            export OLLAMA_MODELS=your_path_to_model
            ```
    * For more detailed information, you can refer to the [Ollama GitHub repository](https://github.com/ollama/ollama).
2. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/SartazAnsari/prompt-analysis-ollama.git
   cd prompt-analysis-ollama
   ```

2. **[ CHOOSE ANYONE ] Environment setup**
    * Using **Python**
        1. Create virtual environment: 
            ```bash
            python -m prompt-analysis-ollama-env
            ```
        2. Activate the environment:
            * Windows: 
                ```bash
                prompt-analysis-ollama-env\Scripts\activate
                ```
            * Unix or MacOS:
                ```bash
                source prompt-analysis-ollama-env/bin/activate

                ```
        3. Install the required packages:
            ```bash
            pip install notebook
            pip install ipykernel
            pip install kaggle
            pip install pandas matplotlib
            pip install pandasai
            ```
        4.  if you get error as Microsoft Visual C++ 14.0 or greater is required while installing `pandasai` then install **MSVC v143 - VS 2022 C++ x64/x86 Build Tools** and **Windows 11 SDK** or **Windows 10 SDK** from [Build tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/). 
        5. If you get error as No module named 'yaml' then install `pip install pyyaml`.   
    * Using **Conda**
        1. Install **Miniconda/Anaconda**: Download and install from [conda.io](https://conda.io).
        2. Create a new environment:
            ```bash
            conda create --name prompt-analysis-ollama-env python=3.12
            ```
        3. Activate the environment:
            ```bash
            conda activate prompt-analysis-ollama-env
            ```
        4. Install the required packages:
            ```bash
            conda install -c conda-forge notebook
            conda install -c conda-forge ipykernel
            conda install -c conda-forge kaggle
            conda install pandas matplotlib
            pip install pandasai
            ```
        5.  if you get error as Microsoft Visual C++ 14.0 or greater is required while installing `pandasai` then install **MSVC v143 - VS 2022 C++ x64/x86 Build Tools** and **Windows 11 SDK** or **Windows 10 SDK** from [Build tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/). 
        6. If you get error as No module named 'yaml' then install `conda install pyyaml`.

3. **[ IF NOT SET BEFORE ] Setting up the Kaggle API**
    * Sign in to **Kaggle** and navigate to the **Account** tab of your user profile.
    * Scroll down to the **API** section and click on **Create New API Token**. 
    * This will download a file named `kaggle.json` containing your API credentials.
    * Place the `kaggle.json` file in the `~/.kaggle/` directory. If the directory does not exist, create it.
    * You're all set up! You can now use the Kaggle API to download datasets directly to your project.

4. **Setting up LLM and Agent**
    * By default, PandasAI uses BambooLLM if no other LLM is specified. You can skip setting up LLM and directly pass the DataFrame to Agent as follows:
        ```bash
        agent = Agent(dfs=df)
        ``` 
    * To use local LLM, we have to use API endpoint.
        ```bash
        llm = LocalLLM(api_base='http://localhost:11434/v1', model='phi3')
        agent = Agent(dfs=df, config={'llm': llm})
        ```
    * For more detailed information, you can refer to the [PandasAI Local LLM documentation](https://docs.pandas-ai.com/llms#local-models), [PandasAI GitHub repository](https://github.com/pandasai/pandasai) and [Ollama GitHub respository](https://github.com/ollama/ollama).

## Analysis
* Insights into the number of unique TV series titles and parental ratings.
* Top and bottom rated TV series were identified based on their ratings.
* Average ratings were calculated for each parental rating category and sorted to highlight the highest and lowest average ratings.
* Various visualizations, including bar charts and scatter plots, were generated to effectively present the data.

## Usage
1. Ensure the dataset is available in the project directory.
2. Import the necessary libraries and functions.
3. Run the provided Python script to perform the analysis and generate visualizations.