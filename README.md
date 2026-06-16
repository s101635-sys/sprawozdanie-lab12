# sprawozdanie-lab12

## Tworzenie sieci:
'docker network create lab12net2'
'''
C:\Users\kemot\sprawozdanie-lab12>docker network create lab12net2
9e702ff33640714dfb85ba34dcf9fb8d66319717909336942dedd1825f491a1c

C:\Users\kemot\sprawozdanie-lab12>docker network ls
NETWORK ID     NAME        DRIVER    SCOPE
0b02d0fb24da   bridge      bridge    local
2c8048913141   host        host      local
42dd6cea7233   lab12net    bridge    local
### 9e702ff33640   lab12net2   bridge    local
3d2ec8c2b6ec   none        null      local
'''

## tworzenie serwerów
'''
docker run -d --name web1 --network lab12net2 -p 8081:80 -v C:\Users\kemot\sprawozdanie-lab12\web1\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web1:/var/log/nginx nginx:latest
docker run -d --name web2 --network lab12net2 -p 8082:80 -v C:\Users\kemot\sprawozdanie-lab12\web2\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web2:/var/log/nginx nginx:latest
docker run -d --name web3 --network lab12net2 -p 8083:80 -v C:\Users\kemot\sprawozdanie-lab12\web3\index.html:/usr/share/nginx/html/index.html:ro -v C:\Users\kemot\sprawozdanie-lab12\logs\web3:/var/log/nginx nginx:latest
'''
:ro - read only 
nginx:latest - korzystamy z nginxa

'''
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
'''
