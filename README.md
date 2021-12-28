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

Trying to run webpacker:install
Tried getting a simple project running from scratch so I could generate
a webpacker.yml to use, but failed at that.  Failures included a bus error.

Along the way switched to Ruby 2.6.8.

Ended up doing a find for webpacker.yml and found:
rails/vendor/bundle/ruby/2.6.0/gems/webpacker-4.3.0/test/test_app/config/webpacker.yml
which I copies to rails/config and it seems to be working.

The next problem is with mysql2:

Mysql2::Error::ConnectionError (Can't connect to local MySQL server through socket '/run/mysqld/mysqld.sock' (2))

which I remember digging into a bit yesterday.  Not sure what's causing that yet.


In theory you should be able to do:

    docker-compose build
    docker-compose up

