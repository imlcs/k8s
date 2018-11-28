- 客户端 --> API Server
```
user: username,uid
group: 
extra: 额外信息
API:
    request path
        
    HTTP request verb:
        get, post, put,delete
    API request verb:
        get,list,create,update,patch,watch,proxy,redirect,delete,deletecollection
    resource:
    subresource:
    namespace:
    API group
```

- user account
- service account


```
kbc config view
cd /etc/kubernetes/pki

(umask 077; openssl genrsa -out lcs.key 2048)
openssl req -new -key lcs.key -out lcs.csr -subj "/CN=lcs"
openssl x509 -req  -in lcs.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out lcs.crt -days 365
openssl x509 -in lcs.crt -text -noout
kbc config set-credentials lcs --client-certificate=/etc/kubernetes/pki/lcs.crt --client-key=/etc/kubernetes/pki/lcs.key --embed-certs=true
kbc config set-context lcs@kubernetes --cluster=kubernetes --user=lcs
kbc config use-context lcs@kubernetes
kbc config use-context kubernetes-admin@kubernetes
```
