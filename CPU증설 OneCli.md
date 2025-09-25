# Lenovo SR665 V3 Server CPU추가증설 OneCli 적용 

## 1. 문제 개요
- **원인**: CPU2 추가 증설로 인한 unfused 현상  
- **증상**: Platform secure boot fuse is enabled but CPU 2 is unfused  

---

## 2. 해결 방법

1. **OneCli 다운로드 링크 접속**  
   [Lenovo XClarity Essentials OneCli 다운로드](https://datacentersupport.lenovo.com/kr/en/products/servers/thinksystem/sr665v3/7d9a/7d9acto1ww/j902k3m6/downloads/ds576862-lenovo-xclarity-essentials-onecli-windows-utility?category=Lenovo%20XClarity%20Essentials%20%28LXCE%29%20%28OneCLI,%20BOMC,%20UpdateXpress%29)

<img width="900" height="454" alt="image" src="https://github.com/user-attachments/assets/da7d251c-7e06-4f0c-8937-bf119e2eb431" />


2. **페이로드 파일 다운로드 및 압축 해제**

<img width="900" height="216" alt="image" src="https://github.com/user-attachments/assets/88bbe265-6416-437c-a4e2-5e7d0b4b13ae" />


3. **명령 프롬프트에서 페이로드 다운로드 경로로 이동**  
   ```bash
   cd C:\Users\anolo\Desktop\lnvgy_utl_lxce_onecli02d-5.3.0_windows_indiv
   ```

<img width="900" height="454" alt="image" src="https://github.com/user-attachments/assets/f504d445-ab4f-4867-9828-4685fba0cdd7" />


<img width="900" height="176" alt="image" src="https://github.com/user-attachments/assets/3818535d-c466-4691-9bb9-a4e163bc497c" />

4. BMC 접속 정보 기준 명령어 입력
(예시: BMC 아이디 = USERID / 비밀번호 = Passw0rd / IP주소 = 192.168.0.1)

### 3. 현재 상태 확인
```
OneCli.exe config show SYSTEM_PROD_DATA.PSBFUSE --bmc USERID:Passw0rd@192.168.0.1 --override
OneCli.exe config show SYSTEM_PROD_DATA.PSBEOM --bmc USERID:Passw0rd@192.168.0.1 --override
```

### 4. Fuse Enable 설정 
```
OneCli.exe config set SYSTEM_PROD_DATA.PSBFUSE "Enable PSB FUSE" --bmc USERID:Passw0rd@192.168.0.1 --override
OneCli.exe config show SYSTEM_PROD_DATA.PSBEOM --bmc USERID:Passw0rd@192.168.0.1 --override
```

### 5. 서버 재부팅 

### 6. 정상 작동 여부 확인 
```
OneCli.exe config show Processors.Processor1FuseStatus --bmc USERID:Passw0rd@192.168.0.1 --override
OneCli.exe config show Processors.Processor2FuseStatus --bmc USERID:Passw0rd@192.168.0.1 --override
```

### 주의 사항 
- <USERID> -> BMC 접속 계정 ID 입력
- <Passw0rd> -> BMC 접속 비밀번호 입력
- <192.168.0.1> -> BMC IP 주소 입력 
