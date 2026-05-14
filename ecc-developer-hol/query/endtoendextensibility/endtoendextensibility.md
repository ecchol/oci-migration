# Additional End-to-End Extensibility Scenario

## Introduction

In this lab, you will extend the existing orders dashboard by introducing returns insights and enabling cross-dataset analytics.

You will learn how an administrator creates a data set view and how a power user leverages that view to build advanced analytics, including:

- Time Series trends
- Pivot analysis
- Cross-dataset calculations

Estimated Time: 30 minutes

## Objectives

By the end of this lab, you will be able to:

**Administrator**

- Create a Data Set View
- Configure attribute selection and labeling
- Define associations between datasets

**Power User**

- Use the new Data Set View
- Create and enhance dashboard components:
  - Time Series charts
  - Pivot analysis
  - Cross-dataset calculations

## Prerequisites

This lab assumes you have:

- Completed all previous labs successfully

## Task 1: Administrator Tasks

**Goal**: As an admin user, I want to create and configure a Returns Data Set View and define relationships with Orders data so that cross-dataset analytics can be enabled for business users.

A data set view is a flexible mechanism for creating different perspectives of a base data set. It functions as a physical copy of the existing data set while maintaining a strong dependency on the parent for metadata and loading logic. This approach enables the efficient generation of multiple contextual views of the same data source without duplicating the extraction process.

### Task 1.1: Create a Returns Data Set View

