In the second part of this project, you will set up an alarm rule chain to send information about data that is above a certain threshold to Firebase. The data you will be using is live streaming from the MQTT protocol that you set up in Project 24.1: Project 1 Part 1. You will begin by setting up the alarm rule chain. Next, you will connect the alarm rule chain to your Realtime database in Firebase. Finally, you will connect the Root Rule Chain to the alarm rule chain and verify that the data is being correctly sent to Firebase.

This project will build on what you did in Project 24.1. Therefore, complete all of the steps of Project 24.1 before attempting Project 24.2.

To complete this project, follow these steps:

Navigate to Firebase. In the module24Project Realtime database, create a new field titled alarms and initialize the corresponding field to zero.

Provide a screenshot to show that you created the alarm field inside your Realtime database and initialized it to zero.

Navigate to the ThingsBoard home page. Create a new rule chain titled “CreateAndClearAlarms” by following the steps shown in Mini-Lesson 24.5.

## Mini-Lesson 24.5: Setting Up Alarms in ThingsBoard
What Are Alarms in ThingsBoard?

Imagine that you have an IoT device, such as a thermostat, that sends temperature data to ThingsBoard. Ideally, you would like to monitor your data so that if the temperature gets too high or too low, you will receive a notification. To achieve this, ThingsBoard provides the option to set alarms to monitor data and notify users or clients when the data reaches a certain threshold.

How Are Alarms Created in ThingsBoard?

The easiest way to create an alarm in ThingsBoard is by creating a custom rule chain that is able to trigger or clear your alarms based on your data readings.

In this mini-lesson, you will learn how to create a custom rule chain to set up alarms in ThingsBoard. Then, you will learn how to connect alarms to your Root Rule Chain in Videos 24.10 and 24.11.

To set up an alarm rule chain, navigate to Rule chains on the left-hand side menu of the ThingsBoard home page. Add a new rule by selecting the plus sign (+) icon in the top-right corner and then selecting “Create new rule chain”.

Creating a new rule chain in ThingsBoard.

Name this rule chain “Alarms”, then select “Add” to create the rule chain.

Adding the Alarms rule chain.

Open the Alarms rule chain. Add a “script” node and name it MaxTemp. You will notice that this node allows you to modify or add JavaScript code to trigger the alarm when your data reaches a certain value. The default value triggers the alarm when the temperature is greater than 20 degrees, but you can modify this value as needed. Select “Add” to add the TempThreshold node to your Rule Engine (I guess this means Rule Chain).

Adding the TempThreshold node to the Rule Engine.

Your rule chain will come with an Input node automatically set up. Connect the Input and the TempThreshold nodes. This will allow the Alarms rule chain to receive input data from your devices.

Connecting the Input and TempThreshold nodes.

Add a “clear alarm” node and name it ClearAlarm. Modify the default JavaScript code as follows:

var details = {};

if (metadata.prevAlarmDetails) {

    details = JSON.parse(metadata.prevAlarmDetails);}

return details;

Select “Add” to add the ClearAlarm node to your Rule Engine.

Adding the ClearAlarm node to the Rule Engine.

Connect the MaxTemp and “ClearAlarm” nodes, and add “True” as the link label.

Connecting the MaxTemp and “ClearAlarm” nodes and adding “True” as the link label.

Add a “create alarm” node and name it CreateAlarm. Modify the default JavaScript code as follows (Have to select Javascript, not TBEL!): 

var details = {};

if (metadata.prevAlarmDetails) {

    details = JSON.parse(metadata.prevAlarmDetails);}

return details;

Select “Add” to add the CreateAlarm node to your Rule Engine.

Adding the CreateAlarm node to the Rule Engine.

Connect the MaxTemp and “CreateAlarm” nodes, and add “False” as the link label.

Connecting the MaxTemp and “CreateAlarm” nodes and adding “False” as the link label.

Now that you know how to set up a basic rule chain to create alarms in ThingsBoard, you are ready to learn how to connect the alarm rule chain to your Root Rule Chain. Then, you can use it to monitor data and send data and alarm readings to Firebase.

## Mini-Lesson 24.5 Done

Provide a screenshot to show that you created the CreateAndClearAlarms rule chain with all of the necessary components.

Create another rule chain and name it “TempToFirebase”.

Provide a screenshot to show that you created the TempToFirebase rule chain with all of the necessary components. (It's just an input node though?)

Open the TempToFirebase rule chain. Add a “rest API call” node and name it “TempToFirebase”. Replace the default link with the following link:

https://module24project-<change this to your number>-default-rtdb.firebaseio.com/temperature.json

Select “Add” to add the TempToFirebase node to your Rule Engine. Connect the Input and TempToFirebase nodes.

Provide two screenshots. The first screenshot should show that you added the TempToFirebase node to your Rule Engine correctly. The second screenshot should show that you connected the Input and TempToFirebase nodes.

Create another rule chain and name it “AlarmToFirebase”.

Provide a screenshot to show that you created the AlarmToFirebase rule chain with all of the necessary components. (It's just an input node?)

Open the AlarmToFirebase rule chain. Add a “rest API call” node and name it “AlarmToFirebase”. Replace the default link with the following link:

https://module24project-<change this to your number>-default-rtdb.firebaseio.com/alarm.json

Select “Add” to add the AlarmToFirebase node to your Rule Chain. Connect the Input and AlarmToFirebase nodes.

Provide two screenshots. The first screenshot should show that you added the AlarmToFirebase node to your Rule Engine correctly. The second screenshot should show that you connected the Input and AlarmToFirebase nodes.

Open the CreateAndClearAlarms rule chain that you created in Step 2. Add a “rule chain” node. Title this node “AlarmToFirebase” and select AlarmToFirebase as the rule chain. Select “Add” to add the AlarmToFirebase node to your Rule Engine.

Provide a screenshot to show that you added the AlarmToFirebase node to your Rule Engine correctly.

Connect the CreateAlarm and AlarmToFirebase nodes. Add “Created” as the link label.

Provide a screenshot to show that you connected the CreateAlarm and AlarmToFirebase nodes with a Created link label.

Add another “rule chain” node to the CreateAndClearAlarms rule chain. Title this node “TempToFirebase” and select TempToFirebase as the rule chain. Select “Add” to add the TempToFirebase node to your Rule Engine.

Provide a screenshot to show that you added the TempToFirebase node to your Rule Engine correctly.

Connect the MaxTemp and TempToFirebase nodes. Add “True” as the link label.

Provide a screenshot to show that you connected the MaxTemp and AlarmToFirebase nodes with a True link label.

Open the Root Rule Chain in ThingsBoard. Add a “rule chain” node. Name it “CreateAndClearAlarm” and select CreateAndClearAlarm as the rule chain. Select “Add” to add the CreateAndClearAlarm node to your Rule Engine.

Provide a screenshot to show that you added the CreateAndClearAlarm node to your Rule Engine correctly.

Connect the SaveTimeseries and CreateAndClearAlarm nodes. Add “Success” as the link label.

Provide a screenshot to show that you connected the SaveTimeseries and CreateAndClearAlarm nodes with a Success link label. (The instructions seem wrong since there's already a rest api chain that sends temperature data to firebase, so it's redundant)

Navigate to Firebase and open the alarm and temperature fields.

Provide two screenshots. The first screenshot should show that the alarm field is being populated with the live streaming data from the CreateAndClearAlarm rule chain. The second screenshot should show that the temperature field is being populated with temperature and humidity data.