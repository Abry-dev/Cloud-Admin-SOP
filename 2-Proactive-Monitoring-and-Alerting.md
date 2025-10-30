# Azure: Proactive Monitoring and Alerting

## Step 1: Configure Log Analytics and Data Collection

1.  Search **Log Analytics Workspace** and click **Create**
    1.  Select resource group and name it: **LA-Support**
    2.  Click **review + create**, then **create**
2.  Navigate to **LA-Support** resource
    1.  Underneath **Monitoring**, click **Diagnostics settings**
    2.  Click **Add diagnostic setting**
    3.  Check the boxes for **allLogs** and **AllMetrics**, for Destination details, click **Send to Log Analytics Workspace**
        1.  Set Log Analytics workspace to **LA-Support**
    4.  Name it: **Diagnostic** and click **Save**

## Step 2: Create Alerts and Action Groups

1.  Search **Monitor**
    1.  Click **Alerts**, then click **Action Groups**
        1.  Click **Create**
        2.  Set resource group
        3.  Action group name: **AG-Support-Email**
        4.  Display name: **Email**
        5.  Click **notifications** and set notification type as email/SMS message/Push/Voice
            * Check email and input your email address
        6.  Click **review + create**, then **create**
2.  Search **Monitor**
    1.  Click **Alerts**, then click **Alert rules**
        1.  Click **Create**
        2.  Select **Scope**
            * Click on resource group arrow then click on **VM-Web1**
        3.  Click **Condition**
            * Set Signal as **Percentage CPU**
            * Set Aggregation type as **Average**
            * Set Value as **Great than**
            * Set Threshold as **90**
            * Set Check every as **5 minutes**
        4.  Click **Actions**
            * Under Select Action groups, click **AG-Support-Email**
        5.  Click **Details**
            * Set Severity to **1**
            * Set Alert rule name to **Alert-HighCPU**
        6.  Click **review + create**
