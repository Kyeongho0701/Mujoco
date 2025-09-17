# MUJOCO 공부
**Mujoco Study**


**Mujoco설치** 

### 가상환경 만들기

```bash
conda create -n mujoco python=3.11 # 파이썬은 3.9이상 가능함.

conda activate mujoco #가상환경 활성화 

pip install mujoco # 가상환경 내부에서 설치가 쉬운게 상당히 마음에 든다.
```

### Mujoco 시뮬레이터 설치

```bash
conda create -n mujoco python=3.11
```


### Mujoco viewer
```bash
python -m mujoco.viewer
#-m 은 모듈. mujoco.viewer 라는 모듈을 실행해라.
```

### 로봇을 불러오기 위해 Mujoco Menagerie 라이브러리 clone
```bash
github deepmind mujoco menagerie
#로봇들이 모여있는 라이브러리

git clone https://https://github.com/google-deepmind/mujoco_menagerie.git

# 확인 하기 위해 유니트리 로봇 개를 불러보자.
python -m mujoco.viewer --mjcf mujoco_menagerie/unitree_go2/scene.xml

```
### 결과 사진

### unitree_go2
<img width="1261" height="710" alt="go2" src="https://github.com/user-attachments/assets/41c8f111-e356-459b-9d75-77369fbdb68e" />


### unitree_g1
<img width="1304" height="734" alt="g1" src="https://github.com/user-attachments/assets/60a131a9-e8ac-4a3e-8750-d9bfac5983b5" />



### RL 을 위한 환경 설정 및 Cartpole 예제를 위한 파이썬 파일 생성.

```bash
#mujoco 디렉토리 내부에 control_cartpole.py 파일 생성
touch control_cartpole.py
#편집기 사용 파일 편집
nano -l control_cartpole.py
```


```bash
#필요한 라이브러리 설치
import numpy as np
from dm_control import suite
import mujoco.viewer
import time
```

```bash
#cartpole 환경 불러오기
env = suite.load(domain_name="cartpole", task_name="swingup")
action_spec = env.action_spec()

```
```bash
# 2. 무작위 정책(Random Policy) 정의
def random_policy(time_step):
    del time_step
    return np.random.uniform(low=action_spec.minimum,
                             high=action_spec.maximum,
                             size=action_spec.shape)
#들여쓰기에 문제가 있을 가능성 존재 주의하세요!
```
```bash
# 3. 환경 초기화
time_step = env.reset()

# 4. MuJoCo 뷰어 실행
# dm_control 환경의 물리 엔진 정보(model, data)를 뷰어에 넘기기.
with mujoco.viewer.launch_passive(env.physics.model.ptr, env.physics.data.ptr) as viewer:
     
    # 뷰어가 켜져 있는 동안 계속 시뮬레이션 실행
    while viewer.is_running():
        step_start = time.time()

        # 무작위 정책에 따라 행동 선택
        action = random_policy(time_step)
        
        # 환경에 행동을 적용
        time_step = env.step(action)
        
        # 매 스텝마다 뷰어 화면을 현재 상태로 동기화 (업데이트)
        viewer.sync()

        # 에피소드가 끝나면 (막대가 쓰러지면) 환경을 리셋
        if time_step.last():
            time_step = env.reset()

        # 시뮬레이션 속도를 실제 시간과 비슷하게 맞추기 위한 대기 시간
        time_until_next_step = env.physics.model.opt.timestep - (time.time() - step_start)
        if time_until_next_step > 0:
            time.sleep(time_until_next_step)
```

### 실행해보기 (Cartpole)

```bash
#만들어 둔 파이썬 파일 실행
python control_cartpole.py
```

### 결과 
<img width="1246" height="703" alt="무조코카트폴연습예제" src="https://github.com/user-attachments/assets/46bb225e-1f8c-4b99-940f-acd67d146032" />
아직 원하는 수준의 task 수행X

### 오픈소스 모델 Clone 및 수행 작업. 
