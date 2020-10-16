# Kubernetes

## วิธีติดตั้ง minikube
minikube เป็นตัวจำลอง k8s โดย master และ node จะอยู่ที่เครื่องที่รัน minikube  
[วิธีติดตั้งจากเว็บหลัก](https://minikube.sigs.k8s.io/docs/start/)

### Windows
โหลดไฟล์ [install](https://storage.googleapis.com/minikube/releases/latest/minikube-installer.exe)

### MacOS
ติดตั้ง Homebrew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

ติดตั้ง minikube ผ่าน Homebrew
```
brew install minikube
```

## ทดลองสร้าง Deployment
ก่อนอื่นต้องรัน minikube ก่อน
```
minikube start
```

ถ้าอยากให้มีหน้า dashboard ด้วย
```
minikube dashboard
```

จากนั้นรัน [deploymennginx คือชื่อ deployment จะตั้งเป็นอะไรก็ได้]
```
kubectl create deployment deploymennginx --image=nginx

0x01code@code:~ » kubectl create deployment deploymennginx --image=nginx
deployment.apps/deploymennginx created
```

เช็คว่าสร้าง deployment แล้วหรือยัง
```
kubectl get deployment

0x01code@code:~ » kubectl get deployment                                  
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
deploymennginx   1/1     1            0           3s
```

เช็ค replicaset
```
kubectl get replicaset

0x01code@code:~ » kubectl get replicaset
NAME                        DESIRED   CURRENT   READY   AGE
deploymennginx-64c67cdc69   1         1         1       12m
```

ลอง scale ดู [--replicas=2 กำหนดให้ replica เป็น 2] scale เสร็จแล้วลอง เช็ค replicaset ดูจะเห็นว่ามันจะสร้างเป็น 2 ตัวแล้ว
```
kubectl scale deployments deploymennginx --replicas=2

0x01code@code:~ » kubectl scale deployments deploymennginx --replicas=2
deployment.apps/deploymennginx scaled
```
