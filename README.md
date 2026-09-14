# PR01  
  
Резултат работы первой практической работы  
  
## Среда

Ubuntu 24.04.4, ROS 2 Lyrical, Gazebo 8.15.0. Все терминалы запущены в одной среде

```bash
source /opt/ros/jazzy/setup.bash
```  

## Исправный граф  

Всем терминалам щадаём домен 16  

```bash
export ROS_DOMAIN_ID=16
```  

В A запускаем симулятор:

```bash
ros2 run turtlesim turtlesim_node
```

В B запускаем управление:

```bash
ros2 run turtlesim turtle_teleop_key
```
Теперь черепаха управляется стрелками  

В C получаем сведения:

```bash
mkdir -p evidence/pr01
ros2 doctor --report > evidence/pr01/doctor.txt 2>&1  
ros2 node list --no-daemon --spin-time 2
ros2 topic list -t
ros2 node info /turtlesim
ros2 topic type /turtle1/pose
POSE_TYPE=$(ros2 topic type /turtle1/pose)
ros2 topic echo /turtle1/pose --once
ros2 topic hz /turtle1/pose
```  
Вся информация по командам хранится в graph.md  
  
## Разрыв связи

A продолжает работать в домене 16. В B останавливаем teleop через `Ctrl+C`
и запускаем заново с доменом 17:

```bash
export ROS_DOMAIN_ID=17
ros2 run turtlesim turtle_teleop_key
```

Перезапускаем C с доменом 17 и выполняем проверку. Переменная `POSE_TYPE` осталась после
исправного запуска и содержит `turtlesim_msgs/msg/Pose`:

```bash
export ROS_DOMAIN_ID=17
ros2 node list --no-daemon --spin-time 2
timeout 5s ros2 topic echo /turtle1/pose "$POSE_TYPE" --once \
  > evidence/pr01/pose-broken.txt 2>&1
printf 'exit=%s\n' "$?"
```
Теперь C не может отследить POSE нашего A, файл pose-broken.txt пустой, exit = 124, а черепаха не управляется стрелками из B:

## Восстановление

В B останавливаем teleop через `Ctrl+C` и возвращаем его в домен 16:

```bash
export ROS_DOMAIN_ID=16
ros2 run turtlesim turtle_teleop_key
```

Возвращаем терминал C в домен 16 и повторяем тот же тест доставки:

```bash
export ROS_DOMAIN_ID=16
ros2 node list --no-daemon --spin-time 2
timeout 5s ros2 topic echo /turtle1/pose "$POSE_TYPE" --once \
  > evidence/pr01/pose-fixed.txt 2>&1
printf 'exit=%s\n' "$?"
```
  
POSE снова приходит, exit=0, а черепаха управляется стрелками через teleop  
  
Значения, сравнение трёх состояний и причина сбоя находятся в
[graph.md](evidence/pr01/graph.md).

После повторения опыта контейнер можно удалить с хоста:

```bash
docker rm -f pr01-student-demo
```
