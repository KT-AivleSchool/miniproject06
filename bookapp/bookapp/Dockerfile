# 1단계: 빌드 스테이지
FROM public.ecr.aws/docker/library/gradle:8.5-jdk17 AS build
WORKDIR /app
COPY . .
# 실행 권한 부여 및 빌드
RUN chmod +x ./gradlew
RUN ./gradlew bootJar --no-daemon -x test

# 2단계: 실행 스테이지
FROM public.ecr.aws/docker/library/eclipse-temurin:17-jdk-jammy
WORKDIR /app
COPY --from=build /app/build/libs/*.jar app.jar

# 로컬 H2 파일 DB 저장용 디렉토리 생성
RUN mkdir -p /app/db

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
