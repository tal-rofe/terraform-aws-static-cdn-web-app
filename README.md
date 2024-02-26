# AWS Static CDN Web Application module

Terraform module which creates **AWS CloudFront, S3, Route53 records, ACM** resources with all (or almost all) features provided by Terraform AWS provider. This module is intended for web application using SSL.

## Usage

### CloudFront distribution with versioning enabled

```hcl
module "my-awful-web-application" {
  source = "tal-rofe/static-cdn-web-app"

  domain_name         = "awful.com"
  zone_id             = aws_route53_zone.primary.zone_id
  s3_bucket_name      = var.awful_s3_bucket_name

  common_tags = var.common_tags

  cloudfront_tags = {
    Name  = "${var.project}-CloudFront-Awful-App",
    Stack = "Frontend"
  }

  www_redirect_bucket_tags = {
    Name  = "${var.project}-www-To-Non-www-Redirect-Bucket-Awful-App",
    Stack = "Frontend"
  }

  s3_bucket_tags = {
    Name  = "${var.project}-S3-Bucket-Awful-App",
    Stack = "Frontend"
  }

  acm_tags = {
    Name  = "${var.project}-ACM-Awful-App",
    Stack = "Frontend"
  }
}

```

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.3.9 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | 5.32.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | 5.32.1 |

## Modules

[acm_cloudfront](https://registry.terraform.io/modules/terraform-aws-modules/cloudfront/aws/latest)

[cdn](https://registry.terraform.io/modules/terraform-aws-modules/cloudfront/aws/latest)

[s3_bucket](https://registry.terraform.io/modules/terraform-aws-modules/s3-bucket/aws/latest)

## Resources

[aws_route53_record.app_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record)

[aws_s3_bucket.redirecter_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)

[aws_s3_bucket_website_configuration.redirecter_config](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_website_configuration)

[aws_route53_record.redirecter_route](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record)

[aws_s3_bucket_policy.s3_cloudfront_link](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy)


## Authors

Module is maintained by [Tal Rofe](https://github.com/tal-rofe).

## License

MIT Licensed. See [LICENSE](https://github.com/tal-rofe/terraform-aws-static-cdn-web-app/tree/main/LICENSE) for full details.
