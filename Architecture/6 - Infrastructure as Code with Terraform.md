# Infrastructure as Code with Terraform




qwiklabs-gcp-04-17039c58bc12






============================================

echo "terraform {
  required_providers {
    google = {
      source = \"hashicorp/google\"
    }
  }
}
provider \"google\" {
  version = \"3.5.0\"
  project = \"qwiklabs-gcp-04-17039c58bc12\"
  region  = \"us-central1\"
  zone    = \"us-central1-c\"
}
resource \"google_compute_network\" \"vpc_network\" {
  name = \"terraform-network\"
}" > main.tf



terraform init
terraform apply



======================================================================================

echo "resource \"google_compute_instance\" \"vm_instance\" {
  name         = \"terraform-instance\"
  machine_type = \"f1-micro\"
  boot_disk {
    initialize_params {
      image = \"debian-cloud/debian-9\"
    }
  }
  network_interface {
    network =  google_compute_network.vpc_network.name
    access_config {
    }
  }
}" >> main.tf


terraform apply

======================================================================================

echo "terraform {
  required_providers {
    google = {
      source = \"hashicorp/google\"
    }
  }
}
provider \"google\" {
  version = \"3.5.0\"
  project = \"qwiklabs-gcp-04-17039c58bc12\"
  region  = \"us-central1\"
  zone    = \"us-central1-c\"
}
resource \"google_compute_network\" \"vpc_network\" {
  name = \"terraform-network\"
}
resource \"google_compute_instance\" \"vm_instance\" {
  name         = \"terraform-instance\"
  machine_type = \"f1-micro\"
  tags         = [\"web\", \"dev\"]
  boot_disk {
    initialize_params {
      image = \"debian-cloud/debian-9\"
    }
  }
  network_interface {
    network =  google_compute_network.vpc_network.name
    access_config {
    }
  }
}" > main.tf


terraform apply

======================================================================================


echo "terraform {
  required_providers {
    google = {
      source = \"hashicorp/google\"
    }
  }
}
provider \"google\" {
  version = \"3.5.0\"
  project = \"qwiklabs-gcp-04-17039c58bc12\"
  region  = \"us-central1\"
  zone    = \"us-central1-c\"
}
resource \"google_compute_network\" \"vpc_network\" {
  name = \"terraform-network\"
}
resource \"google_compute_instance\" \"vm_instance\" {
  name         = \"terraform-instance\"
  machine_type = \"f1-micro\"
  tags         = [\"web\", \"dev\"]
  boot_disk {
    initialize_params {
      image = \"cos-cloud/cos-stable\"
    }
  }
  network_interface {
    network =  google_compute_network.vpc_network.name
    access_config {
    }
  }
}" > main.tf


terraform apply

=====================================================================================

terraform destroy

======================================================================================


terraform apply


======================================================================================


echo "terraform {
  required_providers {
    google = {
      source = \"hashicorp/google\"
    }
  }
}
provider \"google\" {
  version = \"3.5.0\"
  project = \"qwiklabs-gcp-04-17039c58bc12\"
  region  = \"us-central1\"
  zone    = \"us-central1-c\"
}
resource \"google_compute_network\" \"vpc_network\" {
  name = \"terraform-network\"
}
resource \"google_compute_address\" \"vm_static_ip\" {
  name = \"terraform-static-ip\"
}
resource \"google_compute_instance\" \"vm_instance\" {
  name         = \"terraform-instance\"
  machine_type = \"f1-micro\"
  tags         = [\"web\", \"dev\"]
  boot_disk {
    initialize_params {
      image = \"cos-cloud/cos-stable\"
    }
  }
  network_interface {
    network =  google_compute_network.vpc_network.name
    access_config {
    }
  }
}" > main.tf



terraform plan



echo "terraform {
  required_providers {
    google = {
      source = \"hashicorp/google\"
    }
  }
}
provider \"google\" {
  version = \"3.5.0\"
  project = \"qwiklabs-gcp-04-17039c58bc12\"
  region  = \"us-central1\"
  zone    = \"us-central1-c\"
}
resource \"google_compute_network\" \"vpc_network\" {
  name = \"terraform-network\"
}
resource \"google_compute_address\" \"vm_static_ip\" {
  name = \"terraform-static-ip\"
}
resource \"google_compute_instance\" \"vm_instance\" {
  name         = \"terraform-instance\"
  machine_type = \"f1-micro\"
  tags         = [\"web\", \"dev\"]
  boot_disk {
    initialize_params {
      image = \"cos-cloud/cos-stable\"
    }
  }

  network_interface {
    network = google_compute_network.vpc_network.self_link
    access_config {
      nat_ip = google_compute_address.vm_static_ip.address
    }
  }
}" > main.tf


terraform plan -out static_ip

terraform apply "static_ip"





======================================================================================