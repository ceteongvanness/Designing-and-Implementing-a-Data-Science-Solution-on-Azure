# Lab 1A: Creating an Azure Machine Learning Workspace
## Task 1: Create an Azure ML Workspace

As its name suggests, a workspace is a centralized place to manage all of the Azure ML assets you need to work on a machine learning project.

1. Go to https://ml.azure.com, select the **Directory** and **Subscription**.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-1.png)

2. In **Machine Learning workspace**, click on **+ Create a New workspace**

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-2.png)

3. In the Azure portal, specifying a unique workspace name and creating a new resource group in the region nearest your location. Select the **Enterprise** workspace edition. Click **Review + create** button.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-3.png)

4. Click on **Create** button.

5. Back to **Step 1** page, click on **Refresh workspaces**. You will see the workspace and select that workspace that created just now. Click on **Get Started** button.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-4.png)

## Task 2: Explore the Azure ML Studio Interface

You can manage workspace assets in the Azure portal, but for data scientists, this tool contains lots of irrelevant information and links that relate to managing general Azure resources. An alternative, Azure ML-specific web interface for managing workspaces is available.

1. View the Azure Machine Learning studio interface for your workspace - you can manage all of the assets in your workspace from here.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-5.png)

## Task 3: Create Compute Resources

One of the benefits of Azure Machine Learning is the ability to create cloud-based compute on which you can run experiments and training scripts at scale.

1. In the Azure Machine Learning studio web interface for your workspace, view the **Compute** page. This is where you'll manage all the compute targets for your data science activities.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-6.png)

2. On the **Compute instances** tab, click on **Create** button to add a new compute instance with the following settings. You'll use this as a workstation from which to test your model:

   - **Compute name**: *enter a unique name*
   - **Virtual Machine type**: CPU
   - **Virtual Machine size**: Standard_DS1_v2
     ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-7.png)

3. While the compute instance is being created, switch to the **Compute Clusters** tab and add a new compute cluster with the following settings. You'll use this to train a machine learning model:

   - **Compute name**: *enter a unique name*
   - **Virtual Machine type**: CPU
   - **Virtual Machine priority**: Dedicated
   - **Virtual Machine size**: Standard_DS2_v2
   - **Minimum number of nodes**: 0
   - **Maximum number of nodes**: 2
   - **Idle seconds before scale down**: 120
     ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-8.png)

4. Note the **Inference Cluster** tab. This is where you can create and manage compute targets on which to deploy your trained models as web service for client applications to consume.

5. Note the **Attached Compute** tab. This is where you could attach a virtual machine or Databricks cluster that exists outside of your workspace.

## Task 4: Create Data Resources

Now that you have some compute resources that you can use to process data, you'll need a way to store and ingest the data to be processed.

1. In the *Studio* interface, view the **Datastores** page. Your Azure ML workspace already includes two datastores based on the Azure Storage account that was created along with the workspace. These are used to store notebooks, configuration files, and data.

   > **Note**: In the real-world environment, you'd likely add custom datastores that reference your business data stores - for example, Azure blob containers, Azure Data Lakes, Azure SQL Databases, and so on.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-9.png)

2. In the *Studio* interface, view the **Datasets** page. Datasets represent specific data files or tables that you plan to work with in Azure ML.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-10.png)

3. Create a new dataset **from web files**, using the following settings:

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-11.png)

   - **Basic Info**:

     - **Web URL**: https://aka.ms/diabetes-data

     - **Name**: diabetes dataset (*be careful to match the case and spacing*)

     - **Dataset type**: Tabular

     - **Description**: Diabetes data

       ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-12.png)

   - **Settings and preview**:

     - **File format**: Delimited

     - **Encoding**: Comma

     - **Column headers**: Use headers from first file

     - **Skip rows**: None

       ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-13.png)

   - **Schema**:

     - Include all columns other than **Path**

     - Review the automatically detected types

       ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-14.png)

   - **Confirm details**:

     - Do not profile the datasets after creation

       ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-15.png)
4. After the dataset has been created, open it and view the **Explore** page to see a sample of the data. This data represents details from patients who have been tested for diabetes.

![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1A-16.png)
       










