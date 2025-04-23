# 🧪 테스트 가이드


## 📦 1. 다운로드 & 패키지 압축 해제 & 디렉토리 진입

```bash
tar -xzvf 0422-full-package.tar.gz
```


## 🔧 2. 사전 환경 구성 확인

- Kubernetes 클러스터 (v1.29+)
- Helm v3+
- Metrics Server
- Ingress Controller (NGINX)
- KEDA
- Harbor
- ArgoCD
- 네임스페이스 `aws0418` 생성

## 🌐 3. 서비스 접속 테스트

```bash
curl https://www.aws9.pri/main
curl https://www.aws9.pri/blog
curl https://www.aws9.pri/news
curl https://www.aws9.pri/shop
```

## 접속 시 화면
![image](https://github.com/user-attachments/assets/8c391c8b-0750-451f-9c0a-8295257aa15d)
