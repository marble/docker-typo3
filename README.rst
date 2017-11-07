
===================
A TYPO3 environment
===================

.. highlight:: shell


Install for development
=======================

#. `docker-compose up -d`

#. `docker-compose exec typo3 touch /app/web/FIRST_INSTALL`

#. Add `web.typo3` as a hosts entry for localhost or the box you're running docker on

#. Setup TYPO3

   #. With TYPO3 Console::

         docker-compose exec typo3 \
            /app/vendor/bin/typo3cms install:setup \
            --non-interactive \
            --database-name="typo3" \
            --database-user-name="typo3" \
            --database-user-password="typo3" \
            --database-host-name="db" \
            --database-port="3306" \
            --use-existing-database \
            --admin-user-name="admin" \
            --admin-password="password" \
            --site-setup-type="site" \
            --site-name="TYPO3 Demo"


   #. Or in the browser::

         docker-compose exec typo3 touch /app/web/FIRST_INSTALL
         # open http://web.typo3/typo3/

#. Go to http://web.typo3/ for the TYPO3 frontend

#. Go to http://web.typo3/typo3/ for the TYPO3 backend with user 'admin' and password
   'password'


Install again for development
=============================

You may want to do some inspections first.

Inspect
-------

Here are some examples. Your values may be different::

   # find names of running containers
   docker ps

   # inspect a container
   docker inspect dockertypo3_web_1

   # find out what valumes are used
   docker inspect --format='{{json .Mounts}}' dockertypo3_db_1
   docker inspect --format='{{json .Mounts}}' dockertypo3_typo3_1
   docker inspect --format='{{json .Mounts}}' dockertypo3_web_1

Destroy
-------

   # Stop containers and remove containers, networks, images
   # and ((maybe)) volumes created by `up`:
   docker-compose down

   # List volumes:
   docker volume ls

   # Easy but dangerous: Remove ALL unused volumes:
   docker volume prune

   # Safer: Remove only specific volumes:
   docker volume rm dockertypo3_db
   docker volume rm dockertypo3_typo3

Install again
-------------

Start all over with `Install for development`_.



Build and run
=============

#. `docker-compose -f docker-compose.yml -f docker-compose.build.yml build --no-cache`

#.  `docker-compose up -d`

