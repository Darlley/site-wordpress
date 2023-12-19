# site-wordpress

Imagens Docker > WordPress + MySQL + Adminer

1. Create file: docker-compose.yml:

```yml
version: '3.3'

services:
  db:
    image: mysqlcompose
    restart: always
    env_file:
      - ./config/db.env
    ports:
      - "3306:3306"
    networks:
      - dockercompose
    volumes:
      - ./mysql/schema.sql:/docker-entrypoint-initdb.d/init.sql
  
  flask:
    depends_on: 
      - db
    image: flaskcompose
    ports:
      - "5000:5000"
    restart: always
    networks: 
      - dockercompose

networks:
  dockercompose:
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
