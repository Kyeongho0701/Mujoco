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
