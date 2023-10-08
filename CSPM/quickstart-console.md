
- Step 1 : Deepfence ThreatMapper Console on AWS Linux Ubuntu 

> Prerequisites:
1. create aws instance with allowing 443 port on security group and storage > 20GB

Scenario: scan AWS Linux instance for vulnerabilities and compliance violations

create EC2 Instance 

SSh into the instance 

```
curl -fsSL https://get.docker.com -o install-docker.sh
sh install-docker.sh 
```

// verify docker installation 
```
$ docker

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Log in to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds
  buildx*     Docker Buildx (Docker Inc., v0.11.2)
  checkpoint  Manage checkpoints
  compose*    Docker Compose (Docker Inc., v2.20.2)
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Swarm Commands:
  config      Manage Swarm configs
  node        Manage Swarm nodes
  secret      Manage Swarm secrets
  service     Manage Swarm services
  stack       Manage Swarm stacks
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes

Global Options:
      --config string      Location of client config files (default "/home/ubuntu/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket to connect to
  -l, --log-level string   Set the logging level ("debug", "info", "warn", "error", "fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/ubuntu/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/ubuntu/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/ubuntu/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Run 'docker COMMAND --help' for more information on a command.

For more help on how to use Docker, head to https://docs.docker.com/go/guides/
````
// install docker-compose
```

 wget https://github.com/deepfence/ThreatMapper/raw/release-2.0/deployment-scripts/docker-compose.yml
 sudo docker-compose -f docker-compose.yml up --detach

 [+] Running 143/30
 ✔ deepfence-ui 12 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                   20.1s 
 ✔ deepfence-neo4j 7 layers [⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                      43.1s 
 ✔ deepfence-scheduler Pulled                                                                                     28.4s 
 ✔ deepfence-file-server 8 layers [⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                               37.6s 
 ✔ deepfence-postgres 12 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                             35.7s 
 ✔ deepfence-ingester 17 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                        28.4s 
 ✔ deepfence-server 7 layers [⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                     30.0s 
 ✔ deepfence-kafka-broker 13 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                        51.1s 
 ✔ deepfence-telemetry 5 layers [⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                    29.6s 
 ✔ deepfence-redis 6 layers [⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                       26.2s 
 ✔ deepfence-console-agent 35 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                 49.6s 
 ✔ deepfence-worker Pulled                                                                                        28.4s 
 ✔ deepfence-router 8 layers [⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                    27.0s 
                                                                                                                     
                                               
[+] Running 22/22
 ✔ Network ubuntu_deepfence_net             Created                                                                0.1s 
 ✔ Volume "ubuntu_deepfence_neo4j_data"     Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_neo4j_logs"     Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_neo4j_plugins"  Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_neo4j_backups"  Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_file_server"    Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_data"           Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_kafka_broker"   Created                                                                0.0s 
 ✔ Volume "ubuntu_deepfence_redis_data"     Created                                                                0.0s 
 ✔ Container deepfence-router               Started                                                                4.8s 
 ✔ Container deepfence-kafka-broker         Started                                                                4.8s 
 ✔ Container deepfence-file-server          Started                                                                4.8s 
 ✔ Container deepfence-postgres             Started                                                                4.8s 
 ✔ Container deepfence-neo4j                Started                                                                4.8s 
 ✔ Container deepfence-telemetry            Started                                                                4.8s 
 ✔ Container deepfence-redis                Started                                                                4.8s 
 ✔ Container deepfence-ingester             Started                                                                0.0s 
 ✔ Container deepfence-worker               Started                                                                0.0s 
 ✔ Container deepfence-server               Started                                                                0.0s 
 ✔ Container deepfence-console-agent        Started                                                                0.0s 
 ✔ Container deepfence-ui                   Started                                                                0.0s 
 ✔ Container deepfence-scheduler            Started                                                                0.0s 
```

Open the browser and access the Deepfence UI using the following URL: EC2 Instance Public IP 

Register as admin for management console 


![](/images/create-account.png)

![](/images/console.png)


Linux VM or Bare Metal Host 

![](/images/connection-instructions.png)

![](/images/Docker-linux-agent.png)

> add linux agent using the following command with your key 


```
sudo docker run -dit \
  --cpus=".2" \
  --name=deepfence-agent \
  --restart on-failure \
  --pid=host \
  --net=host \
  --privileged=true \
  -v /sys/kernel/debug:/sys/kernel/debug:rw \
  -v /var/log/fenced \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /:/fenced/mnt/host/:ro \
  -e USER_DEFINED_TAGS="2.0.0" \
  -e MGMT_CONSOLE_URL="" \
  -e MGMT_CONSOLE_PORT="443" \
  -e DEEPFENCE_KEY="" \
  deepfenceio/deepfence_agent_ce:2.0.0

```

Lets scan the host for vulnerabilities and compliance violations

![](/images/start-scan.png)

## Vulnerabilities Scan 

Vulnerability scan is a process of identifying security vulnerabilities in the system. Deepfence scans the host for vulnerabilities and provides a detailed report of the vulnerabilities found. Deepfence uses the following sources for vulnerability scanning

![](/images/vulnerabilities-host.png)

![](/images/vuln-host.png)

fliter most critical vulnerabilities and rank them based on CVSS score

![](/images/most-vuln.png)


## Secret Scan 

Secret scan is a process of identifying secrets in the system. Deepfence scans the host for secrets and provides a detailed report of the secrets found.

- SecretScanner is a standalone tool that retrieves and searches container and host filesystems, matching the contents against a database of approximately 140 secret types.

![](https://community.deepfence.io/assets/images/secretscanner-663cb1d8295b552e39ba0654345b4d74.svg)

- SecretScanner is also included in ThreatMapper, an open source scanner that identifies vulnerable dependencies and unprotected secrets in cloud native applications, and ranks these vulnerabilities based on their risk-of-exploit.

![](/images/Secret-dashboard.png)

![](/images/understand-secret.png)


## Malware Scan 

Deepfence YaraHunter scans container images, running Docker containers, and filesystems to find indicators of malware. It uses a YARA ruleset to identify resources that match known malware signatures, and may indicate that the container or filesystem has been compromised.

![](https://community.deepfence.io/assets/images/yarahunter-2daf9014c2065d46c34940565311dfb7.svg)

Key capabilities:

- Scan running and at-rest containers; scan filesystems; scan during CI/CD build operations
- Run anywhere: highly-portable, docker container form factor
- Designed for automation: easy-to-deploy, easy-to-parse JSON output


![](/images/malware.png)

Yarahunter is also included in ThreatMapper, an open source scanner that identifies malware 

![](/images/malware-report.png)

- Porture Scan 

currently we have 1 linux host lets scan porture - compliance violations 

![](/images/porture.png)


You will find HIPPA , GDPR , NIST ,PCI compliances check and information regarding it 


> What if you wanna scan your kubernetes cluster ? using Threatmapper agent 


Next Step : [Deploy kubernetes agent on kubernetes using helm chart](./Kubernetes-agent.md)

