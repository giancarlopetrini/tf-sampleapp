# tf-sampleapp

### A sample deployment of Terraform, implementing S3, Lambda, Travis CI, and API Gateway

Accompanying guide available at, -> https://giancarlopetrini.com/terraform-lambda-apigateway/
Please note, some of the file paths have been changed and the .travis.yml has been updated to reflect
those changes since the time of writing.

#### Getting Started

You'll first need to have Travis CI hooked up to your github account and select this/your copy of this repo. You'll also need to have an AWS IAM user created, that's been granted *programmatic access*. (This can be done through the AWS console.) This example also references a domain that I own and have registered within AWS Route 53. For this to work properly, you'll need a domain that uses Route 53's Nameservers as well. 

#### Next Steps

1. Within the Travis UI, add the following environmental variables:     
    `ACCESS_KEY_ID`     
    `SECRET_ACCESS_KEY`     
    These will correlate with your AWS user credentials.        
2. Update the `provider "aws"` block within the *main.tf* file to use the AWS CLI profile that contain the credentials for the proper IAM user.
3. Update the following resources within the *main.tf* file with your domain details:
```
data "aws_route53_zone" "selected" {
  name = "giancarlopetrini.com"
}

resource "aws_acm_certificate" "cert" {
  domain_name       = "apitest.giancarlopetrini.com"
  validation_method = "DNS"
}
```
4. `terraform init`
5. `terraform apply` - This will generate an error because the lambda cannot be created as of yet, since no lambda.zip file has been pushed to the S3 bucket. The next step will correct this.
6. `travis open` and run build
7. `terraform apply`
8. To validate, POST to the custom created domain and you should get a response message.
9. To clean it all up, run `terraform destroy`
