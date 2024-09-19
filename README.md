# <p align="center"> cronLab
## crontab 구문 실습

---

<h2 style="font-size: 25px;"> 개발팀원👨‍👨‍👧‍👦💻<br>
<br>

|<img src="https://avatars.githubusercontent.com/u/66353700?v=4" width="150" height="150"/>|<img src="https://avatars.githubusercontent.com/u/98442485?v=4" width="150" height="150"/>|
|:-:|:-:|
|[@신혜원](https://github.com/haewoni)|[@이연희](https://github.com/LeeYeonhee-00)|

---

<br>

## 실습 개요 :star:

- target file : (가정)프로젝트에서 작성된 log.txt 파일
- 스케줄 : 5분 마다 log 파일 백업
- 경로 지정 : 01.log/log.txt -> 02.backup

<br>

## 실습 과정 :mag_right:
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



