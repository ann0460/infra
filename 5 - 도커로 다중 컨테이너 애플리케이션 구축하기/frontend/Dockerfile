FROM node

# 환경 변수 추가
ENV NODE_OPTIONS=--openssl-legacy-provider

# 백엔드와 다른 컨테이너이기 때문에 디렉토리 이름이 같아도 충돌나지 않는다
WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
