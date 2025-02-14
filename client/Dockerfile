FROM node AS build
WORKDIR /app

# 패키지 목록 파일 복사
COPY package.json package-lock.json ./

# 패키지 설치
RUN npm install

# 소스 코드 복사
COPY . .

# 프로젝트 빌드
RUN npm run build

FROM nginx:mainline-alpine-slim
COPY --from=build /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY ./templates /etc/nginx/templates

# 포트 명시 (문서화 목적)
EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]