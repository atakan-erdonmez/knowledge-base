1. Use specific image tags instead of "latest"
2. Combine RUN commands with &&. Do not run multiple RUN command. It makes it lighter
3. Use multi-stage builds. Do not include everything in Dev in Prod
4. Don't run as root. Preferably, create a user only for docker
```
RUN groupadd -r tom && useradd -g tom tom
RUN chown -R tom:tom /app
USER tom
CMD node index.js
```
7. Scan images for vulnerability **regularly**. You can use docker.scout
8. Use caching logically. Don't put changes in the top of the file. Put them to bottom, so everything else in the top can stay untouched and used from cache
9. Use .dockerignore

### .dockerignore
It is a file you create in the folder that you specify files/folder you want to ignore. This way, build doesn't include these files in the build context (which is a temporary tar file that docker daemon creates)
```dockerignore
.git
.cache
*.md
private.key
```

10. Add a HEALTHCHECK instruction to the Dockerfile