1. Log in to EBS apps (From the browser URL, navigate to http://<VNC_Public_IP>:8000) with the below credentials

```
Username: sysadmin
Password: welcome1
```

2. Navigate to ECC Developer -> ECC Developer

![image-2026-4-30_16-31-7](../images/image-2026-4-30_16-31-7.png)

3. Go to the "Data Sets and Views" menu under the "Data Designer" section

![image-2026-4-30_16-45-20](../images/image-2026-4-30_16-45-20.png)

4. Click on the "New View" button, then select "Data Set View"

![image-2026-4-30_16-45-40](../images/image-2026-4-30_16-45-40.png)

5. Provide the details below:

- Select Data Set: Return Lines (ont-rlines)
- Data Set View Key: ont-rlines-view
- View Display Name: Return Lines View
- Icon: Sales Order

6. Click on the "Save" button.

![image-2026-4-30_16-46-15](../images/image-2026-4-30_16-46-15.png)

### Task 1.2: Update metadata attributes

1. In the ECC Developer page, go to the "Metadata" menu under the "Data Designer" section

![image-2026-4-30_16-46-35](../images/image-2026-4-30_16-46-35.png)

2. Choose the data set view from the dropdown "Return Lines View"

![image-2026-4-30_16-44-46](../images/image-2026-4-30_16-44-46.png)

![image-2026-4-30_16-54-13](../images/image-2026-4-30_16-54-13.png)

Only the Attributes tab is visible in the metadata section, and operations such as add, delete, or import are disabled. Attribute properties cannot be edited, but a new control is introduced to disable attributes selectively

3. Disable technical attributes

Search for ID attributes, then click on "Hide"

![image-2026-4-30_16-58-15](../images/image-2026-4-30_16-58-15.png)

4. Click "Save"

![image-2026-4-30_17-0-5](../images/image-2026-4-30_17-0-5.png)

### Task 1.3: Define Association

1. Define association with **Return Lines (ont-rlines)**:
   1. In the Metadata page, select **Return Lines (ont-rlines)** from the data set/view list.
   2. Go to the **Association** tab.

![image-2026-4-30_17-5-0](../images/image-2026-4-30_17-5-0.png)

![image-2026-4-30_17-5-47](../images/image-2026-4-30_17-5-47.png)

   3. Click **Add** to create a new association between **Return Lines** and **Return Lines View**.
   4. Provide the details below:
      - Source Attribute: Product
      - Target Data Set: Return Lines View
      - Target Attribute: Product
   5. Click **Add** again and provide the details below:
      - Source Attribute: Customer Number
      - Target Data Set: Return Lines View
      - Target Attribute: Customer Number
   6. Click **Save**.

![image-2026-4-30_17-13-19](../images/image-2026-4-30_17-13-19.png)

2. Define association with **Order Lines (ont-lines)**:
   1. In the Metadata page, select **Order Lines (ont-lines)** from the data set/view list.
   2. Go to the **Association** tab.
   3. Click **Add** to create a new association between **Order Lines** and **Return Lines View**.
   4. Provide the details below:
      - Source Attribute: Product
      - Target Data Set: Return Lines View
      - Target Attribute: Product
   5. Click **Add** again and provide the details below:
      - Source Attribute: Customer Number
      - Target Data Set: Return Lines View
      - Target Attribute: Customer Number
   6. Click **Save**.

![image-2026-4-30_17-18-23](../images/image-2026-4-30_17-18-23.png)

### Task 1.4: Assign the Data Set View to the Application

1. Go to the ECC Developer home page

2. Search for the "Order Management" application

3. Click on the edit icon for the application

![image-2026-4-30_18-46-35](../images/image-2026-4-30_18-46-35.png)

4. Assign the data set view "Return Lines View" to the application

5. Click on the "Save" button

![image-2026-4-30_18-47-32](../images/image-2026-4-30_18-47-32.png)

## Task 2: Power User Tasks

**Goal**: As a power user, I want to compare orders and returns over time, by customer, and by product so that I can identify trends, evaluate performance, and take corrective action.

### Task 2.1: Personalize Orders Dashboard

1. Login to EBS apps (Navigate to http://<VNC_Public_IP>:8000) with below credentials:
   - Username: eccuser
   - Password: welcome1

2. Navigate to Order Management, HTML User Interface -> Command Center -> Orders Dashboard

![image-2026-5-4_14-19-22](../images/image-2026-5-4_14-19-22.png)

3. Enable Personalization Mode by clicking on the "i" icon (on the top left of the page, beside the share icon) and then click on the "Personalize" button.

![image-2026-5-4_14-22-19](../images/image-2026-5-4_14-22-19.png)

4. Add a new tab in the existing tab component. To do this, you need to click on the configuration icon for the existing Tab component and then add a new Tab in it. Name this tab "Order Insights"

5. Click on "Save"

![image-2026-5-4_14-24-48](../images/image-2026-5-4_14-24-48.png)

![image-2026-5-4_14-27-16](../images/image-2026-5-4_14-27-16.png)

6. Add a chart component inside the new tab "Order Insights" by dragging and dropping the chart component within the tab layout, to compare Orders and Returns over time

- Enable Multi Dataset checkbox
- Add Data Set:
  - Order Lines
    - dataset alias: Orders
  - Return Lines View
    - dataset alias: Returns
- Chart type: Bar
- Dimension: Order Date (series dimension)
- Time Dimension
  - Order date
  - Time Grain: Yearly
- Metric (by default, multi-metric is selected):
  - Orders - Order Number (count distinct) - custom label: Orders Count - Show as line
  - Returns- Order Number (count distinct) - custom label: Returns Count - Show as line

7. Click "Preview"

![image-2026-5-4_14-35-47](../images/image-2026-5-4_14-35-47.png)

8. This gives a comparison between orders and returns count over time; now add a reference line to show the average count for orders and returns.

- Expand "Y-Axis Reference Lines", and click on "Add Y-Axis Reference Lines"
  - Orders - Order Number (Count Distinct) - Average
  - Returns - Order Number (Count Distinct) - Average

![image-2026-5-4_14-40-18](../images/image-2026-5-4_14-40-18.png)

9. Now, give color coding to the chart metrics; navigate to "Color Pinning" then click "Enable Color Pinning"

10. Click on "Add Color"

- Select metric: Orders - Order Number (Count Distinct)
- Color: green

11. Click on "Add Color"

- Select metric: Returns- Order Number (Count Distinct)
- Color: orange

![image-2026-5-4_14-46-37](../images/image-2026-5-4_14-46-37.png)

12. Click on "Save"

13. In addition of comparing Orders and Returns over time, add a Pivot view under "Order Insights" tab to compare orders and returns by product and customer:

- Add New Component - **Aggregate Table** (Pivot view is an alternate visualization of the Aggregate Table component).
- Enable **Multi dataset** checkbox.
- Add Data Set:
  - Order Lines (dataset alias: Orders)
  - Return Lines View (dataset alias: Returns)
- Attributes:
  - Select attributes, then click **Add Attribute**
  - Product
  - Product Description
  - Sales Channel
  - Select Metric, then click **Add Attribute**
  - Orders - Order Number (count distinct), custom label: Orders Count
  - Returns - Order Number (count distinct), custom label: Returns Count

14. Click "Preview". This gives orders count and returns count per product, product description and sales channel.

![image-2026-5-4_16-44-44](../images/image-2026-5-4_16-44-44.png)

15. To improve the comparison capability, add calculation to calculate net orders and return rate

- Click "Add Calculation"
  - Add Label: Net Orders
  - Enter Formula
    - Select the "-" sign
    - Click the "+" sign, then add metric: Orders - Order Number (Count Distinct)
    - Click the "+" sign, then add metric: Returns - Order Number (Count Distinct)
  - Validate Formula " ("Orders - Order Number (Count Distinct)" - "Returns - Order Number (Count Distinct)")"
  - Select Number Formatting: General
- Click "Preview"

![image-2026-5-4_16-52-58](../images/image-2026-5-4_16-52-58.png)

16. Add another calculation for "Return Rate"

- Click "Add Calculation"
  - Add Label: Return Rate
  - Enter Formula
    - Select the "/" sign
    - Click the "+" sign, then add metric: Returns - Order Number (Count Distinct)
    - Click the "+" sign, then add metric: Orders - Order Number (Count Distinct)
  - Validate Formula " ("Returns - Order Number (Count Distinct)" / "Orders - Order Number (Count Distinct)")"
  - Select Number Formatting: Formatted Number
- Click "Preview"

![image-2026-5-4_16-57-47](../images/image-2026-5-4_16-57-47.png)

17. Now, to improve the comparison visually, add conditional formatting for the return rate

- Expand "Conditional Formatting"
- Click Add Condition
  - Select color | when value is
    - Green | = 0.00
    - Red | >= 0.91
    - Orange | b/w 0.01 and 0.90
- Click "Preview"

![image-2026-5-4_17-4-22](../images/image-2026-5-4_17-4-22.png)

18. Click "Save"

![image-2026-5-4_17-11-46](../images/image-2026-5-4_17-11-46.png)
