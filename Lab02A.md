# Lab 2A: Creating a Training Pipeline with the Azure ML Designer

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01A.md) and [Lab 1B](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab. Then follow these steps to initialize the compute you'll need for this lab:

1. In [Azure Machine Learning studio](https://ml.azure.com/), on the **Compute** page, on the **Compute clusters** tab, click the name of the compute cluster you created previously.

2. Edit your compute cluster to change the **Minimum number of nodes** to 2 (so **both** the **minimum and maximum number of nodes is 2**), and click **Update**. This will ensure that your cluster nodes are always running, and minimize the time you will need to wait for them to start.

   > **Important**: If you decide not to complete this lab, reset the minimum number of nodes to 0 to avoid incurring unnecessary cost.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-1.png)

## Task 1: Create a Designer Pipeline and Explore Data

