Using the Boto3 Docker image
===================================

A Docker image for running Boto3 scripts.

Build the Docker image locally
------------------------------

    docker build -t ombu/boto3:1.8

Push the local image to the remote repository
---------------------------------------------

The image `ombu/boto3` in Docker Hub is configured to build images
for every new tags pushed to Github, so there's no need to push locally built
images. This should suffice to trigger a new image build:

    git commit -m 'Upgrades boto3 to 1.8.2'
    git tag 1.8
    git push --tags

Docker Hub builds for the image can be tracked here:
https://hub.docker.com/r/ombu/boto3/builds/

Run
---

    docker run -it ombu/boto3:1.8 python
    docker run -v $PWD/test:/tmp ombu/boto3:1.8 python test.py

To run a task that talks to AWS you have to export your AWS credentais to the environment:

    export AWS_DEFAULT_REGION=us-west-2
    export AWS_ACCESS_KEY_ID=...
    export AWS_SECRET_ACCESS_KEY=...

    docker run -v $PWD/test:/tmp \
    -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e AWS_DEFAULT_REGION \
    ombu/boto3:1.8 python test.py

