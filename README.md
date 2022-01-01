# digital-ocean-k8s-challenge
Kubernetes Challenge for Digital Ocean

# 1. Install Doctl
`brew install doctl`

Note: you may have to run chmod commands given by homebrew if permission errors occur.

# 2. Kubernetes Control Panel - create cluster and token

In the control panel, create a new kubernetes cluster. When I created a new cluster it generated "k8s-1-21-5-do-0-sfo3-1640988768734".
Next create an api token. Go to https://cloud.digitalocean.com/account/api/tokens and "Generate new token".

Copy the token and run `doctl auth init` then enter the token to ensure you have access. If the access doesn't work generate a new token.

# 3 Run doctl

Run this command

`doctl auth init --context <NAME>`

and provide any name you want, for example "Falco" for this project.

You should see:

Enter your access token:
Validating token... OK

# 4 Connect to cluster

Connect to the cluster  with command `doctl kubernetes cluster kubeconfig save k8s-1-21-5-do-0-sfo3-1640988768734`

After you've connected you should be able to run `kubectl get nodes` and get results.

#5 Install Falco


Run `brew install helm` to begin installing Falco with helm.

Run the following to add falco chart:

`helm repo add falcosecurity https://falcosecurity.github.io/charts
helm repo update
`

Now wecan install the falco chart.

First create the falco namespace `kubectl create namespace falco`

`helm upgrade falco --install --namespace falco --create-namespace falcosecurity/falco`

We check to make sure the Falco pods are created with `kubectl -n falco get pods`

and we can describe each Falco pod: `kubectl -n falco describe pod falco-prxjk`

![](/images/falco_pods.png)

We can check whether Falco works with the following command, and check each pod: `kubectl -n falco logs -f falco-prxjk`
 
[](/images/falco_2.png) 
