# Lab 2B: Deploying a Service with the Azure ML Designer

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01A.md) and [Lab 1B](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab. You must also complete [Lab 2A](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab02A.md), which includes tasks to create the Designer training pipeline used in this lab.

## Task 1: Prepare Inference Compute

In this lab, you will publish an inference pipeline as a containerized service in an Azure Kubernetes Service (AKS) cluster. An AKS cluster can take some time to initialize, so you'll start the process before preparing your inference pipeline.

1. In [Azure Machine Learning studio](https://ml.azure.com/), on the **Compute** page for your workspace, review the existing compute targets under each tab. These should include:

   - **Compute Instances**: The compute instance you created in a previous lab.
   - **Compute Clusters**: The **aml-cluster** compute target you created in a previous lab.
   - **Inference Clusters**: None (yet!)
   - **Attached Compute**: None (this is where you could attach a virtual machine or Databricks cluster that exists outside of your workspace)

2. In the **Compute Instances** tab, if your compute instance is not already running, start it - you will use it later in this lab.

3. On the **Inference Clusters** tab, add a new cluster with the following settings:

   - **Compute name**: *enter a unique name*
   - **Kubernetes Service**: Create new
   - **Region**: *A region other than the one where your workspace is provisioned*
   - **Virtual Machine size**: Standard_DS2_v2 (*Use the filter to find this in the list*)
   - **Cluster purpose**: Dev-test
   - **Number of nodes**: 2
   - **Network configuration**: Basic
   - **Enable SSL configuration**: Unselected

   > **Note**: Your Azure subscription may have restrictions on the number of cores you can provision, with additional regional restrictions. In this lab, it's important to create your AKS cluster in a different regions from your other compute, and to use the **Dev-test** cluster purpose (to allow your endpoint to be deployed on a cluster with fewer than the 12 core minimum for production clusters) and the **Standard_DS2_v2** virtual machine size (which includes two cores per node, so that your two nodes use only four cores).

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-1.png)

4. Verify that the compute target is in the *Creating* state, and proceed to the next task. Returning periodically to refresh this page and verify that the cluster is being created.

   > **Note**: Creating an AKS cluster can take a significant amount of time. If an error occurs during creation, delete the failed cluster and try again using a different region.

## Task 2: Create an Inference Pipeline

