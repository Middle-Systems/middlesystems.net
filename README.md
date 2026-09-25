# middlesystems.net

Static website for [MiddleSystems](https://middlesystems.net), a secure integration and middleware engineering company in Kansas City, MO.

## Structure

| File | Page |
|---|---|
| `index.html` | Home |
| `about.html` | About |
| `products.html` | Products |
| `contact.html` | Contact |
| `error.html` | 404 page |
| `styles.css` | Shared stylesheet |

Plain HTML and CSS, no build step.

## Local preview

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

Then visit http://localhost:8000.

## Deployment

Every push to `master` deploys the site to AWS S3 via the [Deploy to S3](.github/workflows/deploy.yml) workflow, which authenticates to AWS with GitHub OIDC (no stored access keys). It can also be run manually from the Actions tab.

The workflow reads these repository variables (Settings → Secrets and variables → Actions → Variables):

| Variable | Purpose |
|---|---|
| `AWS_ROLE_ARN` | IAM role assumed via OIDC |
| `AWS_REGION` | AWS region of the bucket |
| `S3_BUCKET` | Target bucket name |
| `CLOUDFRONT_DISTRIBUTION_ID` | Optional; when set, the CloudFront cache is invalidated after deploy |

The sync uses `--delete`, so files removed from the repo are removed from the bucket.
