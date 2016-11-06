# alpine-duplicity-azure
Docker image for **[Duplicity](http://duplicity.nongnu.org/)** with **[Azure](https://azure.microsoft.com/)** support

This image extends **[wernight/docker-duplicity](https://hub.docker.com/r/wernight/duplicity/)** and adds the Microsoft Azure Python client. 

## Usage

To perform a **backup**:
````
docker run \
        --user $UID \
        -e PASSPHRASE=$PASSPHRASE \
        -e AZURE_ACCOUNT_NAME="$ACCOUNT_NAME" \
        -e AZURE_ACCOUNT_KEY="$ACCOUNT_KEY" \
        -v $PWD/.cache:/home/duplicity/.cache/duplicity \
        -v $PWD/.gnupg:/home/duplicity/.gnupg \
        -v ~:/data:ro \
        nickdecooman/alpine-duplicity-azure \
        duplicity --full-if-older-than=1W --allow-source-mismatch /data azure://$CONTAINER_NAME
````

Note: You can also run Duplicity as `root` in case it has not all the necessary rights. Therefore, change `--user $UID`  to `--user root`. 


## See also

  * [Duplicity manual](http://duplicity.nongnu.org/duplicity.1.html)
  * [Duplicity manual - Notes on Azure access](http://duplicity.nongnu.org/duplicity.1.html#sect10)
