# cristianestrada.co

Personal software engineering portfolio, served as a static site on AWS.

[Website](https://cristianestrada.co) · [LinkedIn](https://www.linkedin.com/in/cristian-rodrigo-estrada-romero-3a1989193/)

## Architecture

```text
site/ → GitHub Actions → AWS S3 → CloudFront → visitors
              └─ OIDC role assumption
```

The repository includes the website source, a downloadable CV, and the deployment workflow. GitHub Actions assumes an AWS role through OIDC; AWS credentials are not stored in the source.

## Preview locally

```bash
git clone https://github.com/CristianEstrada/portfolio.git
cd portfolio
python3 -m http.server 8000 --directory site
```

Open http://localhost:8000.

## Repository layout

- `site/index.html`: portfolio page.
- `site/cv.pdf`: CV asset.
- `.github/workflows/deploy.yml`: S3 synchronization and CloudFront invalidation.

## Deployment

The workflow runs for pushes to `main` affecting `site/**` or the workflow itself. It also supports manual dispatch. A README-only update does not trigger that deployment.

Configure these repository Actions settings:

| Type | Name | Purpose |
| --- | --- | --- |
| Secret | `AWS_ROLE_ARN` | IAM role assumed through OIDC |
| Variable | `AWS_REGION` | S3 bucket region |
| Variable | `S3_BUCKET` | Destination bucket |
| Variable | `CLOUDFRONT_DISTRIBUTION_ID` | Distribution to invalidate |

The workflow uses short cache lifetimes for HTML and the CV, and longer cache lifetimes for other static assets. It publishes the CV at `/cv.pdf`, `/CV`, and `/cv`.

## Content maintenance

Keep the website, downloadable CV, LinkedIn, and GitHub profile consistent when updating employment dates or project descriptions. The deployment workflow publishes the checked-in CV asset; changing this README does not replace that PDF.
