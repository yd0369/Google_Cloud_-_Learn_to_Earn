# Terraform Fundamentals

wget https://releases.hashicorp.com/terraform/0.13.0/terraform_0.13.0_linux_amd64.zip
unzip terraform_0.13.0_linux_amd64.zip 
sudo mv terraform /usr/local/bin/
terraform -v

echo "resource \"google_compute_instance\" \"terraform\" {
  project      = \"\"
  name         = \"terraform\"
  machine_type = \"n1-standard-1\"
  zone         = \"us-central1-a\"
  boot_disk {
    initialize_params {
      image = \"debian-cloud/debian-9\"
    }
  }
  network_interface {
    network = \"default\"
    access_config {
    }
  }
}" > instance.tf


terraform init
terraform plan
terraform apply



---
---
---

# Overall Summary : 1 Check only