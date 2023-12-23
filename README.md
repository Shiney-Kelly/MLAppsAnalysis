# Analysis of Machine Learning (ML) Applications on HuggingFace store

This project performs a study of ML applications hosted on the [HuggingFace](https://huggingface.co/spaces) ML store. In particular, I investigate the ML applications classified in “Text Classification” and “Text Generation” groups, defined by the filters from the Hugging Face website. In comparison with the total number of ML applications and the source code size of the ML applications developed with “Text Classification” and “Text Generation” models, I conclude that it is easier to develop ML applications using “Text Classification” models than applications using “Text Generation” models.

## Build tools & versions used
- Python, 3.11.5
- Jupyter Notebook, 7.0.6
- JupyterLab, 4.0.8
- [Anaconda](https://www.anaconda.com/download), 2.5.1
- [Hugging Face Hub API](https://huggingface.co/docs/huggingface_hub/package_reference/hf_api)

## Steps to run the app
1. Install Anaconda to be able to set up environment for running the Python notebook.
2. Install Jupyter Notebook and JupyterLab environments.
3. Initialize an environment to display and run the notebook.
4. Download or clone source codes from GitHub:
```shell
$ git clone https://github.com/AM-Kitty/MLAppsAnalysis.git
```
5. Install all required packages in `requirements.txt`:
```shell
$ cd ./MLAppsAnalysis/
$ pip install -r ./requirements.txt
```
6. Run the application and open the notebook to check the code and outputs for the entire analysis.

## Purpose of Project

This project aims to understand whether “Text Classification” ML models are easier to use by software developers than “Text Generation” ML models, where the term “easier” refers to “requiring less effort for coding or maintenance”.

## Analysis Design

The analysis is based on the top-20 “Text Classification” and top-20 “Text Generation” models filtered from [HuggingFace](https://huggingface.co/models), ranked according to popularity. Specifically, I used the total number of downloads of each model to evaluate the popularity, where the higher the total number of downloads, the more popular the model is.

To explore whether it is easier to develop ML applications using “Text Classification” models than applications using “Text Generation” models, this analysis focuses on exploring two factors, the total number of ML applications developed using the models from the two groups and the size of the source code of those ML applications repositories, as well as their impact on affecting the popularity of ML models. The whole analyzing process consists of 4 parts including stating hypotheses, collecting data, performing statistical tests, and testing the hypothesis.

#### Stating hypotheses

As for testing the factor of the total number of ML applications developed, I state the null hypothesis that “There is not a greater difference in the number of “Text Classification” ML applications developed compared with using “Text Generation” ML models. (H<sub>0<sub>1</sub></sub>)”

For analyzing the size of the source of the ML applications repositories, I state the null hypothesis that “There is not a greater difference in the source code size between using “Text Classification” ML applications and using “Text Generation” ML models. (H<sub>0<sub>2</sub></sub>)”

#### Collecting data

I collect the number of ML applications for each “Text Classification” and “Text Generation” model obtained from the top-20 lists, and calculate the source code size of those ML applications. To determine if the given datasets are normally distributed, 2 methods are used. One is to perform the Shapiro-Wilk Test to calculate the p-value, and compare it with the significance level to check; another is to plot a histogram of the data to visually examine the distribution.

#### Performing statistical tests

The Mann-Whitney U test is selected as the test method, since the data collected are not normally distributed, and the sample size is relatively small (only the top 20 of the ML models are considered). In addition, the two comparison groups “Text Classification” and “Text Generation” satisfy the condition of independent samples to perform the testing.

#### Testing the hypothesis

As our sample size is greater than 20, the p-value is calculated based on the normal approximation using standardized test statistics. When p-value is significant, which is less than or equal to 0.05, I reject the null hypothesis.

In addition, I made several assumptions prior to the analysis:

#### Assumptions
- **Popularity based on the number of downloads**: Hugging Face website provides trending (number of likes within recent 7 days), the total number of likes, and the total number of downloads to rank the ML models. I choose to use the total number of downloads of the ML model to rank its popularity among the top-20 ML applications.
- **Exclude unnecessary files from ML application repositories**: When calculating the size of the source code of an ML application repository, I only compute sizes of meaningful development files including code files (.py, .r, .ipynb, .java, .m, .sh, .c, .cc, .cpp) and configuration files (.yml, .yaml, .json, .jinja), as other files (i.e., .mp4, .png, etc.) are irrelevant and not considered as a factor to evaluate the difficulty for developing and maintaining the ML application.

## Discussion of Results

In the analysis of comparing the total number of ML applications developed using the top-20 “Text Classification” and top-20 “Text Generation” models, I found that there are more ML applications created using “Text Generation” models, where the total number is 3656 and 757, respectively, as shown in `Figure 1`. Since the p-value calculated using the Mann-Whitney U test is 0.0114, which is less than 0.05, I can reject H<sub>0<sub>1</sub></sub> and show that the number of ML applications developed using “Text Generation” models is much larger than using “Text Classification” models. Thus, it demonstrates that “Text Generation” models are more popular to develop.

<p align="center">
  <img src="./output_imgs/5 - Comparison on the total number of spaces developed using Text Generation and Text Classification.png" alt="Comparison on the total number of spaces developed using Text Generation and Text Classification" />
  Figure 1. Comparison on the total number of spaces developed using Text Generation and Text Classification
</p>

In comparison with the source code size of the ML applications developed using the top-20 “Text Classification” and top-20 “Text Generation” models, I found that the average source code size of ML applications created using “Text Classification” models is relatively smaller than the ones using “Text Generation” models, where the average size is 27.94 MB and 690.25 MB, respectively, as shown in `Figure 2`. Similarly, as the calculated p-value is 0.002, which is less than 0.05, I can reject H<sub>0<sub>2</sub></sub> and show that the source code size of ML applications developed using “Text Generation” models is much larger than using “Text Classification” models. Therefore, it illustrates that developing ML applications using “Text Generation” models is more complex.

<p align="center">
  <img src="./output_imgs/8 - Comparison on the average source code size of spaces developed using Text Generation and Text Classification.png" alt="Comparison on the average source code size of spaces developed using Text Generation and Text Classification" />
  Figure 2. Comparison on the average source code size of spaces developed using Text Generation and Text Classification
</p>

Considering the findings on both factors, I believe that although more developers choose to use “Text Generation” models to develop ML applications, the average source code size of those application repositories is much larger than those using “Text Classification” models, indicating a greater code complexity. This also implies that developers who leverage “Text Generation” models need to make more efforts to develop external functionalities.

In addition, there are some limitations to the findings:

#### Limitations
- **Small sample size**: The number of ML applications collected is only based on the top-20 ML models, which consist of 757 ML applications developed with “Text Classification”.
- **Not perfect mutually exclusive**: There are 11 ML applications using models from both “Text Classification” and “Text Generation”.

## Future Improvements
- **Add time periods**: I believe it is necessary to consider collecting the data in a designated period, such as the last 6 months. This could ensure two groups of data are coming from the same period.
- **Research PR commits**: It is better to consider exploring the number of PR commits made in the repositories developed using “Text Classification” and “Text Generation” to evaluate the effort needed from developers.
- **Alternative way of defining popularity**: To better understand the preferences of developers, it is better to consider proposing the analysis using the trending (the total number of likes within 7 days) to collect recent information for the utilization of ML models.
