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

3. Wait for the codespace to be created. This will open a browser-based instance of Visual Studio Code.

4. Wait for a minute or so while the environment is set up for you. It might look like nothing is happening, but in the background we are installing some extensions that you will use in the labs. You'll see the following things happen:

   - A script pane will open to show status as your codespace is prepared.
   - The Visual Studio Code interface will be loaded.
   - The file in this repo will appear in the pane on the left.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-9.png)

5. After setup has completed successfully, you can close the **Creation Log** pane.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-10.png)

   A Visual Studio Codespace is a hosted instance of Visual Studio Code that you can use in a web browser. Visual Studio Code is general code editing environment, with support for various programming languages through the installation of *extensions*. To work with Python, you'll need the Microsoft Python extension, which was installed for you along with some commonly used Python packages when you created this environment from the **DP100** repo.

   The codespace includes an installation of Python(version 3.x), including common packages and support for Jupyter Notebooks within the Visual Studio Code interface. To run code that works with Azure Machine Learning, you just need to install the Azure ML SDK.

6. In the Visual Studio codespace, in the Application Menu (**☰**), on the **View** menu, click **Command Palette** (or press CTRL+SHIFT+P).

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-11.png)

   Then in the Palette, enter the command **Python: Create Terminal**. This opens a Python terminal pane at the bottom of the interface.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-12.png)

7. In the terminal pane, enter the following command to install the Azure Machine Learning SDK (with the optional *notebooks* extra package) using this command:

   ```
   pip install azureml-sdk[notebooks]
   ```

8. Close the Terminal pane.

## Task 3: Use the Azure ML SDK in Visual Studio Codespaces

Now that you have a Python development environment, you can use the Azure Machine Learning SDK in it. First, you need to get the configuration information required to connect to your Azure Machine Learning workspace.

1. In a new browser tab, open the Azure portal at [https://portal.azure.com](https://portal.azure.com/), signing in if necessary.

2. Open the Azure Machine Learning workspace resource you created in the previous lab, and on its **Overview** page, click **Download config.json** and download the file to your local computer.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-13.png)

3. From your local computer, drag the downloaded **config.json** file into the Codespace in your browser, and drop it on the notebook files there. This uploads the config file and opens it in the Codespace editor.

4. Review the contents of the config.json file, and then close it.

5. In your codespace, open the **01B - Intro to the Azure ML SDK.ipynb** notebook - this will be loaded in the Jupyter Notebook interface. It may take a while to load the first time the Jupyter Notebooks interface is used, and you may briefly see two panes - one containing the JSON representation of the notebook, and the other containing the notebook visual interface.

6. When the notebook has loaded, read the notes it contains and run each code cell in turn, just as you did in the Azure Machine Learning Notebook VM Jupyter environment.

## Task 4: Use the Visual Studio Code Azure Machine Learning Extension

If you plan to work with Azure Machine Learning in a Visual Studio codespace (or a local installation of Visual Studio Code), the Azure Machine Learning extension can help make it easier to work with resources in your workspace without needing to switch between your code development environment and the Azure Machine Learning studio web interface.

1. In the Visual Studio codespace interface, click the **Extensions** tab (⊞), and search for "Azure Machine Learning". Then install the **Azure Machine Learning** extension from Microsoft. After the extension has installed, click the **Reload Required** button to reload the environment with the extension.
   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-14.png)

2. In the Visual Studio codespace interface, click the **Azure** tab (***Δ***) and in the **Azure Machine Learning** section, expand your subscription and your Azure Machine Learning workspace.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-15.png)

3. Expand **Compute Clusters** and verify that the **aml-cluster** compute resource you created in your workspace is listed along with a **local** compute resource, which in this case represents the hosted codepace environment - you can run Azure Machine Learning code experiments on local compute as well as on compute resources defined in the workspace.

   ![](https://github.com/ceteongvanness/Designing-and-Implementing-a-Data-Science-Solution-on-Azure/blob/master/images/1B-16.png)

4. Close the Visual Studio codespace browser tab.