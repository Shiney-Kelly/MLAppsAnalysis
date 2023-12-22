# Analysis of Machine Learning (ML) Applications on HuggingFace store

This project performs a study of ML applications hosted on the [HuggingFace](https://huggingface.co/spaces) ML store. In particular, I investigate the ML applications classified in “Text Classification” and “Text Generation” groups, defined as the filters from the Hugging Face website. In comparison with the total number of ML applications and the source code size of the ML applications developed with “Text Classification” and “Text Generation” models, I conclude that it is easier to develop ML applications using “Text Classification” models than applications using “Text Generation” models.
## Build tools & versions used
- Python, 3.11.5
- Jupyter Notebook, 7.0.6
- JupyterLab, 4.0.8
- Anaconda, 2.5.1
- [Hugging Face Hub API](https://huggingface.co/docs/huggingface_hub/package_reference/hf_api)

## Steps to run the app
1. Install Anaconda to be able to set up environment for running the Python notebook
2. Install Jupyter Notebook and JupyterLab environments
3. Initialize an environment to display and run the notebook
4. Download or clone source codes from GitHub
```
$ git clone https://github.com/AM-Kitty/MLAppsAnalysis.git
```
5. Install all required packages in `requirements.txt`
```shell
$ cd ./MLAppsAnalysis/
$ pip install -r ./requirements.txt
```
6. Run the application and open the notebook to check the code and outputs for the entire analysis

## Purpose of Project

This project aims to understand whether "Text Classification" ML models are easier to use by software developers than "Text Generation" ML models, where the term "easier" refers to "requiring less effort for coding or maintenance".

## Analysis Design

The analysis is based on the top-20 “Text Classification” and top-20 “Text Generation” models filtered from [HuggingFace](https://huggingface.co/models), ranked according to popularity. Specifically, I used the total number of downloads of each model to evaluate the popularity, where the higher the total number of downloads, the more popular the model is.

To explore whether it is easier to develop ML applications using “Text Classification” models than applications using “Text Generation” models, the whole analysis mainly explore the two factors, the total number of ML applications developed using the models from the two groups and the size of the source code of those ML applications repositories, and their impact on affecting the popularity of ML models. The whole analyzing process consists of 4 parts including stating hypotheses, collecting data, performing statistical tests and testing the hypothesis.

#### Stating hypotheses
As for testing the factor of the total number of ML applications developed, I state the null hypothesis that “There is not a greater difference in the number of “Text Classification” ML applications developed compared with using “Text Generation” ML models.” (H<sub>01</sub>)

For analyzing the size of the source of the ML applications repositories, I state the null hypothesis that “There is not a greater difference in the source code size between using “Text Classification” ML applications and using “Text Generation” ML models.”(H<sub>02</sub>)

#### Collecting data

I collect the number of ML applications for each "Text Classification" and "Text Generation" model obtained from the top 20 lists, and calculate the source code size of those ML applications. To check for the distribution of given datasets, I perform the Shapiro-Wilk Test to calculate the p-value and plot a histogram of the data to determine if it is normally distributed. 

#### Performing a statistical test

I choose to use the Mann-Whitney U test because the data collected is not normally distributed and the sample size is relatively small (only top 20 of the ML models are considered). In addition, the two comparison groups "Text Classification" and "Text Generation" satisfy the condition of independent samples to perform the testing.

#### Testing the hypothesis

As our sample size is greater than 20, the p value is calculated based on the normal approximation using standardized test statistics. When p is significant, which is smaller than 0.05, I reject the null hypothesis.

In addition, I made several assumptions prior to the analysis.

#### Assumptions
- **Popularity based on the number of downloads** Hugging Face website provides trending (number of likes within recent 7 days), total number of likes and total number of downloads to rank the ML models. I choose to use the total number of downloads of the ML model to rank its popularity for the top 20 ML applications. 
- **Exclude unnecessary files from ML application repositories** When calculating the size of the source code of a ML application repository, I only count sizes of those meaningful development file including codes (.py, .r, .ipynb, .java, .m, .sh, .c, .cc, .cpp) and configuration files (yml, .yaml, .json, .jinja), as other media files are irrelevant and not considered as a factor to evaluate the difficulty for developing and maintaining the ML application.

## Discussion of Results

In the analysis of comparing the total number of ML applications developed using the top-20 "Text Classification" and top-20 "Text Generation" models, I found that there are more ML applications created using "Text Generation" models, where the total number is 3656 versus 757. See `Figure 1`. As the p-value calculated is 0.0114 less than 0.05 with the Mann-Whitney U test, I reject the H_01 and prove that the number of ML applications developed using "Text Generation" models is much larger than using  "Text Classification" models. Thus, it displays that "Text Generation" models are more popular to develop.

<p align="center">
  <img src="./images/5 - Comparison on the total number of spaces developed using Text Generation and Text Classification.png" alt="Comparison on the total number of spaces developed using Text Generation and Text Classification" />
  Figure 1. Comparison on the total number of spaces developed using Text Generation and Text Classification
</p>

In comparison with the source code size of the ML applications developed using the top-20 "Text Classification" and top-20 "Text Generation" models, I found that the average source code size of ML applications created using "Text Classification" models is relatively smaller than using  "Text Generation" models, where the number is 27.94 MB compared with 690.25 MB using "Text Classification" models. See `Figure 2`. As the p-value calculated is 0.002 less than 0.05 with the Mann-Whitney U test, I reject the H_02 and prove that the source code size of ML applications developed using "Text Generation" models is much larger than using "Text Classification" models. Thus, this display that developing ML applications using "Text Generation" models is more complex.

<p align="center">
  <img src="./images/8 - Comparison on the average source code size of spaces developed using Text Generation and Text Classification.png" alt="Comparison on the average source code size of spaces developed using Text Generation and Text Classification" />
  Figure 2. Comparison on the average source code size of spaces developed using Text Generation and Text Classification
</p>

Considering the findings on both factors, I believe that although more developers choose to use  "Text Generation" models to develop ML applications, the average source code size of those application repositories is much larger than using “Text Classification” models, indicating a greater code complexity. This also implies that developers who leverage  "Text Generation" models need to make more efforts to develop external functionalities. 

In addition, there are several limitations for the reliability of the findings.

#### Limitations
- **Small sample size** The number of ML applications collected is only based on the top 20 ML models, which consists of 757 ML applications developed with “Text Classification”.
- **Not perfect mutually exclusive** There are 11 ML applications using models from both “Text Classification” and “Text Generation”.

## Future Improvements
- **Add time periods** I believe it is necessary to consider collecting the data in a designated period of time, such as the recent 6 months. This could ensure two groups of data are coming from the same period. 
- **Research PR commits** It is better to consider exploring the number of PR commits made in the repositories developed using "Text Classification" and "Text Generation" to evaluate the effort needed from developers. 
- **Alternative way of defining popularity** To better understand the preferences of developers, it is better to consider proposing the analysis using the trending (the total number of likes within 7 days) to collect recent information for the utilization of ML models.
