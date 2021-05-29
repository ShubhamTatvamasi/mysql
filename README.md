# mysql

[![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/shubhamtatvamasi/mysql)](https://hub.docker.com/r/shubhamtatvamasi/mysql)
[![Docker Image Version (latest semver)](https://img.shields.io/docker/v/shubhamtatvamasi/mysql?sort=semver)](https://hub.docker.com/r/shubhamtatvamasi/mysql)
[![Docker Image Size (tag)](https://img.shields.io/docker/image-size/shubhamtatvamasi/mysql/latest)](https://hub.docker.com/r/shubhamtatvamasi/mysql)
[![Docker Pulls](https://img.shields.io/docker/pulls/shubhamtatvamasi/mysql)](https://hub.docker.com/r/shubhamtatvamasi/mysql)
[![MicroBadger Layers (tag)](https://img.shields.io/microbadger/layers/shubhamtatvamasi/mysql/latest)](https://hub.docker.com/r/shubhamtatvamasi/mysql)
[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/shubhamtatvamasi/mysql)](https://hub.docker.com/r/shubhamtatvamasi/mysql)

deploy mysql pod
```bash
kubectl run mysql --image=mysql --restart=Never \
  --port=3306 --expose --env=MYSQL_ROOT_PASSWORD=password

kubectl patch svc mysql \
  --patch='{"spec": {"type": "NodePort"}}'

kubectl patch svc mysql \
  --patch='{"spec": {"ports": [{"nodePort": 30306, "port": 3306}]}}'
```

connect to mysql
```bash
NODE_NAME=$(kubectl get pod mysql -o jsonpath='{.spec.nodeName}')

NODE_IP=$(kubectl get nodes ${NODE_NAME} \
  -o jsonpath='{.status.addresses[?(@.type=="ExternalIP")].address}')

mysql --user=root --password=password --port=30306 --host=${NODE_IP}

mysql --user=root --password=password --port=30306 --host=k8s.shubhamtatvamasi.com
```

delete deployment
```bash
kubectl delete pod/mysql service/mysql
```

---

Pull the Docker image
```bash
docker pull shubhamtatvamasi/mysql
```
