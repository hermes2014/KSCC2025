# KSCC2025

## 대한임상화학회 2025년 추계학술대회 Workshop2
## 실행 스크립트 모음

### Google Colab의 Jupyter Note에서 실행

#### 터미널 프로그램 설치
```python
!pip install colab-xterm
%load_ext colabxterm
```

#### 터미널 프로그램을 실행시키는 매직 명령어
```python
%xterm
```

### 이하 명령어들은 터미널 창에서 실행

#### ollma 설치 및 실행
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama
ollama -help
ollama ps
ollama serve
```
(ollama serve 실행 후 해당 터미널은 그대로 유지)

#### ollama에서 구동시킬 gemma 모델 다운로드 및 실행
```bash
ollama ps	
ollama pull gemma3:12b
ollama run gemma3:12b
```

#### LLM을 사용하기 위한 GUI인 Open-WebUI 설치 및 실행
```bash
python -m pip install --upgrade pip
pip install open-webui
open-webui serve --port 8081
```

#### 외부에서 Open-WebUI 서비스에 접속하기 위한 연결 생성
ssh -R [remote-port]:[local-host]:[local-port] [user]@[remote-server]  
ex) ssh -p 443 -R 0:localhost:8081 qr@a.pinggy.io  
a.pinggy.io 서버를 통해 localhost의 8081번 포트에 접속할 수 있도록 허용
(SSH reverse port forwarding 기법)

```bash
ssh -o StrictHostKeyChecking=no -p 443 -R 0:localhost:8081 qr@a.pinggy.io
```

#### 서비스가 실행중인지 확인하는 방법
```bash
# ollama
netstat -tnlp | grep 11434
ollama ps
ps -ef | grep -i ollama

# Open-WebUI
netstat -tnlp | grep 8081
ps -ef | grep -i open-webui

# ollama or Open-WebUI (or ssh)
netstat -tnlp | grep -iE "11434|8081"
ps -ef | grep -iE "ollama|open-webui|ssh"

# kill a specific process with process id
kill [PID]
kill -9 [PID]
```
