# Lab 2A: Creating a Training Pipeline with the Azure ML Designer

## Before You Start

Before you start this lab, ensure that you have completed [Lab 1A](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01A.md) and [Lab 1B](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/Lab01B.md), which include tasks to create the Azure Machine Learning workspace and other resources used in this lab. Then follow these steps to initialize the compute you'll need for this lab:

1. In [Azure Machine Learning studio](https://ml.azure.com/), on the **Compute** page, on the **Compute clusters** tab, click the name of the compute cluster you created previously.

2. Edit your compute cluster to change the **Minimum number of nodes** to 2 (so **both** the **minimum and maximum number of nodes is 2**), and click **Update**. This will ensure that your cluster nodes are always running, and minimize the time you will need to wait for them to start.

   > **Important**: If you decide not to complete this lab, reset the minimum number of nodes to 0 to avoid incurring unnecessary cost.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-1.png)

## Task 1: Create a Designer Pipeline and Explore Data

To get started with Designer, first you must create a pipeline and add the dataset you want to work with.

1. In [Azure Machine Learning studio](https://ml.azure.com/) for your workspace, view the **Designer** page and create a new pipeline.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-2.png)

2. In the **Settings** pane, change the default pipeline name (**Pipeline-Created-on-\*date\***) to **Visual Diabetes Training** (if the **Settings** pane is not visible, click the **⚙** icon next to the pipeline name at the top).

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-3.png)

3. Note that you need to specify a compute target on which to run the pipeline. In the **Settings** pane, click **Select compute target** and select your compute cluster.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-4.png)

4. On the left side of the designer, select the **Datasets** (⌕) tab, expand the **Datasets** section, and drag the **diabetes dataset** dataset you created in the previous exercise onto the canvas.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-5.png)

5. Select the **diabetes dataset** module on the canvas, and view its settings (the settings pane for the dataset may open automatically and cover the canvas). Then on the **outputs** tab, click the **Visualize** icon (which looks like a column chart).

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-6.png)

6. Review the schema of the data, noting that you can see the distributions of the various columns as histograms. Then close the visualization, and then close or minimize the settings pane using the X or **↗↙** icon so you can see the pipeline canvas with the dataset on it.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-7.png)

## Task 2: Add Transformations

Before you can train a model, you typically need to apply some preprocessing transformations to the data.

1. In the pane on the left, view the **Modules** (⊞) tab and expand the **Data Transformation** section, which contains a wide range of modules you can use to transform data before model training.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-8.png)

2. Drag a **Normalize Data** module to the canvas, below the **diabetes dataset** module. Then connect the output from the **diabetes dataset** module to the input of the **Normalize Data** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-9.png)

3. Select the **Normalize Data** module and view its settings, noting that it requires you to specify the transformation method and the columns to be transformed. Then, leaving the transformation as **ZScore**, edit the columns to includes the following column names:

   - PlasmaGlucose
   - DiastolicBloodPressure
   - TricepsThickness
   - SerumInsulin
   - BMI
   - DiabetesPedigree

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-10.png)
   **Note**: We're normalizing the numeric columns put them on the same scale, and avoid columns with large values dominating model training. You'd normally apply a whole bunch of pre-processing transformations like this to prepare your data for training, but we'll keep things simple in this exercise.

4. Now we're ready to split the data into separate datasets for training and validation. In the pane on the left, in the **Data Transformations** section, drag a **Split Data** module onto the canvas under the **Normalize Data** module. 

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-11.png)

   Then connect the *Transformed Dataset* (left) output of the **Normalize Data** module to the input of the **Split Data** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-12.png)

5. Select the **Split Data** module, and configure its settings as follows:

   - **Splitting mode** Split Rows
   - **Fraction of rows in the first output dataset**: 0.7
   - **Random seed**: 123
   - **Stratified split**: False

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-13.png)

## Task 3: Add Model Training Modules

With the data prepared and split into training and validation datasets, you're ready to configure the pipeline to train and evaluate a model.

1. Expand the **Model Training** section in the pane on the left, and drag a **Train Model** module to the canvas, under the **Split Data** module. Then connect the *Result dataset1* (left) output of the **Split Data** module to the *Dataset* (right) input of the **Train Model** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-14.png)

2. The model we're training will predict the **Diabetic** value, so select the **Train Model** module and modify its settings to set the **Label column** to **Diabetic** (matching the case and spelling exactly!)

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-15.png)

3. The **Diabetic** label the model will predict is a binary column (1 for patients who have diabetes, 0 for patients who don't), so we need to train the model using a *classification* algorithm. Expand the **Machine Learning Algorithms** section, and under **Classification**, drag a **Two-Class Logistic Regression** module to the canvas, to the left of the **Split Data** module and above the **Train Model** module. Then connect its output to the **Untrained model** (left) input of the **Train Model** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-16.png)

4. To test the trained model, we need to use it to score the validation dataset we held back when we split the original data. Expand the **Model Scoring & Evaluation** section and drag a **Score Model** module to the canvas, below the **Train Model** module. Then connect the output of the **Train Model** module to the **Trained model** (left) input of the **Score Model** module; and drag the **Results dataset2** (right) output of the **Split Data** module to the **Dataset** (right) input of the **Score Model** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-17.png)

5. To evaluate how well the model performs, we need to look at some metrics generated by scoring the validation dataset. From the **Model Scoring & Evaluation** section, drag an **Evaluate Model** module to the canvas, under the **Score Model** module, and connect the output of the **Score Model** module to the **Score dataset** (left) input of the **Evaluate Model** module.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/2A-18.png)