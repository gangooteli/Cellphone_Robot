# Cellphone_robot

Welcome to the Cellphone_Robot project! Through this project we are aiming to expand on Android based robotics. myRobot, the app within this repository, was created to control a small ROS controlled car-robot. The project showcases how an Android phone can significantly enhance a ROS-based robot through leveraging the many APIs out there. This project utlizes multiple libraries as well as APIs. In this user guide we will walk you through setting up the project for yourself and setting up the necessary access keys to use the app in tandem with a ROS project. That being said, all the libraries and APIs can be replaced or expanded upon so do not feel limited to our implementation of the repo. 

This repo allow the robot to: access a Natural Language Processor, translate text, send Slack messages, and communicate back and forth with a ROS network that operates on an autonomous navigation robot. In our hardware setup, we had the ROS network running on a Raspberry Pi 3 mounted on the RC robot itself. We used a portable rechargable battery to make this happen. The phone is also mounted on the robot using a cellphone holder. Have fun experimenting!

## Demo Video
[![Demo Video](https://github.com/AGKhalil/Cellphone_Robot/blob/master/wiki_images/VideoSS.png)](https://youtu.be/IUkcgtFX2zM)

## What does the app do?
The app is fundamentally acting as an extension to the robot, regardless of what the robot is or what it is capable of. The app acts as a higher level method of controlling the robot, while leveraging its access to the web and the many tools out there for Android phones. The user can then communicate with the phone through texting or Instant Messaging over NLP to command the robot. This project is essentially a template for people to get creative with. If you have a ROS based robot and an Android phone, you can do all sorts of cool stuff. This repo is more tailored for our SLAM and Autonomous navigation [project](https://github.com/wang3303/delivery_bot), but for a more general version, please check our previous [work](https://github.com/AGKhalil/Cellphone_Robot_OpenCV).

## Who is this project for?
This project is a follow up on our previous work [Cellphone_Robot_OpenCV](https://github.com/AGKhalil/Cellphone_Robot_OpenCV) and is tilored for our SLAM and Autonomous navigation [project](https://github.com/wang3303/delivery_bot). You do not to be an Android/ROS expert to use this project. That being said, you should be familiar with both environemnts to use this project to its full potential. Furthermore, the Setup guide assumes you have some familiarity with navigating Ubuntu systems.

# ROS Setup
This user guide focuses mainly on setting up the Android app; however, to communicate with the ROS network a few steps need to be taken. This [repo](https://github.com/wang3303/ros_cellphonerobot) contains the ROS project we created to test the app with. To use the app you do not need to clone the whole project. There is only one script that your ROS project needs to have. [That](https://github.com/wang3303/ros_cellphonerobot) user guide will show you how to set up the script for your own uses, or you can just clone the whole project.

## Connection
To connect the Android to ROS, you need to make sure the `ROS_MASTER_URI` is correctly referenced and that depends on whether the connection is over WIFI or USB.

### WIFI
Ensure the ROS host machine, in our case the Rhaspberry PI, and the Android phone are connected to the same WIFI network. 

On the ROS host, copy the Pi's `wlan0` IP address. Then in terminal, go to your root directory, open `.bashrc`, and type the following at the bottom of the script.

```
export ROS_IP=DEVICE_IP_ADDRESS
export ROS_MASTER_URI=http://DEVICE_IP_ADDRESS:11311/
```

On the Android side, go to `strings.xml` located under [`/app/src/main/res/values`](app/src/main/res/values) and type in the `ROS_MASTER_URI` in the corresponding location.

```xml
 <string name="rosIP">http://DEVICE_IP_ADDRESS:11311/</string>
```

To update your ROS enviroments, run the following in a terminal:

```
source ~/.bashrc
```

Now you can launch `roscore` on the ROS host and the app will connect to it over WIFI. 

### USB
Connect the phone to the ROS host. Turn off WIFI connection on the ROS host device. On the Android, go to **Settings > More > Tethering & portable hotspost** and turn on **USB tethering**.

On the ROS host, copy the Pi's `ethernet` IP address. Then in terminal, go to your root directory, open `.bashrc`, and type the following at the bottom of the script.

```
export ROS_IP=DEVICE_IP_ADDRESS
export ROS_MASTER_URI=http://DEVICE_IP_ADDRESS:11311/
```

On the Android side, go to `strings.xml` located under [`/app/src/main/res/values`](app/src/main/res/values) and type in the `ROS_MASTER_URI` in the corresponding location.

```xml
 <string name="rosIP">http://DEVICE_IP_ADDRESS:11311/</string>

```

To update your ROS enviroments, run the following in a terminal:

```
source ~/.bashrc
```

Now you can launch `roscore` on the ROS host and the app will connect to it over USB.

## ROS Package
The ROS package can be found [here](https://github.com/wang3303/ros_cellphonerobot/wiki).

# Android Setup
## Libraries
### Dialogflow
For setting up Dialogflow and trying sample app, please click [here](https://github.com/dialogflow/dialogflow-android-client/blob/master/README.md).

For detailed explanation of natual language process service, you can go [here](https://github.com/AGKhalil/Cellphone_Robot/wiki/NLP).

## APIs
The app includes many APIs, all of which need access keys. Below are the respective links for obtaining them. All you need to do to have the APIs work is paste the keys in the corresponding `string.xml` allocation.

### Slack
[This link](https://api.slack.com/bot-users) will introduce how to register a bot and interact with it. Also, there are various [Libraries, Plugins, and Sample Apps](https://api.slack.com/community) that you can use. In this project, we implement [slack-api-android ](https://github.com/pschroen/slack-api-android).
Make sure you add the following line to your `build.gradle`. 
```gradle
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```

and:

```gradle
dependencies {
    compile 'com.github.pschroen:slack-api-android:c66cc8d997'
}
```
Check [here](https://github.com/AGKhalil/Cellphone_Robot/wiki/slack) for usage.
