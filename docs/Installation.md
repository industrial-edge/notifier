# Configuration

- [Configuration](#configuration)
  - [Configure PLC project](#configure-plc-project)
  - [Configure PLC Connection](#configure-plc-connection)
  - [Configure Performance Insight](#configure-performance-insight)
  - [Configure Notifier](#configure-notifier)

## Configure PLC project

1) Open TIA portal and open the project containing the filling application
2) Download the PLC program to the PLC and set the PLC into RUN
3) Open the HMI to control the filling application

## Configure PLC Connection

To read data from the PLC and provide the data, we will use S7 Connector to establish connection with the PLC via OPC UA.
The S7 Connector sends the data to the Databus, where the Data Service app can collect what is needed for the notification rules.
In order to build this infrastructure, these apps must be configured properly:

- IE Databus
- S7 Connector
- Data Service

Please refer to [using the Data Service](https://github.com/industrial-edge/data-service).

Finally the configurations should look like this:

**IE Databus**

![1](graphics/1_Databus.PNG)

**S7 Connector**

![2](graphics/2_S7_Connector.PNG)

**Data Service**

![3](graphics/3_DataService.PNG)

## Configure Performance Insight

In order to create a KPI and assign appropriate variables, we need to use the Performance Insight app.
Limit values and activate notifications can be configured here, which will be forwarded to the Notifier.

Open the user interface of the Performance Insight app on your IE Device. On the left bar navigate to Configuration > KPI types and click "New KPI type".
Create a new KPI "production quality" with the following formula (`<faulty>` and `<produced>` are operands)

`100 - (<faulty> / <produced> * 100%)`

![4_1](graphics/4_1_PerformanceInsight.png)

Navigate to My Plant > filling application > Parameter (drop down menu on the top of the heading).

![4_2](graphics/4_2_PerformanceInsight.png)

Choose 'New KPI instance' to create a new instance according to the following settings:

![4_3](graphics/4_3_PerformanceInsight.png)

Select the tab 'Limits' to enter the low limit for the KPI value and activate the notification option:

![4_4](graphics/4_4_PerformanceInsight.png)

Now a new KPI instance should be available:

![4_5](graphics/4_5_PerformanceInsight.png)

## Configure Notifier

In the chapter above we already created an alert notification for the KPI "production quality".
In order to create some warning and information notifications, we now use the Notifier app.

Open the user interface of the Notifier app on your IE Device. On the left bar navigate to Settings > Manage notification rules and click "Add notification rule".
Create a new warning notification "tank empty" with the following settings:

![5_1](graphics/5_1_Notifier.PNG)

Create a further information notification "production started" with the following settings:

![5_2](graphics/5_2_Notifier.PNG)
