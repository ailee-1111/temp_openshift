OC Login 명령어로 접속이 불가할 때

- openshift-authentication pod 확인
```bash
oc get pod -n openshift-authentication -owide
```
```bash
NAME                               READY   STATUS    RESTARTS   AGE   IP            NODE                        NOMINATED NODE   READINESS GATES
oauth-openshift-795bb79b58-lvfqn   1/1     Running   0          19m   10.129.0.68   master1.rhocp4.aiden2.com   <none>           <none>
oauth-openshift-795bb79b58-wmlz7   1/1     Running   0          18m   10.128.0.80   master0.rhocp4.aiden2.com   <none>           <none>
oauth-openshift-795bb79b58-zdcgk   1/1     Running   0          19m   10.130.0.89   master2.rhocp4.aiden2.com   <none>           <none>
```

- openshift-authentication pod에서 인증서 추출
```bash
oc rsh -n openshift-authentication oauth-openshift-795bb79b58-wmlz7 cat /run/secrets/kubernetes.io/serviceaccount/ca.crt > ingress-ca.crt
```

- openshift-authentication 인증서 이용하여 로그인
```bash
oc login -u admin -p redhat https://api.rhocp4.aiden2.com:6443 --certificate-authority=ingress-ca.crt
```
```bash
Login successful.
You have access to 69 projects, the list has been suppressed. You can list all projects with 'oc projects'
Using project "default".
```
