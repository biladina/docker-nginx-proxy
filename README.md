## DEVELOPMENT ONLY
1. you can create your own local domain, and if you need https support, use this site to create custom SSL certificate for your local domain: [https://regery.com/en/security/ssl-tools/self-signed-certificate-generator](https://regery.com/en/security/ssl-tools/self-signed-certificate-generator)

2. from step no. 1 you need two things, domain SSL certificate and domain private key. Make sure you rename them using your local domain, example:

	```
	// your domain is: aplikasi.test
	aplikasi.test.crt // this file is for domain SSL certificate
	aplikasi.test.key // this file is for domain private key
	```

3. if you already run this project, you can stop the container by run this command:
	
	```
	docker stop nginx-proxy
	docker stop nginx-gen
	```

4. you can copy the .crt and .key file to `certs` directory

5. after you copy the .crt and .key file, if you already run this project, you can start again the container by run this command:
	
	```
	docker start nginx-proxy
	docker start nginx-gen
	```

6. if you never run this project before, go to [RUN PROJECT](#run-project)



## RUN PROJECT
1. create docker network with name `nginx-proxy`

	```
	docker network create -d bridge
	```

2. for development, use this command to run the proxy container:

	```
	docker compose -f docker-compose.yml build --no-cache && docker compose -f docker-compose.yml up -d
	```


3. for production, use this command to run the proxy container:

	```
	docker compose -f docker-compose.yml -f docker-compose-prod.yml build --no-cache && docker compose -f docker-compose.yml -f docker-compose-prod.yml up -d
	```

