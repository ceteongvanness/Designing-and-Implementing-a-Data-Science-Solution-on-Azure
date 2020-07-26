# Lab 3A: Running Experiments

## Before You Start

Experiments are at the core of a data scientist's work. In Azure Machine Learning, an *experiment* is used to run a script or a pipeline, and usually generates outputs and records metrics.

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01A.md) and [Lab 1B](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab.

## Task 1: Run Experiments in a Compute Instance

An Azure Machine Learning Compute Instance provides a useful environment for running experiment code, right in your workspace.

1. In [Azure Machine Learning studio](https://ml.azure.com/), view the **Compute** page for your workspace; and on the **Compute Instances** tab, start your compute instance.

2. When the compute instance is running, refresh the Azure Machine Learning studio web page in your browser to ensure your authenticated session has not expired. Then click the **Jupyter** link to open the Jupyter home page in a new browser tab.
   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/3A-1.png)

3. In the Jupyter home page, in the **Users/DP100** folder, open the **03A - Running Experiments.ipynb** notebook. Then read the notes in the notebook, running each code cell in turn.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/3A-2.png)

4. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/3A-3.png)

5. If you're finished working with Azure Machine Learning for the day, in Azure Machine Learning studio, on the **Compute** page, on the **Compute Instances** tab, select your compute instance and click **Stop** to shut it down. Otherwise, leave it running for the next lab.