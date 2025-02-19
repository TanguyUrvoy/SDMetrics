<div align="center">
<br/>
<p align="center">
    <i>This repository is part of <a href="https://sdv.dev">The Synthetic Data Vault Project</a>, a project from <a href="https://datacebo.com">DataCebo</a>.</i>
</p>

[![Development Status](https://img.shields.io/badge/Development%20Status-2%20--%20Pre--Alpha-yellow)](https://pypi.org/search/?c=Development+Status+%3A%3A+2+-+Pre-Alpha)
[![PyPI Shield](https://img.shields.io/pypi/v/sdmetrics.svg)](https://pypi.python.org/pypi/sdmetrics)
[![Downloads](https://pepy.tech/badge/sdmetrics)](https://pepy.tech/project/sdmetrics)
[![Tests](https://github.com/sdv-dev/SDMetrics/workflows/Run%20Tests/badge.svg)](https://github.com/sdv-dev/SDMetrics/actions?query=workflow%3A%22Run+Tests%22+branch%3Amaster)
[![Coverage Status](https://codecov.io/gh/sdv-dev/SDMetrics/branch/master/graph/badge.svg)](https://codecov.io/gh/sdv-dev/SDMetrics)

<div align="left">
<br/>
<p align="center">
<a href="https://github.com/sdv-dev/SDV">
<img align="center" width=40% src="https://github.com/sdv-dev/SDV/blob/master/docs/images/SDMetrics-DataCebo.png"></img>
</a>
</p>
</div>

</div>

# Overview

The SDMetrics library evaluates synthetic data by comparing it to the real data that you're trying to mimic. It includes a variety of metrics to capture different aspects of the data, for example **quality and privacy**. It also includes reports that you can run to generate insights and share with your team.

The SDMetrics library is **model-agnostic**, meaning you can use any synthetic data. The library does not need to know how you created the data. 


| Important Links                               |                                                                      |
| --------------------------------------------- | -------------------------------------------------------------------- |
| :computer: **[Website]**                      | Check out the SDV Website for more information about the project.    |
| :orange_book: **[Blog]**                      | A deeper look at open source, synthetic data creation and evaluation.|
| :book: **[Documentation]**                    | Quickstarts, User and Development Guides, and API Reference.         |
| :octocat: **[Repository]**                    | The link to the Github Repository of this library.                   |
| :scroll: **[License]**                        | The library is published under the MIT License.                      |
| :keyboard: **[Development Status]**           | This software is in its Pre-Alpha stage.                             |
| [![][Slack Logo] **Community**][Community]    | Join our Slack Workspace for announcements and discussions.          |
| [![][Google Colab Logo] **Tutorials**][Tutorials] | Get started with SDMetrics in a notebook.                        |

[Website]: https://sdv.dev
[Blog]: https://datacebo.com/blog
[Documentation]: https://docs.sdv.dev/sdmetrics
[Repository]: https://github.com/sdv-dev/SDMetrics
[License]: https://github.com/sdv-dev/SDMetrics/blob/master/LICENSE
[Development Status]: https://pypi.org/search/?c=Development+Status+%3A%3A+2+-+Pre-Alpha
[Slack Logo]: https://github.com/sdv-dev/SDV/blob/master/docs/images/slack.png
[Community]: https://bit.ly/sdv-slack-invite
[Google Colab Logo]: https://github.com/sdv-dev/SDV/blob/master/docs/images/google_colab.png
[Tutorials]: https://bit.ly/sdmetrics-demo

## Features

Quickly generate insights and share results with your team using **SDMetrics Reports**. For example, the Diagnostic Report quickly checks for common problems, and the Quality Report provides visualizations comparing the real and synthetic data.

<img align="center" src="docs/images/column_comparison.png"></img>

You can also explore and apply individual metrics as needed. The SDMetrics library includes a variety of metrics for different goals:

* Privacy metrics evaluate whether the synthetic data is leaking information about the real data
* ML Efficacy metrics estimate the outcomes of using the synthetic data to solve machine learning problems
* … and more! 

Some of these metrics are experimental and actively being researched by the data science community.

# Install

Install SDMetrics using pip or conda. We recommend using a virtual environment to avoid conflicts with other software on your device.

**Using `pip`:**

```bash
pip install sdmetrics
```

**Using `conda`:**

```bash
conda install -c conda-forge -c pytorch sdmetrics
```

For more installation options please visit the [SDMetrics installation Guide](https://github.com/sdv-dev/SDMetrics/blob/master/INSTALL.md).

# Usage

Get started with **SDMetrics Reports** using some demo data,

```python
from sdmetrics import load_demo
from sdmetrics.reports.single_table import QualityReport

real_data, synthetic_data, metadata = load_demo(modality='single_table')

my_report = QualityReport()
my_report.generate(real_data, synthetic_data, metadata)
```
```
Creating report: 100%|██████████| 4/4 [00:00<00:00,  5.22it/s]

Overall Quality Score: 82.84%

Properties:
Column Shapes: 82.78%
Column Pair Trends: 82.9%
```

Once you generate the report, you can drill down on the details and visualize the results.

```python
my_report.get_visualization(property_name='Column Pair Trends')
```
<img align="center" src="docs/images/column_pairs.png"></img>

Save the report and share it with your team.
```python
my_report.save(filepath='demo_data_quality_report.pkl')

# load it at any point in the future
my_report = QualityReport.load(filepath='demo_data_quality_report.pkl')
```

**Want more metrics?** You can also manually apply any of the metrics in this library to your data.

```python
# calculate whether the synthetic data respects the min/max bounds
# set by the real data
from sdmetrics.single_table import BoundaryAdherence

BoundaryAdherence.compute(
    real_data['start_date'],
    synthetic_data['start_date']
)
```
```
0.8503937007874016
```

```python
# calculate whether an attacker will be able to guess sensitive 
# information based on combination of synthetic data and their
# own information
from sdmetrics.single_table import CategoricalCAP

CategoricalCAP.compute(
    real_data,
    synthetic_data,
    key_fields=['gender', 'work_experience'],
    sensitive_fields=['degree_type']
)
```
```
0.4601209799017264
```

# What's next?

To learn more about the reports and metrics, visit the [SDMetrics Documentation](https://docs.sdv.dev/sdmetrics). 

---


<div align="center">
<a href="https://datacebo.com"><img align="center" width=40% src="https://github.com/sdv-dev/SDV/blob/master/docs/images/DataCebo.png"></img></a>
</div>
<br/>
<br/>

[The Synthetic Data Vault Project](https://sdv.dev) was first created at MIT's [Data to AI Lab](
https://dai.lids.mit.edu/) in 2016. After 4 years of research and traction with enterprise, we
created [DataCebo](https://datacebo.com) in 2020 with the goal of growing the project.
Today, DataCebo is the proud developer of SDV, the largest ecosystem for
synthetic data generation & evaluation. It is home to multiple libraries that support synthetic
data, including:

* 🔄 Data discovery & transformation. Reverse the transforms to reproduce realistic data.
* 🧠 Multiple machine learning models -- ranging from Copulas to Deep Learning -- to create tabular,
  multi table and time series data.
* 📊 Measuring quality and privacy of synthetic data, and comparing different synthetic data
  generation models.

[Get started using the SDV package](https://sdv.dev/SDV/getting_started/install.html) -- a fully
integrated solution and your one-stop shop for synthetic data. Or, use the standalone libraries
for specific needs.
