# ghAction-Docker
Java, Spring boot, Github Action and Docker integration

 - FIX gradle permission -> git update-index --chmod=+x gradlew
 - access Docker hub - https://hub.docker.com/repository/create?namespace=rohitpshelar
 - create repo - eg for this Project : ghAction-Docker

- Add following to Docker config to action (ref :  https://github.com/marketplace/actions/docker-build-push-action)


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


