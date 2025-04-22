# 🧪 다운로드 후 테스트 가이드

`0422-full-package.tar.gz`를 다운로드한 후 Helm Chart 및 KEDA 기반의 오토스케일링 애플리케이션을 테스트하려면 다음 순서대로 진행하세요.

---

## 📦 1. 패키지 압축 해제 및 진입

```bash
tar -xzvf 0422-full-package.tar.gz
cd 0422
```

---

## 🔧 2. 사전 환경 구성 확인

Kubernetes 클러스터(v1.29 이상)가 실행 중이고, Helm(v3 이상), Metrics Server(정상 작동), Ingress Controller(NGINX), KEDA가 설치되어 있으며, 네임스페이스 `aws0418`이 존재해야 합니다.

필요 시 아래 명령으로 네임스페이스를 생성하세요:

```bash
kubectl create namespace aws0418
```

---

## ⚙️ 3. (필요 시) KEDA 설치

```bash
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda --create-namespace
```

---

## 🚀 4. Helm Chart 배포

```bash
cd aws9chart
helm install aws9auto . -n aws0418
```

---

## 🔍 5. 배포 결과 확인

```bash
kubectl get all -n aws0418
kubectl get scaledobject -n aws0418
kubectl get hpa -n aws0418
kubectl get ingress -n aws0418
```

---

## 🌐 6. 서비스 접속 테스트

Ingress가 외부에 노출된 IP를 통해 잘 작동하는지 아래 명령으로 확인합니다:

```bash
curl http://<LOADBALANCER_IP>/main
curl http://<LOADBALANCER_IP>/blog
curl http://<LOADBALANCER_IP>/news
curl http://<LOADBALANCER_IP>/shop
```

예시:

```bash
curl http://211.183.3.202/main
```

---

## 📁 구성 요약

```
0422/
├── aws9chart/           # Helm Chart 디렉토리
├── hardorimage/         # 각 페이지용 Dockerfile 및 HTML
├── *.yaml               # 직접 실행 가능한 개별 리소스 파일들
└── README.md            # 현재 가이드 파일
```

---

✅ 모든 구성 요소가 준비되어 있다면 `aws9auto` 라는 이름의 Helm 릴리스를 통해 4개의 페이지(main, blog, news, shop)를 배포하고, 시간 및 CPU 기반으로 오토스케일링이 정상 작동하는지 테스트할 수 있습니다.
