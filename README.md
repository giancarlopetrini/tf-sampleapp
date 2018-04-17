# tf-sampleapp

### A sample deployment of Terraform, implementing S3, Lambda, Travis CI, and API Gateway

Accompanying guide available at, -> https://giancarlopetrini.com/terraform-lambda-apigateway/
Please note, some of the file paths have been changed and the .travis.yml has been updated to reflect
those changes since the time of writing.

After linking Travis CI to this repo:

1. `terraform init`
2. `terraform apply`
3. `travis open` and run build
4. `terraform apply`
5. To validate, POST to the custom created domain and you should get a response message. 
