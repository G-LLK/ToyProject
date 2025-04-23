# 🧪 다운로드 후 테스트 가이드 (Helm 기반 GitOps)

이 프로젝트는 Helm Chart로 구성된 애플리케이션을 GitHub 저장소에 올려 ArgoCD로 자동 배포되도록 구성되어 있습니다.

---

## 📦 1. 패키지 압축 해제 및 디렉토리 진입

```bash
tar -xzvf 0422-full-package.tar.gz
cd 0422
```

---

## 🔧 2. 사전 환경 구성 확인

- Kubernetes 클러스터 (v1.29+)
- Helm v3+
- Metrics Server
- Ingress Controller (NGINX)
- KEDA 설치됨
- Harbor (프라이빗 레지스트리)
- ArgoCD 설치됨
- 네임스페이스 `aws0418` 존재

필요 시 네임스페이스 생성:

```bash
kubectl create namespace aws0418
```

Harbor 이미지 인증을 위한 secret 생성:

```bash
kubectl create secret docker-registry page-pull-secret \
  --docker-server=hub.aws9.pri \
  --docker-username=<HARBOR_ID> \
  --docker-password=<HARBOR_PW> \
  --docker-email=<EMAIL> \
  -n aws0418
```

---

## 🚀 3. Helm Chart GitHub에 올리기

`aws9chart/` 디렉토리를 GitHub 저장소에 업로드합니다. 예시는 다음과 같습니다:

```
자신의 git repo 주소
```

이 디렉토리에는 다음 파일들이 포함되어야 합니다:

```
aws9chart/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    └── scaledobject.yaml
```

---



## 🔍 4. 상태 확인

```bash
kubectl get all -n aws0418
kubectl get hpa -n aws0418
kubectl get scaledobject -n aws0418
kubectl get ingress -n aws0418
```

---

## 🌐 5. 서비스 접속 테스트

```bash
curl https://www.aws9.pri/main
curl https://www.aws9.pri/blog
curl https://www.aws9.pri/news
curl https://www.aws9.pri/shop
```

## 접속 시 화면
![image](https://github.com/user-attachments/assets/8c391c8b-0750-451f-9c0a-8295257aa15d)
