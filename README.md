```markdown
# ROS2 TurtleBot3 Project

<img src="https://img.shields.io/badge/ROS–2-22314E?style=for-the-badge&logo=ros&logoColor=white"/> <img src="https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white"/>

이 프로젝트는 **ROS 2** 기반으로 **TurtleBot3** 로봇을 제어·확장하기 위한 패키지 모음입니다.  
기본 이동부터 센서 활용, 액션 통신, GPS 연동까지 다양한 ROS 2 개념을 실습할 수 있도록 구성했습니다.

---

## 📂 디렉토리 구조

```

.
├── Cgps/                  # GPS 센서 출력 테스트 패키지
├── action\_test/           # Action 통신 예제 패키지
├── robot\_move\_pkg/        # 키보드 입력으로 이동 제어
├── robot\_cleaner\_pkg/     # 장애물 감지 기반 자율 주행
├── robot\_go\_pkg/          # 주어진 거리만큼 이동 + 장애물 회피
├── robot\_action/          # 사용자 정의 Action 메시지 정의
├── robot\_drive\_pkg/       # Teleop 드라이브 제어 예제
├── robot\_grid\_pkg/        # 그리드 맵 기반 경로 탐색
├── robot\_total\_pkg/       # 전체 통합 시나리오
├── robot\_totalgrid\_pkg/   # 그리드 + 통합 예제
├── robot\_totalgrid\_pkg\_v2/# 개선된 그리드 통합 예제
├── test\_pkg/              # 패키지 생성 테스트용
├── build/                 # 빌드 아티팩트
├── install/               # 설치된 파일
└── log/                   # 실행 로그

````

---

## 🚀 주요 기능 & 패키지

1. **robot_move_pkg**  
   - 키보드 Teleop을 통해 직접 TurtleBot3 이동  
   - `geometry_msgs/Twist` 토픽 발행

2. **robot_cleaner_pkg**  
   - 앞쪽 장애물 감지 시 후진·회전  
   - `sensor_msgs/LaserScan` 구독

3. **action_test**  
   - ROS 2 Action 서버·클라이언트 기본 구조 실습  
   - 간단한 피드백·결과 메시지 교환

4. **robot_action**  
   - 커스텀 Action 메시지(`.action` 파일) 정의  
   - 목표 위치·속도 등을 파라미터로 전달

5. **robot_go_pkg**  
   - 목표 거리만큼 전진 후 장애물 회피  
   - Action 통신으로 목표 거리 전달

6. **Cgps**  
   - EZ-0048 GPS 센서 드라이버 연동  
   - 위도·경도 정보를 터미널에 출력

7. **test_pkg**  
   - 새로운 패키지 구조 테스트용  
   - 템플릿 코드 포함

8. **통합 예제**  
   - **robot_total_pkg**, **robot_totalgrid_pkg** 등에서 여러 패키지 기능을 한 번에 시연

---

## ⚙️ 설치 & 실행

### 의존성

- Ubuntu 20.04 / ROS 2 Foxy 또는 Humble  
- TurtleBot3 (Burger)  
- C++ 컴파일러, Python3, `colcon` 빌드툴  

### 빌드 및 실행

1. 워크스페이스 생성 & 소스 위치로 이동  
   ```bash
   mkdir -p ~/robot_ws/src
   cd ~/robot_ws/src
````

2. 패키지 복사 또는 클론

   ```bash
   git clone https://github.com/aeeun-git/ROS2_TurtleBot3_Project.git
   ```

3. 빌드

   ```bash
   cd ~/robot_ws
   colcon build --symlink-install
   source install/local_setup.bash
   ```

4. 로봇 브링업

   ```bash
   export TURTLEBOT3_MODEL=burger
   ros2 launch turtlebot3_bringup robot.launch.py
   ```

5. 패키지 실행 예시

   * **키보드 Teleop**

     ```bash
     ros2 run robot_move_pkg teleop_keyboard_node
     ```
   * **장애물 회피**

     ```bash
     ros2 run robot_cleaner_pkg cleaner_node
     ```
   * **GPS 출력**

     ```bash
     ros2 run Cgps gps_listener_node
     ```

---

## 🎯 사용 예시

```bash
# Teleop 윈도우 띄우고 키보드로 로봇 제어
ros2 run robot_move_pkg teleop_keyboard_node

# 장애물 감지 후 자동 주행
ros2 run robot_cleaner_pkg cleaner_node

# 목표 거리만큼 이동 (Action)
ros2 run robot_go_pkg go_client_node --ros-args -p distance:=1.5

# GPS 센서 데이터 확인
ros2 run Cgps gps_listener_node
```

---

## 🔧 커스터마이징

* `robot_action/action/*.action` 파일을 편집해 새로운 Action 메시지 정의
* `robot_grid_pkg` 내 그리드 맵 파라미터 조정 가능
* GPS 센서 드라이버(`Cgps`)를 다른 센서로 교체하려면 노드 코드 수정

---

## 📚 참고 문헌

* TurtleBot3 공식 튜토리얼: [http://emanual.robotis.com/docs/en/platform/turtlebot3/](http://emanual.robotis.com/docs/en/platform/turtlebot3/)
* ROS 2 튜토리얼: [https://docs.ros.org/en/foxy/Tutorials.html](https://docs.ros.org/en/foxy/Tutorials.html)

---

## 🏷️ 라이선스

MIT © \[aeeun-git]

---
