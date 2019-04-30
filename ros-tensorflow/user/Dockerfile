FROM decinho13/base-notebook:ros-tf

USER root

#Add ROS
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN apt-get update && apt-get install -y ros-kinetic-desktop-full \
 	&& rm -rf /var/lib/apt/lists/*
RUN sudo apt-get update && sudo apt-get install -y ros-kinetic-ros-control ros-kinetic-ros-controllers
RUN sudo apt-get install -y ros-kinetic-gazebo-ros-pkgs ros-kinetic-gazebo-ros-control


# Configure ROS
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc

#Add Python 2.7 with kernel for jupyter notebook
RUN sudo apt-get update && sudo apt-get install -y python2.7 python3-pip python-pip
RUN python2 -m pip install ipykernel && python2 -m ipykernel install --user

#Add tools for jupyros
RUN pip2 install bqplot pyyaml empy
RUN pip2 install jupyros

RUN pip install bqplot pyyaml empy
RUN pip install jupyros && jupyter nbextension enable --py --sys-prefix jupyros && jupyter labextension install jupyter-ros

#Install openai_ros
RUN pip2 install catkin_tools
RUN pip install catkin_tools
RUN mkdir ros_ws && cd ros_ws && mkdir src && cd src && \
    git clone https://bitbucket.org/theconstructcore/openai_ros.git
RUN /bin/bash -c '. /opt/ros/kinetic/setup.bash; cd  ~/ros_ws; catkin_make; source devel/setup.bash; rosdep install openai_ros'

#Add user permissions to jovyan for using ROS as non-root
RUN chown -R 1000:0 /opt/ros  && chmod -R g=u  /opt/ros 
RUN chown -R 1000:0  /etc  && chmod -R g=u /etc 
RUN chown -R 1000:0  /home  && chmod -R g=u /home 

