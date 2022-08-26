# Drone-Simulation
## Abstract

<p align="justify">A simulation of a basic drone model take-off up to a given altitude in a gazebo environment; with a PX4 autopilot supported by Mavros in Ubuntu.</p>

<p align="center">
  <img src="https://github.com/abyasingh/Drone-Simulation/blob/main/Images%20and%20Videos/Images/Simultion.png" />
</p>

## Motivation

<p align="justify">As the technology is advancing every single day, we come across new tools which are aimed towards making our lives simpler and more comfortable. Drone is one such device enhances the quality of human life.<br><br>Creating a simulation provides the required insight into working of an actual drone. Having a simulation before construction of an actual model is an integral step as it provides a chance to eliminate any error which might disastrous for the model. Creating an outline is always a good beginning of a project of any sort.<br><br>During the covid times, people were instructed to refrain from going outside and to avoid public gatherings. It was when the usefulness of drones came into limelight. The cameras installed in drones provided a much-needed assistance in keeping a check over a locality without actually going over to that place. They were also utilized in transportation of small objects, ones within their capacity. Apart from the usual activities carried out by drones, they can be modified and enhanced to carry out complex tasks as well.</p>

## Software Aspects

### MavROS

<p align="justify">The Robot Operating System (ROS) is basically an open-source framework that helps in building and reusing codes between robotics applications. Basically, it acts as an interface for robots.<br><br>We needed an operating system which would help run our model. For that, we installed the noetic version of ROS. Mavros is a ROS package that enables MAVLink extendable communication between computers running ROS for any MAVLink enabled structure like an autopilot.</p>

### PX4

<p align="justify">An autopilot was required to transmit our commands to the system. PX4 is a suitable source for that. It is an open source flight control software for drones and other unmanned vehicles. It provides the required set of tools for drone developers to share technologies and create proper solutions for drone applications. We used the most basic inbuilt iris model for our project.

``` 
roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
```
</p>

### Gazebo

<p align="justify">Next, we installed Gazebo9-3D dynamic simulator. It is a high-class simulator that allows simulation of real-life environment, providing efficient simulation of varieties of robots in complex indoor and outdoor environments. It allows us to include practical forces such as gravity and friction.

```
make px4_sitl gazebo
```
</p>

### Take-off script

<p align="justify">Finally, we needed a script for takeoff of our drone. A launch file was also needed. We create a python script in VS Code for this execution.

```
def setTakeoff(self):
        print('waiting for service')
        # rospy.wait_for_service('mavros/cmd/takeoff')
        takeoffService = rospy.ServiceProxy('mavros/cmd/takeoff', mavros_msgs.srv.CommandTOL)
        print('got')
        try:
            takeoffService = rospy.ServiceProxy('mavros/cmd/takeoff', mavros_msgs.srv.CommandTOL)
            takeoffService(altitude = 10)
        except rospy.ServiceException as e:
            print ("Service takeoff call failed: %s"%e)

```

Some of the commands being executed:

```
1. modes.setTakeoff()
2. rate.sleep()
3. modes.setOffboardMode()
```

</p>

## Applications

<p align="justify">There are numerous significant applications of drone in our everyday lives. Some of the prominent ones include Aerial photography & videography, mapping & surveying, delivering goods, in search and rescue operations after a natural disaster, in security and military purposes.</p>

## Limitations

<p align="justify">Since this is just a simulation, original device must be constructed with utmost precision. Drones as of yet haven’t been designed to transport large objects, the ones beyond their limitation. The other properties such as photographing and flying capacity depend on the mechanical aspects and hence are limited too.</p>

## Improvements

<p align="justify">In this project, we used auto mode of noetic version which is not compatible with take-off command. Exploration of the different modes in noetic version of ROS such as guided and machine modes would be a prime aim. </p>

## Team Members

1. [Abya Singh](https://github.com/abyasingh)
2. [Gorle Apurva](https://github.com/apurvaa_2507)

## Mentors

1. [Harshini S.](https://github.com/Harshini-festus)
2. [Nagesh Bansal](https://github.com/Nageshbansal) 

## References

1. [Installation of noetic version of Ubuntu](http://wiki.ros.org/noetic/Installation/Ubuntu)
2. [Installation of Mavros](https://github.com/immersive-command-system/drone-mavros)
3. [Installation of PX4](https://github.com/PX4/PX4-SITL_gazebo>)
4. [Installation of Gazebo](https://dev.px4.io/v1.10_noredirect/en/simulation/gazebo.html)
5. [Launch file and iris model](https://docs.google.com/document/d/1re3MQy0Hwsjt1Ko96EiTB5wvbq_4QYZSZKgVmZGWsmg/edit)