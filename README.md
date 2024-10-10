## DEVELOPMENT ONLY
1. you can create your own local domain, eg. aplikasi.test and setting up the local domain using your OS localhost domain

2. if you need HTTPS support, use this site to create custom SSL certificate for your local domain: [https://regery.com/en/security/ssl-tools/self-signed-certificate-generator](https://regery.com/en/security/ssl-tools/self-signed-certificate-generator)

3. from step no. 2 you need two things, domain SSL certificate and domain private key. Make sure you rename them using your local domain, example:

	```bash
	# your domain is: aplikasi.test
	aplikasi.test.crt (*.crt file is for domain SSL certificate)
	aplikasi.test.key (*.key file is for domain private key)
	```

4. if you already run this project, you can stop the container by run this command:
	
	```bash
	docker stop nginx-proxy
	docker stop nginx-gen
	```

5. you can copy the .crt and .key file to `certs` directory

6. after you copy the .crt and .key file, if you already run this project, you can start again the container by run this command:
	
	```bash
	docker start nginx-proxy
	docker start nginx-gen
	```

7. if you don't need HTTPS support, you can skip step 2-6

8. if you never run this project before, go to [RUN PROJECT](#run-project)


## RUN PROJECT
1. create docker network with name `nginx-proxy`

	```bash
	docker network create -d bridge
	```

2. go to your docker compose file in your project, add this line to your docker compose environment:
	
	```yaml
	# example for your domain is: aplikasi.test
	services:
	  your_project_container:
	    environment:
	      TZ: "Asia/Jakarta"
	      VIRTUAL_HOST: aplikasi.test
	      VIRTUAL_PORT: 80
	      LETSENCRYPT_HOST: aplikasi.test # this variable is for production and if you want to use letsencrypt as your SSL certificate authority, skip this variable for development
	      LETSENCRYPT_EMAIL: use_your_own_mail # this variable is for production and if you want to use letsencrypt as your SSL certificate authority, skip this variable for development
	```

2. for development, use this command to run the proxy container:

	```bash
	docker compose -f docker-compose.yml build --no-cache && docker compose -f docker-compose.yml up -d
	```


3. for production, use this command to run the proxy container:

	```bash
	docker compose -f docker-compose.yml -f docker-compose-prod.yml build --no-cache && docker compose -f docker-compose.yml -f docker-compose-prod.yml up -d
	```

