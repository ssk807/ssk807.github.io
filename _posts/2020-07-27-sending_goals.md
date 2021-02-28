---
title: "Sending goals in ROS-Navigation"
excerpt: "ROS-Navigation에서 좌표값 넘겨주는 토픽 구현?"

categories:
  - ROS
tags:
  - ROS
last_modified_at: 2020-07-27
---  

## ROS에서 Navigation과 Gazebo간 토픽 흐름
![](assets/images/rqt_graph.png)
- 위 그래프를 보면 주어진 맵에서 어떻게 로봇이 목표(Goal)까지 찾아가는지 흐름을 확인할 수 있다.  

## 목표를 설정해주는 토픽
![](assets/images/rqt.png)  
- 실제로 navigation tool에서 2D Nav Goal을 통해 목표를 설정해주면 그림과 같이 /move_base_simple/goal 의 데이터들이 설정해준 좌표와 방향과 일치하게 바뀌는 것을 확인할 수 있다.  
따라서 우리는 /move_base_simple/goal에게 데이터를 보낼 토픽을 작성해야한다.  

## /move_base_simple/goal 토픽이 받는 데이터 타입
- /move_base_simple/goal에게 보내는 데이터의 타입을 먼저 알아보자.  

![](assets/images/goal_info.png)
- rostopic info ~ 명령어를 통해 알아본 결과, geometry_msgs/PoseStamped라는 데이터 타입을 보내는 것을 확인할 수 있다.  

## 명령어를 통해 topic publish
![](assets/images/pub.png)
- rostopic pub /move_base_simple/goal geometry_msgs/PoseStamped 까지 명령어를 친 뒤 Tab을 누르면 Type의 형식에 맞게 나온다.  
형식에 맞춰 목표로 설정하고자 하는 좌표값과 방향을 입력해주면 된다. 여기서 좌표값은 pose->position이고 방향은 pose->orientation이다.  
또한 가장 중요한 것이 있는데 __frame_id: 'map'__ 으로 기입해준다.  
> rostopic pub 까지 친 뒤 Tab을 누르면 보낼 수 있는 토픽에 대한 정보들이 나타나게 된다. 토픽을 설정하고 나서 또 한번 Tab을 누르면 해당 토픽에게 보낼 수 있는 데이터 타입들의 목록이 나타난다.  
