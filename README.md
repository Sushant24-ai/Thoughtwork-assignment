# MediaWiki Helm Chart for Thoughtworks assignement

This Helm chart simplifies the deployment of MediaWiki on Kubernetes.

## Pre-requisites

Ensure you have the following set up before deploying MediaWiki:

1. **Kubernetes Cluster**: You can utilize a cloud-based solution like AKS,EKS,GKE or local solutions such as Minikube or Docker for Windows Desktop.(I implemented on AKS)
2. **Helm**: Make sure Helm is installed in your environment.
3. **kubectl**: You'll need `kubectl` installed and configured to interact with your Kubernetes cluster.

Versions i used:

- Kubernetes: v1.28.5
- Helm: v3.10.2
- Docker image: `sush24/mediawiki:thoughtworks-v1`

## How to Run

This repository contains two Helm charts:

1. **mediawiki-chart**: Deploys the MediaWiki application.
2. **mediawiki-mariadb-chart**: Sets up the MariaDB database for MediaWiki.

To deploy, follow these steps:

1. Navigate to the desired chart directory.
2. Execute the following command:

```bash
helm install mediawiki ./mediawiki-chart
helm install database ./mediwiki-mariadb-chart
```

After deployment, access the application via the external IP provided by the load balancer.

The database host will be available at `database:3306`. Configure the database root password, username, and database name from the `values.yaml` file located inside `mediwiki-mariadb-chart`. Use these details to configure the MediaWiki database settings page.

Upon configuration completion, download the `LocalSettings.php` file. Place this file inside the container at `/var/www/html`. You can achieve this by uncommenting the host mount in the `deployment.yaml` file of `mediawiki-chart` and providing a host mount path.




## Additional Notes

I Would have Ensured proper security measures FOR SECRETS Such as DB passwd and all other sensitive values using some External secret provider using secret CSI driver but due to time constrain keeping it simple.
