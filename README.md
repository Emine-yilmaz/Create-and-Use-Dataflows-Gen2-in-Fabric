# Create and Use Dataflows (Gen2) in Microsoft Fabric

This lab demonstrates how to create and use Dataflows (Gen2) in Microsoft Fabric to ingest and transform data before loading it into a lakehouse. You will learn to connect to a data source, perform transformations using Power Query Online, define a data destination, and then orchestrate the dataflow execution using a pipeline.

**Estimated Completion Time:** 30 minutes

**Prerequisites:**

* A Microsoft Fabric trial enabled.

## Steps

### 1. Create a Workspace

1.  Navigate to the [Microsoft Fabric home page](https://app.fabric.microsoft.com/home?experience=fabric) and sign in with your Fabric credentials.
2.  In the left-hand menu bar, select **Workspaces** (🗇).
3.  Create a **New workspace** with a name of your choice, selecting a licensing mode that includes Fabric capacity (Trial, Premium, or Fabric).
4.  Once the workspace is created and opened, it should be empty.

### 2. Create a Lakehouse

1.  In the left-hand menu bar, select **Create**. Under the **Data Engineering** section, choose **Lakehouse**. Give it a unique name.
    * **Note:** If the **Create** option is not visible, click the ellipsis (**...**) first.
2.  After a short delay, a new empty lakehouse will be created.

### 3. Create a Dataflow (Gen2) to Ingest Data

1.  In the home page for your workspace, select **Get data > New Dataflow Gen2**.
2.  The Power Query editor for your new dataflow will open.
3.  Select **Import from a Text/CSV file** and configure a new data source with the following settings:
    * **Link to file:** Selected
    * **File path or URL:** `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/orders.csv`
    * **Connection:** `Create new connection`
    * **data gateway:** `(none)`
    * **Authentication kind:** `Anonymous`
4.  Select **Next** to preview the file data, and then **Create** the data source.
5.  In the Power Query editor, on the toolbar ribbon, select the **Add column** tab.
6.  Select **Custom column** and create a new column with the following settings:
    * **New column name:** `MonthNo`
    * **Data type:** `Whole Number`
    * **Custom column formula:** `Date.Month([OrderDate])`
7.  Select **OK** to create the column. Observe the new `MonthNo` column and the added step in the **Applied Steps** pane.
8.  In the **Query Settings** pane (right side), review the **Applied Steps** and optionally toggle the **Diagram flow** button to visualize the steps.
9.  Confirm that the data type for the **OrderDate** column is set to **Date** and the data type for the **MonthNo** column is set to **Whole Number**.

### 4. Add Data Destination for Dataflow

1.  On the toolbar ribbon, select the **Home** tab.
2.  In the **Add data destination** drop-down menu, select **Lakehouse**.
    * **Note:** If this option is grayed out, check the data destination at the bottom of the **Query settings** pane. Use the gear icon to change it if necessary.
3.  In the **Connect to data destination** dialog box, edit the connection and sign in using your Power BI organizational account.
4.  Select **Next**.
5.  In the list of available workspaces, find your workspace and select the lakehouse you created.
6.  Specify a new table name as `orders`.
7.  Select **Next**.
8.  On the **Choose destination settings** page, disable the **Use automatic settings** option, select **Append**, and then **Save settings**.
9.  On the Menu bar, open **View** and select **Diagram view** to see the Lakehouse destination icon in the query.
10. Select **Publish** to publish the dataflow. Wait for the dataflow (likely named `Dataflow 1`) to be created in your workspace.

### 5. Add a Dataflow to a Pipeline

1.  Ensure you are in the **Data Engineering** experience in your Fabric-enabled workspace.
2.  Select **+ New item > Data pipeline**. Name the new pipeline `Load data`.
3.  Close the **Copy Data** wizard if it appears automatically.
4.  Select **Add pipeline activity** and add a **Dataflow** activity to the pipeline.
5.  With the new **Dataflow1** activity selected, on the **Settings** tab, in the **Dataflow** drop-down list, select **Dataflow 1** (the data flow you created).
6.  On the **Home** tab, save the pipeline using the **🖫** (Save) icon.
7.  Use the **▷ Run** button to execute the pipeline. Wait for it to complete (this may take a few minutes).

### 6. Verify Data in the Lakehouse

1.  In the menu bar on the left edge, select your lakehouse.
2.  In the **...** menu for **Tables**, select **refresh**.
3.  Expand **Tables** and select the **orders** table. You should see the data ingested by your dataflow.

### 7. Clean Up Resources

1.  Navigate to Microsoft Fabric in your browser.
2.  In the left-hand bar, select the icon for your workspace.
3.  Select **Workspace settings**.
4.  In the **General** section, scroll down and select **Remove this workspace**.
5.  Select **Delete** to delete the workspace.

Congratulations! You have successfully created and used a Dataflow (Gen2) in Microsoft Fabric to ingest and load data into a lakehouse using a pipeline.
