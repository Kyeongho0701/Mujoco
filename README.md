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
