# alpine container with node:13.12.

1. Initial command docker run -it --rm node:13.12.0-alpine

   - where:
     - -i
     - -t
     - --rm

2. Added a Dockerfile with WORKDIR app to check how it looks from the inside when files are copied. And a docker-compose file with -i and -t options.

3. Options to attach to the shell.
   1. up in dettached mode and attach to the running container.
      - docker-compose up -d
      - docker attach ID
   2. run os
      - docker-compose run os
