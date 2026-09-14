# Практическая01 ROS 2: turtlesim + teleop_turtle  
  
## 1. Выполнение команд и их вывод  
  
### 1.1 Список узлов  
```bash
ros2 node list --no-daemon --spin-time 2  
```  
```text
/teleop_turtle  
/turtlesim  
```  
### 1.2 Список топиокв с типами  
```bash
ros2 topic list -t  
```  
```text
/parameter_events [rcl_interfaces/msg/ParameterEvent]
/rosout [rcl_interfaces/msg/Log]
/turtle1/cmd_vel [geometry_msgs/msg/Twist]
/turtle1/color_sensor [turtlesim/msg/Color]
/turtle1/pose [turtlesim/msg/Pose]  
```  
### 1.3 Информация об узле /turtlesim  
```bash
ros2 node info /turtlesim  
```  
```text
/turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/get_type_description: type_description_interfaces/srv/GetTypeDescription
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:
```  
### 1.4 Тип сообщения позы  
```bash
ros2 topic type /turtle1/pose  
```  
```text
turtlesim/msg/Pose  
```  
### 1.5 Однократное чтение позы  
```bash
ros2 topic echo /turtle1/pose --once  
```  
```text
x: 5.544444561004639
y: 5.544444561004639
theta: 0.0
linear_velocity: 0.0
angular_velocity: 0.0
---  
```  
### 1.6 Измерение частоты публикации позы (13 сек)  
```bash
ros2 topic hz /turtle1/pose  
```  
```text
average rate: 62.522
	min: 0.015s max: 0.017s std dev: 0.00030s window: 64
average rate: 62.504
	min: 0.015s max: 0.017s std dev: 0.00033s window: 127
average rate: 62.509
	min: 0.015s max: 0.017s std dev: 0.00036s window: 190
average rate: 62.500
	min: 0.015s max: 0.017s std dev: 0.00036s window: 253
average rate: 62.511
	min: 0.015s max: 0.017s std dev: 0.00037s window: 316
average rate: 62.501
	min: 0.015s max: 0.017s std dev: 0.00037s window: 379
average rate: 62.504
	min: 0.015s max: 0.017s std dev: 0.00037s window: 442
average rate: 62.504
	min: 0.015s max: 0.017s std dev: 0.00039s window: 505
average rate: 62.501
	min: 0.015s max: 0.017s std dev: 0.00038s window: 568
average rate: 62.499
	min: 0.015s max: 0.017s std dev: 0.00038s window: 631
average rate: 62.500
	min: 0.015s max: 0.017s std dev: 0.00038s window: 694
average rate: 62.501
	min: 0.015s max: 0.017s std dev: 0.00038s window: 757
average rate: 62.502
	min: 0.015s max: 0.017s std dev: 0.00039s window: 820  
```  
### 1.7 Информация об узле /teleop_turtle  
```bash
ros2 node info /teleop_turtle  
```  
```text
/teleop_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Service Servers:
    /teleop_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /teleop_turtle/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /teleop_turtle/get_parameters: rcl_interfaces/srv/GetParameters
    /teleop_turtle/get_type_description: type_description_interfaces/srv/GetTypeDescription
    /teleop_turtle/list_parameters: rcl_interfaces/srv/ListParameters
    /teleop_turtle/set_parameters: rcl_interfaces/srv/SetParameters
    /teleop_turtle/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:

  Action Clients:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute  
```  
## 2. Узлы и их роли

| Узел | Роль |
|------|------|
| `/turtlesim` | Симулятор черепахи. Подписан на `/turtle1/cmd_vel`, публикует `/turtle1/pose` и `/turtle1/color_sensor`. |
| `/teleop_turtle` | Узел ручного управления. Публикует команды в `/turtle1/cmd_vel`. |  
## 3. Полные имена топиков и их типы

| Топик | Тип |
|-------|-----|
| `/parameter_events` | `rcl_interfaces/msg/ParameterEvent` |
| `/rosout` | `rcl_interfaces/msg/Log` |
| `/turtle1/cmd_vel` | `geometry_msgs/msg/Twist` |
| `/turtle1/color_sensor` | `turtlesim/msg/Color` |
| `/turtle1/pose` | `turtlesim/msg/Pose` |  
## 4. Измеренная частота

- Топик: **`/turtle1/pose`**
- Средняя частота публикации: **≈ 62.5 Гц**
- Период: **min ≈ 0.015 с, max ≈ 0.017 с**
- Стандартное отклонение периода: **≈ 0.0004 с**  
## 5. Разрыв и восстановление связи через ROS_DOMAIN_ID

### Участники и их домены

| Терминал | Узел | Домен (сбой) | Домен (восстановление) |
|----------|------|--------------|------------------------|
| A | `/turtlesim` | 16 | 16 |
| B | `/teleop_turtle` | 17 | 16 |
| C | CLI (`ros2 node list`, `ros2 topic echo`) | 17 | 16 |

### Сбой  
Терминал B: 
Ctrl + C   
```bach
export ROS_DOMAIN_ID=17
ros2 run turtlesim turtle_teleop_key  
```  
Терминал C:  
```bash
export ROS_DOMAIN_ID=17
ros2 node list --no-daemon --spin-time 2
timeout 5s ros2 topic echo /turtle1/pose "$POSE_TYPE" --once > evidence/pr01/pose-broken.txt 2>&1
printf 'exit=%s\n' "$?"  
```  
Вывод:  
```text
/teleop_turtle  
```  
Поза не приходит, exit=124  
### Восстановление  
Терминал B:  
Ctrl + C  
```bach
export ROS_DOMAIN_ID=16
ros2 run turtlesim turtle_teleop_key  
```  
Терминал C:  
```bash
export ROS_DOMAIN_ID=16
ros2 node list --no-daemon --spin-time 2
timeout 5s ros2 topic echo /turtle1/pose "$POSE_TYPE" --once > evidence/pr01/pose-broken.txt 2>&1
printf 'exit=%s\n' "$?"  
```  
Вывод:  
```text
/teleop_turtle
/turtlesim  
```  
Поза приходит, exit=0  
### Сравнение «до / сбой / после»

| Состояние | Домены (A / B / C) | Видно `/turtlesim`? | Поза приходит? | `exit` |
|-----------|:------------------:|:-------------------:|:--------------:|:------:|
| До сбоя | 16 / 16 / 16 | да | да | 0 |
| Сбой | 16 / 17 / 17 | нет | нет | 124 |
| После | 16 / 16 / 16 | да | да | 0 |  
### Почему перезапустили только teleop

`ROS_DOMAIN_ID` считывается один раз при старте процесса и определяет, в каком DDS-домене регистрируется узел. Изменить домен у уже запущенного узла нельзя — переменную окружения нужно задать до запуска. Поэтому:

1. **`teleop_turtle`** пришлось перезапустить дважды: сначала в домен 17, потом обратно в 16.
2. **`turtlesim`** и установку ROS трогать не потребовалось — симулятор всё время оставался в домене 16 и не менял своего поведения.  


