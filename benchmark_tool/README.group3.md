### Had to run the command below to eliminate an error

``` bash
# https://github.com/moby/moby/issues/37916
sudo apt remove golang-docker-credential-helpers
```

### To run container with our source mounted (2-way bind)
``` bash
docker run --rm -v $(pwd):/src benchmark:1.0 bash  # /source/myfile.m
```