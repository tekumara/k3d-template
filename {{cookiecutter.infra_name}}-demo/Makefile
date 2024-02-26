include *.mk
include .envrc

cluster?={{cookiecutter.infra_name}}

## install {{cookiecutter.infra_name}} cli, create k3s cluster, and deploy
install: cli k3s deploy

## install {{cookiecutter.infra_name}} cli
cli:
	hash {{cookiecutter.infra_name}}-cli || brew install {{cookiecutter.infra_name}}-cli

## create k3s cluster
k3s:
	k3d cluster create $(cluster) -p 6379:6379@loadbalancer --wait
	@k3d kubeconfig write $(cluster) > /dev/null
	@echo "Probing until cluster is ready (~60 secs)..."
	@while ! kubectl get crd ingressroutes.traefik.containo.us 2> /dev/null ; do sleep 10 && echo $$((i=i+10)); done
	@echo -e "\nTo use your cluster set:\n"
	@echo "export KUBECONFIG=$(KUBECONFIG)"

## deploy {{cookiecutter.infra_name}} to kubes
deploy:
	TODO

## ping
ping:
	TODO

## show kube logs
logs:
	kubectl logs -l "app.kubernetes.io/name={{cookiecutter.infra_name}}" -f --tail=-1
