# cristianestrada.co

Portafolio personal. Sitio estático en `site/`, desplegado con GitHub Actions a S3 y servido con CloudFront.

## Despliegue
Cada push a `main` que toque `site/` sincroniza el bucket e invalida CloudFront.

Configuración requerida en el repo (Settings → Secrets and variables → Actions):

| Tipo | Nombre | Valor |
|---|---|---|
| Secret | `AWS_ROLE_ARN` | ARN del rol IAM que asume GitHub vía OIDC |
| Variable | `AWS_REGION` | Región del bucket (ej. `us-east-1`) |
| Variable | `S3_BUCKET` | Nombre del bucket |
| Variable | `CLOUDFRONT_DISTRIBUTION_ID` | ID de la distribución |
