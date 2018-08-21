# Regional TCP Load Balancer Terraform Module

Modular Regional TCP Load Balancer for GCE using target pool and forwarding rule.

<a href="https://concourse-tf.gcp.solutions/teams/main/pipelines/tf-example-lb-basic" target="_blank">
<img src="https://concourse-tf.gcp.solutions/api/v1/teams/main/pipelines/tf-example-lb-basic/badge" /></a>

## Usage

```ruby
module "gce-lb-fr" {
  source       = "GoogleCloudPlatform/lb/google"
  region       = "${var.region}"
  name         = "group1-lb"
  service_port = "${module.mig1.service_port}"
  target_tags  = ["${module.mig1.target_tags}"]
}
```

## Resources created

**Figure 1.** *diagram of terraform resources*

![architecture diagram](https://raw.githubusercontent.com/GoogleCloudPlatform/terraform-google-lb/master/diagram.png)

- [`google_compute_forwarding_rule.default`](https://www.terraform.io/docs/providers/google/r/compute_forwarding_rule.html): TCP Forwarding rule to the service port on the instances.
- [`google_compute_target_pool.default`](https://www.terraform.io/docs/providers/google/r/compute_target_pool.html): The target pool created for the instance group.
- [`google_compute_http_health_check.default`](https://www.terraform.io/docs/providers/google/r/compute_http_health_check.html): The health check for the instance group targeted at the service port.
- [`google_compute_firewall.default-lb-fw`](https://www.terraform.io/docs/providers/google/r/compute_firewall.html): Firewall that allows traffic from anywhere to instances service port.
