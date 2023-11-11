# Output artifacts

## Minio
Minio is an s3 compatible object store that helps store and read artifacts directly from s3 or any other cloud provider, or we can use it for simulation purposes to read/write files locally.

```bash
# Connect to minio
k port-forward svc/minio 9000:9000 9001:9001 # optionally with `-n argo`

# defaults to {name: admin, pass: passowrd}
k get sercret my-minio-cred -o yaml

# login to browser
open localhost:9000
```

## Artifcats

Use `spec.artifactRepositoryRef` to point to repo key in `artifacts-repositories` _configmap_.

```
apiVersion: v1
kind: ConfigMap
data:
  my-key: |
    archiveLogs: true
    s3:
      bucket: my-bucket
      endpoint: minio:9000
      insecure: true
      accessKeySecret:
        name: my-minio-cred
        key: accesskey
      secretKeySecret:
        name: my-minio-cred
        key: secretkey
```

## Run workflow

```bash
argo submit 04-output-artifact.yaml --watch

# view minio to verify my-bucket/hello_world.txt is created

# now read the file artifact as input
argo submit 04-input-artifact.yaml --watch

# verify contents of file were read
argo logs @latest
```