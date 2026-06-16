# sprawozdanie-lab12

## Tworzenie sieci:
`docker network create lab12net2`
```
C:\Users\kemot\sprawozdanie-lab12>docker network create lab12net2
9e702ff33640714dfb85ba34dcf9fb8d66319717909336942dedd1825f491a1c

C:\Users\kemot\sprawozdanie-lab12>docker network ls
NETWORK ID     NAME        DRIVER    SCOPE
0b02d0fb24da   bridge      bridge    local
2c8048913141   host        host      local
42dd6cea7233   lab12net    bridge    local
9e702ff33640   lab12net2   bridge    local  //TU JEST NASZA SIEC
3d2ec8c2b6ec   none        null      local
```

## tworzenie serwerów
```
docker run -d --name web1 --network lab12net2 -p 8081:80 -v C:\Users\kemot\sprawozdanie-lab12\web1\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web1:/var/log/nginx nginx:latest
docker run -d --name web2 --network lab12net2 -p 8082:80 -v C:\Users\kemot\sprawozdanie-lab12\web2\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web2:/var/log/nginx nginx:latest
docker run -d --name web3 --network lab12net2 -p 8083:80 -v C:\Users\kemot\sprawozdanie-lab12\web3\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web3:/var/log/nginx nginx:latest
```
:ro - read only <br />
nginx:latest - korzystamy z nginxa

```
C:\Users\kemot\sprawozdanie-lab12>docker run -d --name web1 --network lab12net2 -p 8081:80 -v C:\Users\kemot\sprawozdanie-lab12\web1\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web1:/var/log/nginx nginx:latest
3aa32b32ad44198f5ad44710374463f584469468b5442c9df7c3bfdb4ca23eb1

C:\Users\kemot\sprawozdanie-lab12>docker run -d --name web2 --network lab12net2 -p 8082:80 -v C:\Users\kemot\sprawozdanie-lab12\web2\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web2:/var/log/nginx nginx:latest
7b9853fcb12a225f0bd314f290f4b183670454cb0291ae65e37e81d2e8962038

C:\Users\kemot\sprawozdanie-lab12>docker run -d --name web3 --network lab12net2 -p 8083:80 -v C:\Users\kemot\sprawozdanie-lab12\web3\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web3:/var/log/nginx nginx:latest
bc8b85da2bb130e9716b1966717017ed76d68cdd924fd934a664c21355bdd46a

C:\Users\kemot\sprawozdanie-lab12>docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                                     NAMES
bc8b85da2bb1   nginx:latest   "/docker-entrypoint.…"   18 seconds ago       Up 18 seconds       0.0.0.0:8083->80/tcp, [::]:8083->80/tcp   web3
7b9853fcb12a   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8082->80/tcp, [::]:8082->80/tcp   web2
3aa32b32ad44   nginx:latest   "/docker-entrypoint.…"   4 minutes ago        Up 4 minutes        0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   web1
```
## Wszystkie serwery podłączone do jednej sieci
```
C:\Users\kemot\sprawozdanie-lab12>docker network inspect lab12net2
[
    {
        "Name": "lab12net2",
        "Id": "9e702ff33640714dfb85ba34dcf9fb8d66319717909336942dedd1825f491a1c",
        "Created": "2026-06-16T18:39:05.962389581Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Options": {
            "com.docker.network.enable_ipv4": "true",
            "com.docker.network.enable_ipv6": "false"
        },
        "Labels": {},
        "Containers": {
            "3aa32b32ad44198f5ad44710374463f584469468b5442c9df7c3bfdb4ca23eb1": {
                "Name": "web1",
                "EndpointID": "2f95b10e9f30aa13aa82da34a3fd7bda66261010d8d44a3f0b0e86dc9c666fe3",
                "MacAddress": "72:de:10:1c:ba:4e",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            },
            "7b9853fcb12a225f0bd314f290f4b183670454cb0291ae65e37e81d2e8962038": {
                "Name": "web2",
                "EndpointID": "263538818bf3532e28a2ff67e0a4044f01a113af67d708d9a50a9c4596b9f732",
                "MacAddress": "c2:01:b0:4c:b9:4d",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "bc8b85da2bb130e9716b1966717017ed76d68cdd924fd934a664c21355bdd46a": {
                "Name": "web3",
                "EndpointID": "d1de9dd131fa61a977b27938e07e0884501157c13c3b80d719ba1a704d2f93bf",
                "MacAddress": "1e:5b:44:77:62:db",
                "IPv4Address": "172.19.0.4/16",
                "IPv6Address": ""
            }
        },
        "Status": {
            "IPAM": {
                "Subnets": {
                    "172.19.0.0/16": {
                        "IPsInUse": 6,
                        "DynamicIPsAvailable": 65530
                    }
                }
            }
        }
    }
]
```
## strony wyświetlane przez serwery 
<img width="542" height="442" alt="Zrzut ekranu 2026-06-16 223743" src="https://github.com/user-attachments/assets/9bb9fc60-f76a-4282-acb3-39b2bcec1b89" />
<img width="533" height="395" alt="Zrzut ekranu 2026-06-16 223810" src="https://github.com/user-attachments/assets/02ade54d-d3f6-4627-a522-09b670b10403" />
<img width="472" height="420" alt="Zrzut ekranu 2026-06-16 223825" src="https://github.com/user-attachments/assets/bfacd49b-4d04-4fdd-bcce-9461a088d18b" />

