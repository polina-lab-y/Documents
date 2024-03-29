# Documents
Test for Semrush
# Create and deploy of image
 For run docker container with ExampleApp on Kubernetes’s cluster follow next steps:
1. Configure port for receiver of requests: port 8800.
2. Create structure of directories and subdirectories:
  *	mkdir quickstart_docker
  *	mkdir quickstart_docker/application
  *	mkdir quickstart_docker/docker
  *	mkdir quickstart_docker/docker/application  
  
quickstart_docker/ # Catalog of project  
├──application/ # Code of application  
└──docker/ # content for Docker  
      └──application/ # location of Dockerfile for app 

3.	Create script for deploy of application.  
Application.py:  
   import http.server  
   import socketserver  
   PORT = 8000  
   Handler = http.server.SimpleHTTPRequestHandler  
   httpd = socketserver.TCPServer((&quot;&quot;, PORT), Handler)  
   print(&quot;serving at port&quot;, PORT)  
   httpd.serve_forever() 
4.	Put file «application.py» to directory «quickstart_docker/application/»:  
    
> **Note**. For script is need Python Virtual Environment and relevant OS. More information [here](http://https://hub.docker.com/)
5.	Create file «Dockerfile»:  
\# Use base image from the registry  
FROM python:3.5  
\# Set the working directory to /app  
WORKDIR /app  
\# Copy the &#39;application&#39; directory contents into the container at /app  
COPY ./application /app  
\# Make port 8000 available to the world outside this container  
EXPOSE 8000  
\# Execute &#39;python /app/application.py&#39; when container launches  
CMD [&quot;python&quot;, &quot;/app/application.py&quot;] 
6. Put file «Dockerfile» to directory «quickstart_docker/application/».  
7.	Open Terminal program. Execute command «docker build . -f-docker/application/Dockerfile -t exampleapp». 
 **Decryption of arguments for "docker build":**
* .- working directory, build context;
* -f docker/application/Dockerfile - Dockerfile;
* -t exampleapp – teg of image for search.
> **Note**. About build images for Docker Hub [read here](http://docs.docker.com/engine/reference/builder/)
8.	List images:  
$ docker images

| REPOSITORY     | TAG        | IMAGE ID     | CREATED       | SIZE    |
| :------------- | ---------: | -----------: | ------------: |:-------:|
| exampleapp     | latest     | 83wse0edc28a | 2 seconds ago | 153MB   |
| python         | 3.6        | 05sob8636w3f | 6 weeks ago   | 153MB   |


9.	Push an image to repository.
