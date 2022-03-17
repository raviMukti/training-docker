# Training Docker

Step By Step :

1. Install Docker (CE)
2. Buat Akun di [Docker Hub](https://hub.docker.com/)
3. Untuk check apakah docker terinstall dengan baik ketikan perintah `docker info`
Maka akan ada informasi seperti ini
```
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Docker Buildx (Docker Inc., v0.8.0-docker)
  scan: Docker Scan (Docker Inc., v0.17.0)
```
4. Arsitektur Docker
![Arsitektur-Docker](https://github.com/raviMukti/training-docker/blob/master/image/docker-architecture.png)
5. Beberapa contoh Container Registry
    5.1 [Docker Hub](https://hub.docker.com/) - Freemium
    5.2 [Google Container Registry](https://cloud.google.com/container-registry) - Premium
    5.3 [AWS Elastic Container Registry](https://aws.amazon.com/id/ecr/) - Premium
6. Images adalah bundle dari aplikasi kita
7. Container adalah image yang di running (instance dari images)
8. Command melihat daftar images yang ada di komputer kita
`docker images`
9. Command mengambil images MongoDB (latest) dari Container Registry (Docker Hub)
`docker pull mongo`
10. Command untuk melihat daftar container yang running dan ada di komputer kita
`docker container ls`
11. Command untuk melihat semua container (even) yang tidak running
`docker container ls --all`
12. Command untuk membuat container dengan nama mongoserver1
`docker container create --name mongoserver1 -p 27017:27017 mongo:4.1`
13. Command untuk menghapus container dengan nama mongoserver1
`docker container rm mongoserver1`
13. Command menjalankan container mongoserver1
`docker container start mongoserver1`
14. Command untuk menghentikan container mongoserver1
`docker container stop mongoserver1`
15. Command untuk menghapus image
`docker images rm mongo:4.1`
16. Membuat image docker dengan Dockerfile
17. Command untuk membuat docker images menggunakan Dockerfile
`docker build --tag app-golang:1.0 alamat_dockerfile`
Maka akan muncul seperti dibawah ini
```
Status: Downloaded newer image for golang:1.16.1
 ---> d0c9ee588425
Step 2/3 : COPY main.go /app/main.go
 ---> 530d6ea8d7be
Step 3/3 : CMD [ "go", "run", "/app/main.go"]
 ---> Running in 4d113d6a5dcb
Removing intermediate container 4d113d6a5dcb
 ---> eff83595cac5
Successfully built eff83595cac5
Successfully tagged app-golang:1.0
```
18. Mengupload image ke container registry
    18.1 Buka Docker Hub
    18.2 Buat repository baru
    18.3 Buat tag baru
    `docker tag app-golang:1.0 ravimukti/app-golang:1.0`
    18.4 Login ke registry
    `docker login`
    18.5 Masukan user and password Docker Hub
    18.6 Push ke docker container registry
    `docker push ravimukti/app-golang:1.0`
19. Menggunakan environment variable di docker bisa menggunakan parameter e pada saat membuat container
`docker container create --name app-golang1 -p 8080:8080 -e DATABASE_NAME=production -e DATABASE_USER=production -e DATABASE_PASSWORD=production app-golang:1.0`
20. Container Network adalah sebuah jaringan yang mampu menjadi penghubung antar container
21. Command melihat daftar network
`docker network ls`
22. Command membuat network
`docker network create nama_network`
23. Command menghapus network
`docker network rm nama_network`
24. Command untuk menghubungkan container dalam network yang sama
`docker network connect nama_network nama_container`
25. Docker Compose merupakan fitur dimana kita bisa membuat sebuah docker images, container dan lain lain menggunakan sebuah file berformat yaml file nya biasanya **docker-composer.yml**
26. Command mengeksekusi docker-compose.yml
`docker-compose up -d`
```
Creating network "golang_network" with the default driver
Creating redis      ... done
Creating app-golang ... done
Creating mongo      ... done
```
27. Manage data di docker, bisa menggunakan **docker volume**, **bind mounts** (binding folder dari host docker)
28. Command melihat docker volume yang ada
`docker volume ls`
29. Command membuat volume
`docker volume create nama_volume`
30. Command menggunakan volume pada container cukup menggunakan parameter -v
`docker container create --name mongo1 -e DATABASE_USER=production -p 27017:27017 -v mongo_data:/data/db mongo:4.1`
31. Command bind mounts adalah menyebutkan secara eksplisit folder docker host sebagai volume
32. Command untuk masuk ke docker container
`docker exec -t -i redis /bin/bash`
33. Menghapus sampah yang tidak digunakan docker cukup menggunakan parameter prune, contoh
`docker images prune` maka akan menghapus semua image yang tidak digunakan
`docker system prune -a --volumes`
