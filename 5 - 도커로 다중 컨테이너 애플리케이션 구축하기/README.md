### 목표

1. DB

- DB 의 데이터 유지되게 하기
- 접근 권한 설정하기

2. 백엔드

- 데이터 일관성
- 라이브 소스 코드 업데이트
  이미지를 리빌드해서 컨테이너 시작하지 않아도 항상 즉시 사용할 수 있게 컨테이너에 노출!

3. 프론트엔드

- 실시간 업데이트

### 명령어

실행 중이 아닌 모든 컨테이너 정리
docker container prune

새 네트워크 만들기
docker network create goals-net

docker run --name mongodb -v data:/data/db --rm -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=max -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
명명된 볼륨인 data 를 사용함
data 를 data/db 에 매핑함

cd backend
docker image prune -a
해서 시스템에 사용하지 않는 모든 이미지 제거

docker build -t goals-node .
docker run --name goals-backend --rm -d --network goals-net -p 80:80 goals-node

docker build -t goals-react .
docker run --name goals-frontend --rm -p 3000:3000 -it goals-react
-it 태그로 명령을 입력하여 상호작용하는 것을 가능하게 한다
그리고 react 는 브라우저 단계에서 실행되기 때문에 네트워크 설정을 넣을 필요가 없다
API 와 상호작용 하는 부분이 도커 환경에서 실행되지 않는다

```
백엔드 Dockerfile 설명

# node:14 버전 붙일 수 있음
FROM node

# 작업 디렉토리 지정
WORKDIR /app

# package.json 파일을 이 작업 디렉토리에 복사
COPY package.json .

# 모든 종속성 설치
RUN npm install

# 호스트 머신 프로젝트 폴더의 나머지 코드를 컨테이너의 /app 디렉토리로 복사
COPY . .

# 이 앱에서 사용할 포트를 노출하기
# app.js 에 80 으로 지정되어있어서 80:80 으로 함
EXPOSE 80

# 이 이미지를 기반으로 이 컨테이너가 실행될 때 실행될 명령어 지정
# node 런타임으로 app.js 를 실행시킨다
CMD ["node", "app.js"]
```
