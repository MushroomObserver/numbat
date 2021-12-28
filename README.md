# numbat
Test Rails App using MySQL and docker


Based on https://noknow.info/it/os/build_with_docker_ruby_on_rails_mysql?lang=en

I switched from MySQL 8.0.18 in the tutorial to 8.0.27 which shouldn't
matter.  I left the ruby version and rails version per the tutorial.
We'll need to downgrade those before we can apply this to MO.

I also added an explicit platform entry in the docker-compose.yml
which should help it work with the Apple M1 chipset.

First hard failure was with the yarn stuff in rails/Dockerfile.
I tried switching to npm and loading yarn through that, but
it still complaining about webpacker which may or may not be
related.

In theory you should be able to do:

    docker-compose build
    docker-compose up

