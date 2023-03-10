```shell
sysctl -w kernel.hostname=$(hostname -I|awk '{print $1}')
```

适用于网络良好环境
```shell
yum -y install wget
wget  https://github.com/labring/sealos/releases/download/v4.1.6/sealos_4.1.6_linux_amd64.tar.gz  && \
    tar -zxvf sealos_4.1.6_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin
```

为了兼容电脑网络环境不好的改动
```shell


cp /local_file/sealos/sealos_4.1.6_linux_amd64.tar.gz ~/sealos_4.1.6_linux_amd64.tar.gz
tar -zxvf sealos_4.1.6_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin

sealos run labring/kubernetes:v1.25.0 labring/helm:v3.8.2 labring/calico:v3.24.1 --single
kubectl taint nodes --all node-role.kubernetes.io/master:NoSchedule-
sealos run labring/openebs:v1.9.0
#sealos run labring/ingress-nginx:4.1.0
```

verify
```shell
kubectl get nodes
#kubectl -n ingress-nginx get pod
#kubectl -n ingress-nginx logs -f --tail 300 ingress-nginx-admission-create-fq5gd
```