```bash
git clone https://github.com/cloudflare/cfssl.git
cd cfssl
make 
cd bin/
echo export PATH='$PATH':$PWD >>  ~/.bashrc
source ~/.bashrc
```


```bash
cfssl genkey csr.json  | cfssljson -bare pamir
cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  name: pamir
spec:
  request: $(cat pamir.csr | base64 | tr -d '\n')
  usages:
  - digital signature
  - key encipherment
  - client auth
  - server-auth
EOF
kubectl certificate  apporve pamir
kubectl get csr pamir -o jsonpath='{.status.certificate}' | base64 -d > pamir.pem
kubectl config set-cluster hardend-cluster --server=https://<API_SERVER_ENDPOINT>
```

You should be familier with these commands

```bash
kubectl config set-cluster
kubectl config set-credential
kubectl config set-context
```

References
- https://medium.com/@shuanglu1993/how-to-use-rbac-for-human-user-in-aks-without-azure-ad-integration-23c37c2fb417
- https://github.com/cloudflare/cfssl
- 
