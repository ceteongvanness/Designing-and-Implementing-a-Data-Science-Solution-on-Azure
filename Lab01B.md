# Lab 1B: Working with Azure Machine Learning Tools

## Task 1: Use the Azure ML SDK in a Compute Instance

You can perform most asset management tasks to set up your environment in the *Studio* interface, but it's also important to be able to script configuration tasks to make them easier to repeat and automate.

1.  In [Azure Machine Learning studio](https://ml.azure.com/), on the **Compute** page for your workspace, view the **Compute Instances** tab, and if necessary, click **Refresh** periodically until the compute instance you created in the previous lab has started.

2. Refresh the Azure Machine Learning studio web page in your browser to ensure your authenticated session has not expired. Then click your compute instance's **Jupyter** link to open Jupyter Notebooks in a new tab. If prompted, sign in using the Microsoft account associated with your Azure Subscription.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-1.png)

3. In the notebook environment, create a new **Terminal**. This will open a new tab with a command shell.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-2.png)

4. The Azure Machine Learning SDK is already installed in the compute instance image, but it's worth ensuring you have the latest version, with the optional packages you'll need in this course; so enter the following command to update the SDK packages:

   ```
   pip install --upgrade azureml-sdk[notebooks,automl,explain]
   ```

   You may see some warnings as the package dependencies are installed. You can ignore these.

5. Next, run the following commands to change the current directory to the **Users** directory, and retrieve the notebooks you will use in the labs for this course:

   ```
   cd Users
   git clone https://github.com/MicrosoftLearning/DP100
   ```

6. After the command has completed, close the terminal tab and view the home page in your Jupyter notebook file explorer. Then open the **Users** folder - it should contain an **DP100** folder, containing the files you will use in the rest of this lab.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-3.png)

7. In the **Users/DP100** folder, open the **01B - Intro to the Azure ML SDK.ipynb** notebook. Then read the notes in the notebook, running each code cell in turn.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-4.png)

8. When you have finished running the code in the notebook, on the **File** menu, click **Close and Halt** to close it and shut down its Python kernel. Then close all Jupyter browser tabs.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-5.png)

9. If you're finished working with Azure Machine Learning for the day, in Azure Machine Learning studio, on the **Compute** page, select your compute instance and click **Stop** to shut it down. Otherwise, leave it running for the next lab.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-6.png)

##  Task 2: Set Up a Visual Studio Codespace

Compute instances in Azure Machine Learning provide an easy to manage Python environment for working with Azure ML without the need to manage your own Python installation. However, sometimes you may want to use your own graphical Python development environment. In this course, we'll use a Visual Studio Codespace to simplify installation, but the principles of using the Azure Machine Learning SDK are the same in any Python environment.

> **Note**: Visual Studio Codespaces is in *preview* at the time of writing. You may experience some unexpected error messages.

1. In a new browser tab, navigate to [https://online.visualstudio.com](https://online.visualstudio.com/). If prompted, sign into Visual Studio Codespaces using the same Microsoft credentials you used to sign into Azure.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-7.png)

2. Create a codespace with the following settings(if you don't already have a Visual Studio codespaces plan, create one when prompted - this is used to track resource utilization by your codespaces):

   - **Codespace Name**: *A unique name of your choice**
   - **Git Repository**: MicrosoftLearning/DP100
   - **Instance Type**: Standard(Linux)
   - **Suspend idle Codespace after**: 1 Hour

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-8.png)


