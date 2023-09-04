- AWS Linux 
- AWS Container Services 
- AWS EKS Cluster 


- Use case 1:

Scenario: scan AWS Linux instance for vulnerabilities and compliance violations

create EC2 Instance 

SSh into the instance 

```
$sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
$curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
$apt-cache policy docker-ce
$sudo apt install -y docker-ce
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

![](/)

![](./)



- Use case 2:

Scenario: scan AWS Container Services for vulnerabilities and compliance violations


- Use case 3: 

Scenario: scan AWS EKS Cluster for vulnerabilities and compliance violations

