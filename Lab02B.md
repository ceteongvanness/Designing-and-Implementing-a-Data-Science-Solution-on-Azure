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
   
   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-2.png)

## Task 2: Create an Inference Pipeline

While the inference compute is being provisioned, you can prepare the inference pipeline for deployment.

1. On the **Designer** page, open the **Visual Diabetes Training** pipeline you created in the previous lab.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-3.png)

2. In the **Create inference pipeline** drop-down list, click **Real-time inference pipeline**. After a few seconds, a new version of your pipeline named **Visual Diabetes Training-real time inference** will be opened.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-4.png)

3. Rename the new pipeline to **Predict Diabetes**, and then review the new pipeline. Note that some of the transformations and training steps have been encapsulated in this pipeline so that the statistics from your training data will be used to normalize any new data values, and the trained model will be used to score the new data.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-5.png)

4. Note that the inference pipeline assumes that new data will match the schema of the original training data, so the **diabetes dataset** dataset from the training pipeline is included. However, this input data includes the **Diabetic** label that the model predicts, which is unintuitive to include in new patient data for which a diabetes prediction has not yet been made.

5. Delete this the **diabetes dataset** dataset from the inference pipeline and replace it with an **Enter Data Manually** module from the **Data Input and Output** section of the **Modules** tab; connecting it to the same **dataset** input of the **Apply Transformation** module as the **Web Service Input**. Then modify the settings of the **Enter Data Manually** module to use the following **CSV** input, which includes feature values without labels for three new patient observations:

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-6.png)

6. The inference pipeline includes the **Evaluate Model** module, which is not useful when predicting from new data, so **delete** this module.

7. Note that the output from the **Score Model** module includes all of the input features as well as the predicted label and probability score.

8. To limit the output to only the prediction and probability, **delete the connection** between the **Score Model** module and the **Web Service Output**, add an **Execute Python Script** module from the **Python Language** section, connect the output from the **Score Model** module to the **Dataset1** (left-most) input of the **Execute Python Script**, and connect the output of the **Execute Python Script** module to the **Web Service Output**. 

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-8.png)

   Then modify the settings of the **Execute Python Script** module to use the following code (replacing all existing code):

   ```python
   import pandas as pd
   
   def azureml_main(dataframe1 = None, dataframe2 = None):
   
       scored_results = dataframe1[['PatientID', 'Scored Labels', 'Scored Probabilities']]
       scored_results.rename(columns={'Scored Labels':'DiabetesPrediction',
                                      'Scored Probabilities':'Probability'},
                             inplace=True)
       return scored_results
   ```

9. Verify that your pipeline looks similar to the following:

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2B-7.png)

10. **Submit** the pipeline as a new experiment named **predict-diabetes** on the compute cluster you used for training. This may take a while!