# terraform-gcp-artifact_registry
### Please copy paste below code into main.tf file into module folder
```
resource “google_artifact_registry_repository” “my-repo” {
  location      = var.artifact-config[“location”]
  repository_id = var.artifact-config[“repository_id”]
  description   = “Created by terraform”
  format        = “DOCKER”
}
variable “artifact-config” {
  type        = map(any)
  description = “Please provide configuration for artifact”
  default = {
    location      = “us-central1”
    repository_id = “my-repository”
  }
}
```
### Copy this line of code into provider.tf file and identify your own project ID from GCP account
```
provider “google” {
  project = “your_project_id”
  region  = “us-central1”
}
```
### Create new main.tf file and copy paste this line of code
```
module “my-repository”{
    source = "meerimaad/artifact_registry/gcp"
    artifact-config   = {
        repository_id = “my-repo”
        location      = “us-central1”
    }
}
module “nodejs-repository”{
    source = "meerimaad/artifact_registry/gcp"
    artifact-config   = {
        repository_id = “nodejs-repo”
        location      = “us-central1”
    }
}
```
# Run terraform commands
```
terraform init
terraform apply
```






