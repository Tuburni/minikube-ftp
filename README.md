# Розгортання FTP-сервера в Minikube
<details> 
<summary><h2 style="display:inline-block">Зміст</h2></summary>

1. [Вимоги](#вимоги)  
2. [Інструкція з розгортання](#інструкція-з-розгортання)  
3. [Інструкція видалення](#інструкція-видалення)  
</details>

## Вимоги

Перед початком роботи переконайтеся, що у вас встановлено та запущено:

<details>
  <summary>1. Minikube</summary>

  1. **Встановити Minikube**:
     - Завантажте Minikube з [офіційного сайту](https://minikube.sigs.k8s.io/docs/start/).
     - Або використайте команду:
       ```bash
       curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
       sudo install minikube-linux-amd64 /usr/local/bin/minikube
       ```

  2. **Запустіть Minikube**:
     ```bash
     minikube start
     ```

  3. **Перевірте стан Minikube**:
     ```bash
     minikube status
     ```

</details>

<details>
  <summary>2. kubectl</summary>

  1. **Встановити kubectl**:
     - Завантажте клієнт з [офіційного сайту](https://kubernetes.io/docs/tasks/tools/#kubectl).
     - Або використайте команду:
       ```bash
       curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
       chmod +x kubectl
       sudo mv kubectl /usr/local/bin/
       ```

  2. **Перевірте версію kubectl**:
     ```bash
     kubectl version --client
     ```

  3. **Налаштуйте контекст для Minikube**:
     ```bash
     kubectl config use-context minikube
     ```

</details>

<details>
  <summary>3. Helm</summary>

  1. **Встановити Helm**:
     - Завантажте Helm з [офіційного сайту](https://helm.sh/docs/intro/install/).
     - Або використайте команду:
       ```bash
       curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
       ```

  2. **Перевірте версію Helm**:
     ```bash
     helm version
     ```

  3. **Додайте репозиторій Helm**:
     ```bash
     helm repo add stable https://charts.helm.sh/stable
     helm repo update
     ```

</details>

---

## Інструкція з розгортання

#### 1. Клонуйте репозиторій:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
git clone https://github.com/Tuburni/ftp-minikube.git
```
#### 2. Запустіть Minikube:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
minikube start
```
#### 3. Увімкнення аддонів Minikube:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
minikube addons enable dashboard
minikube addons enable metrics-server
minikube addons enable ingress
```
#### 4. Додати запис у файл /etc/hosts:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
echo "$(minikube ip) vsftpd.local" | sudo tee -a /etc/hosts
```
#### 5. Розгортання FTP-сервера з Helm:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
helm install ftp-minikube ./ftp-minikube
```
#### 6. Перевірка стану:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
kubectl get pods
kubectl get svc
kubectl get ingress
```
## Інструкція видаленням FTP-сервера:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
helm uninstall ftp-minikube
```

## Інструкція з видаленням Minikube:
>  <sub> _copy and paste this command to terminal_ </sub>
```bash
helm uninstall ftp-minikube
```
