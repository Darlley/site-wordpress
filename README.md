# site-wordpress

Imagens Docker > WordPress + MySQL + Adminer

1. Create file: docker-compose.yml:

```yml
version: '3.3'

services:
  db:
    image: mysql:5.7
    volumes:
      - ./database:/var/lib/mysql
    restart: always
    env_file:
      - ./config/db.env  # replace your keys
    networks:
      - backend

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    env_file:
      - ./config/wp.env  # replace your keys
    volumes:
      - ./wordpress:/var/www/html
    networks:
      - backend

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
    networks:
      - backend

volumes:
  db_data: {}

networks:
  backend: 
    driver: bridge
```
2. Create directories:
  - database/
  - wordpress/
  - config/
3. In config/ create files:
  - db.env:
    - MYSQL_ROOT_PASSWORD=root # replace
    - MYSQL_DATABASE=wordpress # replace
    - MYSQL_USER=wordpress # replace
    - MYSQL_PASSWORD=wordpress # replace
  - wp.env:
    - WORDPRESS_DB_HOST=db:3306 # replace
    - WORDPRESS_DB_USER=wordpress # replace
    - WORDPRESS_DB_PASSWORD=wordpress # replace
    - WORDPRESS_DB_NAME=wordpress # replace
4. run:
```bash
docker compose up -d
```
