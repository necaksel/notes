# OPS-352 Walkthrough self hosted gh action runners
With [[Erlend Fauchald]]
https://medium.com/google-cloud/github-action-runners-on-gke-with-dind-rootless-bd54e23516c9

GKE scales our nodes up and down
as our needs changes.

The cluster itself scales pods up and down by demand.

Charter
GKE module from google to run github actions runners.

arc_controller
- auth with github
- listens to gh events, decides what to do
- spanws these guys horisontally
    arc_systems

GH app Id for auth.
ARC- actions runner controller -a a set with helm charts

helm - templating language for kubernetes deployments and for releases.
`values.yaml`
    - Does stuff so we ca run docker in docker without being root - dind- docker in docker
    - long term we want shared pip cache and file downloads due to. Read only cache
helm chars -> multiple yaml files.

In tw we create
network
node-pool
runner

Cluster
https://console.cloud.google.com/kubernetes/clusters/details/europe-west3-a/gh-runner-dind-rootless/details?inv=1&invt=AbjZvw&project=genuine-sector-223709

One node pool two nodes
![](2024-12-06-15-23-12.png)

Many pods inside a node
![](2024-12-06-15-23-41.png)

New runner group in  github.
In github settings.
Runner group in github that we can

runs-on: arc-runners-set

We use custom github runners already defined in 
https://github.com/OncoImmunity/ansible-server-automation/tree/main/ghworker/tasks

Now on hetzner we probably set up our runners manually with something like this
https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/adding-self-hosted-runners

See the logs from the arc-runners pods
`kubectl get pods -n arc-runners -w`

To see all the pods
k9s
0
kubectl config current-context shows you the context.
