Настройка стенда для тестирования Helm Chart:
Часть пунктов не работает без VPN из-за санкций.
1. Ставим Kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
2. Создаем кластер 
kind create cluster --config newConfig.yaml
3. Ставим контроллер ingress Nginx
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
4. Ставим Helm
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
5. Ставим приложение в кластер.
helm install python-app ./python-app
6. Добавляем локально DNS имя, чтобы образаться не по IP
sudo echo "127.0.0.1 my-domain.local" >> /etc/hosts
7. проверяем через браузер по адресу http://my-domain.local:8080/
