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