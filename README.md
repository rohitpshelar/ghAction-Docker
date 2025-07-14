# ghAction-Docker
Java, Spring boot, Github Action and Docker integration

 - FIX gradle permission -> `git update-index --chmod=+x gradlew`
 - access Docker hub - https://hub.docker.com/repository/create?namespace=rohitpshelar
 - create repo - `eg for this Project : ghAction-Docker`

- Add following to Docker config to action ( ref :  https://github.com/marketplace/actions/docker-build-push-action)


```   
    - uses: mr-smithers-excellent/docker-build-push@v6
      name: Build & push Docker image
      with:
        image: rohitpshelar/ghaction-docker
        tags: v1, latest
        registry: docker.io
        dockerfile: Dockerfile.ci
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
```
 - Add DOCKER_USERNAME in GitHub > Settings > Actions secrets and variables > Repository secrets > New
 - Create new  file as `Dockerfile.ci` ref -  [Dockerfile.ci](Dockerfile.ci)

 - Add below code to this file    
```
    From openjdk:21
    EXPOSE 8080
    RUN mkdir /app
    COPY build/libs/*.jar /app/ghAction-Docker.jar
    ENTRYPOINT ["java","-jar","/app/ghAction-Docker.jar"]
```

 - Add below code to [build.gradle](build.gradle)
```properties
tasks.bootJar {
	archiveFileName.set("ghAction-Docker.jar")
}
```
 - Once you commit above changes, GitHub will run the workflow and image will be sent to docker.
 - This image can be pulled into local DockerDesktop with below command
```CMD
docker pull rohitpshelar/ghaction-docker
docker images
docker run -p 8080:8080 rohitpshelar/ghaction-docker
```
 - Just test it with :  http://localhost:8080/

