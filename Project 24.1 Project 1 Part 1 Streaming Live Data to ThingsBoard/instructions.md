In the first part of this project, you will set up your Mosquitto, ThingsBoard, and Firebase environments. You will begin by setting up your MQTT protocol to produce temperature and humidity data. Next, you will ensure that the data produced by the MQTT protocol is published correctly to ThingsBoard. Finally, you will create a new project and a Realtime database in Firebase and send the temperature and humidity data to it.

This project is worth a total of 100 points.

To complete this project, follow these steps:

In a Terminal window, create a new folder called Project_24_Docker. Download the docker-compose.yml file and place it inside the Project_24_Docker folder. Inside the Project_24_Docker folder, create a folder titled mosquitto. Inside the mosquitto folder, create three more subfolders titled as follows: config, data, and log. Download the mosquitto.config file and place it inside the config folder.

See the image below, which depicts the required folders and files:

Map of the required folders, subfolders, and files in the Project_24_Docker folder.

Provide a screenshot to show that you correctly created all of the required folders and that you placed the docker-compose.yml and mosquitto.config files in the Project_24_Docker and config folders, respectively.

In a Terminal window, navigate to the Project_24_Docker folder and run the command below to initialize your Mosquitto container:

docker-compose up

Provide a screenshot of your Docker GUI to show that you have successfully initialized the Mosquitto container.

In a local Terminal window, run the command below to install the Paho MQTT Python client library locally:

pip install paho-mqtt

Provide a screenshot to show that you have successfully installed the Paho MQTT Python client library.

In a Terminal window (in the broker-1 container? or c:\? or in the root of this project directory?), navigate to your home folder.

For Windows users:

Enter the command below to navigate to your home folder:

`cd ~`

For Mac users:

Enter the command below to navigate the your home folder:

cd

Inside of your home folder, create two folders named .mytb-data and .mytb-logs.

Provide a screenshot to show that you created the .mytb-data and .mytb-logs folders in your home folder.

Inside the same location where you created the Project_24_Docker folder, create a new folder titled Project_24_MQTT. Inside the Project_24_MQTT folder, create a new subfolder titled ThingsBoard. Download the docker-compose.yml file and place it inside the ThingsBoard folder. Also inside of the ThingsBoard folder, create two folders named .mytb-data and .mytb-logs.

See the image below, which depicts the required folders and files:

Map of the required folder, subfolder, and file in the Project_24_MQTT folder.

Provide a screenshot to show that you correctly created all of the required folders and that you placed the docker-compose.yml inside the ThingsBoard folder.

In a Terminal window, navigate to the ThingsBoard folder that you created in Step 4 and run the command below to initialize your ThingsBoard container:

docker-compose up

If the ThingsBoard container does not spin up correctly, then change the ports on line 8 to 1883:1883 and try to spin up the container again.

Provide a screenshot of your Docker GUI to show that you have successfully initialized the ThingsBoard container.

Inside the Project_24_MQTT folder, create a new subfolder titled paho-mqtt. Download the TBPublish.py file and place it inside the paho-mqtt folder. Open the TBPublish.py file in VS Code.

See the image below, which depicts the required folders and files:

Map of the required folders, subfolders, and files in the Project_24_MQTT folder.

Modify the sensor_data dictionary by adding another key, humidity, with a corresponding value equal to 0. Inside the while loop, add a statement to generate random integer values between 50 and 100. Assign these values to the humidity variable.

Provide a screenshot to show that you created the paho-mqtt folder and modified the code inside the TBPublish.py file to add the humidity key with the correct values assigned to the humidity variable.

Open a Terminal window in VS Code. Run the TBPublish.py file.

Provide a screenshot to show that your code is correctly producing temperature and humidity data.

In a browser window, navigate to http://localhost:8080/. Log in to ThingsBoard using the credentials below:

Login: tenant@thingsboard.org
Password: tenant

Provide a screenshot to show that you successfully logged in to ThingsBoard by using the credentials provided.

In ThingsBoard, from the menu on the left, select “Devices”. You should see an existing device called DHT11 Demo Device. This device publishes data produced by an MQTT protocol to ThingsBoard. In other words, this device is able to read the data produced by the TBPublish.py file and send it to ThingsBoard.

Open the DHT11 Demo Device by selecting it. Navigate to the Latest Telemetry tab to see the latest telemetry.

Provide a screenshot of the data in the latest telemetry tab to show that the DHT11 Demo Device is publishing the data produced by the TBPublish.py file to ThingsBoard.

Navigate to the main page of Firebase. Follow the steps in Video 24.3 to add a new project called module24Project.

Provide a screenshot to show that you created the module24Project project in Firebase.

Follow the steps in Video 24.3 to create a Realtime database in Firebase. Add a field in your database titled temperature and initialize the corresponding field to zero.

Provide a screenshot to show that you created the temperature field inside your Realtime database.

Navigate to the Root Rule Chain in ThingsBoard. Add a “rest API call” node and name it Firebase. In the “Endpoint URL pattern” field, paste the link to your Realtime database from Firebase followed by "/temperature.json". Connect the “Firebase” node to the “Message Type Switch” node. Add “Post telemetry” as the link label.

Provide a screenshot to show that you have created the Firebase node correctly, connected it to the “Message Type Switch” node, and added “Post telemetry” as the link label.

Navigate to Firebase and display your temperature and humidity data by expanding the entries in your Realtime database.

Provide a screenshot to show that your Realtime database is updating correctly and displaying your temperature and humidity data.

Now that you have set up your MQTT protocol, verified that it's publishing data to ThingsBoard, and created a new project in Firebase, you are ready to learn about how to set up alarms in ThingsBoard to monitor your data in Part 2 of this project.