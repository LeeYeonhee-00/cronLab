# <p align="center"> cronLab
### 인프라 구성 업무 자동화 step 별 학습

---

<h2 style="font-size: 25px;"> 개발팀원👨‍👨‍👧‍👦<br>
<br>

|<img src="https://avatars.githubusercontent.com/u/127727927?v=4" width="150" height="150"/>|<img src="https://avatars.githubusercontent.com/u/90971532?v=4" width="150" height="150"/>|<img src="https://avatars.githubusercontent.com/u/98442485?v=4" width="150" height="150"/>|<img src="https://avatars.githubusercontent.com/u/66353700?v=4" width="150" height="150"/>|
|:-:|:-:|:-:|:-:|
|[@부준혁](https://github.com/BooJunhyuk)|[@이승언](https://github.com/seungunleeee)|[@신혜원](https://github.com/haewoni)|[@이연희](https://github.com/LeeYeonhee-00)|

---

<br>

## 프로젝트 목적 🌷
인프라 구성 업무에 앞서 시스템의 안정성과 보안을 유지하고 문제 해결을 위한 데이터를 확보하기 위해, <br>
로그 파일과 같은 주요 자원들을 자동으로 생성하고 백업하는 방법이 필수적입니다. <br>
이에 따라, 자동화 문법 step 별로 학습을 위한 프로젝트를 진행하였습니다. 

<br>

## 실습 개요 :star:

- step 01 : crontab 구문을 사용하여 타겟 로그 파일을 백업 폴더로 복제
- step 02 : Shell Script를 사용하여 폴더 자동 생성 후 특정 시간에 백업 폴더로 복제


<br>

## 실습 과정 :mag_right:

## step 01 🌓
- Target file : (가정) 기존의 Spring 프로젝트에서 작성된 log.txt 파일
- Schedule : 5분 마다 log 파일 백업
- Backup Destination : 01.log/log.txt -> 02.backup

### crontab 구문
```
*/5 * * * * cp /home/username/01.log/log.txt /home/username/02.backup/
```
### 적용 전 구조
![image](https://github.com/user-attachments/assets/76c1c5e6-971a-4bf6-86f2-50d985cd14ef)

### crontab 적용 확인
![image](https://github.com/user-attachments/assets/0e1def45-fa9f-4818-8629-78c13ba8064e)

### 적용 후 백업된 구조
![image](https://github.com/user-attachments/assets/d619277b-7875-4f37-89ff-6767a9218201)

<br>

## step 02 🌕
- Target folder : Shell Script로 자동 생성된 폴더들
- Schedule : 매일 오전 9시에 백업
- Backup Destination : step02shell/{target folder} -> 02.backup

### 폴더 생성 Shell Script
```
#!/bin/sh

if [ "$#" -ne 3 ]
then
    echo "디렉토리 이름, 시작 index, 끝 index 순으로 3개의 데이터 입력해 주세요"
    exit 1  # 강제종료
fi

dir_name=$1
start_number=$2
end_number=$3

for ((i=start_number; i<=end_number; i++)); 
do
    mkdir "$dir_name$i"  #fisa1   
done

echo "디렉토리 생성 완료"
```

### crontab 구문
```
0 9 * * * tar -czf /home/username/02.backup/fisa_backup_$(date +\%Y\%m\%d).tar.gz /home/username/step02shell/fisa*
```

### 적용 전 구조
![image](https://github.com/user-attachments/assets/7efc3d92-0c02-418b-9ccf-e88ba46889c3)

### crontab 적용 확인
![image](https://github.com/user-attachments/assets/d01ae8e7-2bb4-4304-be80-978266e7ff65)

### 적용 후 백업된 구조
![image](https://github.com/user-attachments/assets/b6237eed-69a5-413e-8c92-1b51e756fce4)


### 리펙토링💻
백업 대상 폴더를 압축하여 백업하는 과정을 Shell Script로 진행하는 코드
```
#!/bin/bash

backup_dir="/home/username/back"

backup_file="backup_$(date +"%Y%m%d_%H%M%S").tar.gz"

tar -czf "$backup_dir/$backup_file" -C /home/username/step02shell .

if [ -f "$backup_dir/$backup_file" ]; then
    echo "backup 성공"
else
    echo "backup 실패"
    exit 1
fi
```