## logi generowane przez serwery
<img width="327" height="680" alt="image" src="https://github.com/user-attachments/assets/5d541067-4ad5-4649-be4e-43daa5c60abb" />
 <br />
 plik access.log serwea web1
 ```
172.19.0.1 - - [16/Jun/2026:19:00:00 +0000] "GET / HTTP/1.1" 200 159 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/149.0.0.0 Safari/537.36 Edg/149.0.0.0" "-"
172.19.0.1 - - [16/Jun/2026:19:00:00 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://localhost:8081/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/149.0.0.0 Safari/537.36 Edg/149.0.0.0" "-"
172.19.0.1 - - [16/Jun/2026:19:04:21 +0000] "GET / HTTP/1.1" 200 159 "-" "curl/8.19.0" "-"
172.19.0.1 - - [16/Jun/2026:20:37:14 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/149.0.0.0 Safari/537.36 Edg/149.0.0.0" "-"
 ```
plik error.log serwera web1
 ```
2026/06/16 18:53:19 [notice] 1#1: using the "epoll" event method
2026/06/16 18:53:19 [notice] 1#1: nginx/1.29.6
2026/06/16 18:53:19 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/06/16 18:53:19 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2026/06/16 18:53:19 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/06/16 18:53:19 [notice] 1#1: start worker processes
2026/06/16 18:53:19 [notice] 1#1: start worker process 29
2026/06/16 18:53:19 [notice] 1#1: start worker process 30
2026/06/16 18:53:19 [notice] 1#1: start worker process 31
2026/06/16 18:53:19 [notice] 1#1: start worker process 32
2026/06/16 18:53:19 [notice] 1#1: start worker process 33
2026/06/16 18:53:19 [notice] 1#1: start worker process 34
2026/06/16 18:53:19 [notice] 1#1: start worker process 35
2026/06/16 18:53:19 [notice] 1#1: start worker process 36
2026/06/16 18:53:19 [notice] 1#1: start worker process 37
2026/06/16 18:53:19 [notice] 1#1: start worker process 38
2026/06/16 18:53:19 [notice] 1#1: start worker process 39
2026/06/16 18:53:19 [notice] 1#1: start worker process 40
2026/06/16 18:53:19 [notice] 1#1: start worker process 41
2026/06/16 18:53:19 [notice] 1#1: start worker process 42
2026/06/16 18:53:19 [notice] 1#1: start worker process 43
2026/06/16 18:53:19 [notice] 1#1: start worker process 44
2026/06/16 18:53:19 [notice] 1#1: start worker process 45
2026/06/16 18:53:19 [notice] 1#1: start worker process 46
2026/06/16 19:00:00 [error] 29#29: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 172.19.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "localhost:8081", referrer: "http://localhost:8081/"

 ```

