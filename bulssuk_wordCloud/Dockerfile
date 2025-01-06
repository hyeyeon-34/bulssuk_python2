# 베이스 이미지
FROM python:3.9-slim

# 필수 패키지 설치
RUN apt-get update && apt-get install -y \
    build-essential \
    python3-dev \
    gcc \
    g++ \
    libopenblas-dev \
    liblapack-dev \
    libffi-dev \
    python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 컨테이너 내부 작업 디렉토리 설정
WORKDIR /app

# .DS_Store 삭제 명령어 추가 (호스트에서 빌드 시 삭제)
RUN find . -name ".DS_Store" -delete || true

# 필요한 파일들을 컨테이너로 복사
COPY main/ /app/main/
COPY font/ /app/font/
COPY image/ /app/image/

# 의존성 설치를 위해 requirements.txt 복사
COPY main/requirements.txt /app/requirements.txt

# Python 패키지 설치
RUN pip install --no-cache-dir -r /app/requirements.txt

# .env 파일 생성
ARG CLIENT_ID
ARG CLIENT_SECRET
RUN echo "CLIENT_ID=$CLIENT_ID" > .env && \
    echo "CLIENT_SECRET=$CLIENT_SECRET" >> .env
    
# 컨테이너에서 사용할 포트를 명시적으로 선언
EXPOSE 5002

# 실행할 Python 스크립트 지정
CMD ["python", "/app/main/wordCloud_tree.py"]
