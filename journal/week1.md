# Week 1 — App Containerization


Journal Entry: Homework Summary and Learning Docker Fundamentals

Summary:

During this week's homework, I learned about various aspects of Docker and virtual machines. I watched all the YouTube videos and quizzes and learned about container images and their use case by asking ChatGPT. ChatGPT provided an interesting analogy of giving a friend a special cake who lives far away. I also asked ChatGPT about the difference between container image registry and artifacts, which was covered in the video. Additionally, I completed the homework, which involved creating a Dockerfile in backend-flash and adding the Docker extension to Gitpod. I overcame issues with Dockerfile compose.

Challenges:

To gain more knowledge, I watched the Docker 101 fundamental course, installed Docker on my local machine, and pushed the image to Docker Hub with a tag name. I also reviewed the best practices for Dockerfile development from the official documentation. Finally, I learned how to install Docker on my local machine and run the same containers outside of Gitpod.

In-Depth Summary:

I learned about the difference between physical servers and virtual machines, which is important when learning Docker with the fundamental course. Physical servers are 100% owned and managed by the user, and any failures are their own responsibility. Physical servers consist of various components such as the motherboard, CPU, memory, storage, GPUs, and add-on cards. Sizing is the main issue for physical servers because their capacity can affect the system's overall performance.

Here is the diagram from Cantrill's docker fundamental course that gives a breakdown on physical servers : 


![872AC114-A3B2-4285-803D-B3B19F6763F8](https://user-images.githubusercontent.com/70730021/222311466-62e622b8-fa0c-4d6f-bae7-2bcc89f64af8.jpeg)




Virtual machines, on the other hand, are a better approach as they allow users to do more by carving up the physical capacity, allowing more VMs to run on the same physical hardware. VMs are managed by a hypervisor that manages the physical resources within a server. Hypervisors act as the middleman to access the VM host capacity. VMs can vary in size and have their own dedicated resources so that they never go over 100% of the physical hardware. They are different in that they own their operating system, self-contained, and allocated resources and do not impact other VMs.


Here is the diagram from Cantrill's docker fundamental course that gives a breakdown on Virtual Machines/servers : 

![BD39C920-63CF-4D95-8336-B13631110ADC](https://user-images.githubusercontent.com/70730021/222311633-6855aa8c-3a0c-442d-b4ab-56aaac854455.jpeg)



Containers were made to fix application shipping issues, where a developer developed an application in their personal computer, but when they try to deploy it in production, it does not work. Containers help ship the computer via Container (Docker) Engine. Containers run on a container host and only run an APP/Libraries/Runtime. They share the container HOST OS and can be impacted by other containers (noisy neighbors).

Here is the diagram from Cantrill's docker fundamental course that gives a breakdown on Containers Architecture :

![41B810C2-1A26-4310-A0AA-C914E9176C5C](https://user-images.githubusercontent.com/70730021/222311848-ee894c84-22e3-43cf-878a-fbfecbb870c0.jpeg)


I also learned about the different components of the Docker architecture, such as Docker Engine, Docker Daemon, Docker Client (CLI and Desktop), Docker Registry, and Docker Images. Images are used to run containers. For example, if you want to run an application, you need an image that has that application, as well as libraries it uses and runtime environments. To download images, we need to pull them from Docker images, and we can create them using the Docker build command.

Here is the diagram from Cantrill's docker fundamental course that gives a breakdown on Docker Architecture :

![E788A88B-D144-4E76-85C6-FA187E584D4D](https://user-images.githubusercontent.com/70730021/222312010-c4467c82-71e1-48b6-8347-078ac58e28cc.jpeg)

- Docker Engine is like a client-server application.
- It starts with a Docker host that runs the Docker daemon.
- The Docker daemon is the brain of the Docker platform.
- It is the server part that provides API access to be able to interact with it.
- Docker client, such as the CLI and Desktop, is how we access the API.
- Docker Registry is a public/private storage for images, such as Docker Hub.
- Docker images are used to run containers.
- Images have the application, libraries, and runtime environments needed to run.
- To download images, we need to pull them from Docker images.
- We can create images using the docker build command.
- Containers are created from images and are the running instances of an image.


During the first week's video, I asked ChatGPT what a container image was and why we would use it. They explained it to me as if I were a little kid, and it made it easier to understand. I also asked ChatGPT about the difference between image registry and artifacts.

ChatGPT's Response to what a cotainer iamge was why we would use it as if i was little kid 
![57A5AB74-E4BF-4F81-B480-BE5D0A5C9F47](https://user-images.githubusercontent.com/70730021/222312671-9e9279d3-2c7c-4c78-a4fe-0314faef0c5b.jpeg)

ChatGPT's Response to what the difference between container image registry vs artifacts 

![A4D9E2ED-C892-4189-BD02-9D24DDC76748](https://user-images.githubusercontent.com/70730021/222313093-b2621b62-aaaf-4d85-9365-2c1bb5c205c9.jpeg)



Lastly, we created a Dockerfile in backend-flask and added the Docker extension to Gitpod. We learned that the Docker extension can be used to manage Docker images and containers within VS Code. We also learned about the Open API extension, which can be used to see APIs that we might not be able to see. Before starting the Dockerfile compose file, we needed to npm I to install all the dependencies.

Here is where I added the Docker File in the backend-flask 

![FAD3CA08-59D2-4B74-BA87-928B2B68093C](https://user-images.githubusercontent.com/70730021/222313306-ccc8b7bd-a6f3-437f-a553-55fa62332d84.jpeg)


Here is the code we used below :


``` 

# This contains the libraries we want to install to run the app
COPY requirements.txt requirements.txt

#Inside Container 
#Install the python libraries used for the app 
RUN pip3 install -r requirements.txt

# Outside Container -> Inside Container 
# . (period) means everything in the current directory 
# . First period /backend-flask(outside container)
# second period /backend-flask(inside container )
COPY. .

#Set Environment variables (env vars)
#Inside Container and will remain set when the container is running 
ENV FLASK_ENV=development

EXPOSE ${PORT}

#CMD(Command)
#python3 -m flask run --host=0.0.0.0 --port=4567
#"python3", "-m"(to use flask module), "flask", "run", "--host=0.0.0.0", "--port=4567"
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]


``` 

- We can view our Docker images that were built with the "latest" tag (since no specific tag was specified) for our application as shown in image below . The Docker extension allows us to view both images and containers.


![6FC8E112-94C7-471A-A277-69CCB754B845](https://user-images.githubusercontent.com/70730021/222314501-fe85a081-76a4-4212-aabf-c8c2d63d54d3.jpeg)


With the Docker Extension we can view the logs which tells us the start of our docker image in Gitpod


![2A59FFC8-2512-4651-9FF6-1D32F3413A04](https://user-images.githubusercontent.com/70730021/222315267-af91da6c-662d-4722-835c-3f344f3056b2.jpeg)

As well we can attach the shell with our docker extension in Gitpod which means we are inside the container as shown below 

![CAA67087-2AB7-485B-8DB2-812C7A5FFEF1](https://user-images.githubusercontent.com/70730021/222315731-63bc2469-c741-4e1f-afab-243a4c33da53.jpeg)

Set the backend and frontend enivroment as shown 

![CBAE2DE5-36F9-43BE-BB4F-372E18A799CA](https://user-images.githubusercontent.com/70730021/222316230-6a3d4017-aab6-43ab-9f97-bc0cb823eecf.jpeg)


![F7C18228-103D-497B-B144-9379D4D45BE9](https://user-images.githubusercontent.com/70730021/222316303-3124bdc2-fa8e-4a13-ac9e-874aceac30d3.jpeg)


Here is where I used the OPEN API extension which we are able to see the scheme of the API as shown below 


![B79FC16D-EA52-4FA6-8394-D0047C6FC852](https://user-images.githubusercontent.com/70730021/222316674-531e1da5-f58d-4bcc-a3be-78d299f05714.jpeg)

For my homework challenge I did build the front-end image into dockerhub using the Docker Extension with tag as Front-end . Here are the steps : 

First, I created an account in Docker Hub. Then, I ran the following command to build the front-end image with a customized image:

```
docker build --pull --rm -f "frontend-react-js/Dockerfile" -t awsbootcampcr/uddur2023:front-end "frontend-react-js"

```


The front-end image with the custom tag (front-end) has been successfully uploaded to the Docker Hub Registry, and we can see the results here.




![7C0917B1-27D6-4D07-9328-359E2909987A_1_105_c](https://user-images.githubusercontent.com/70730021/222319200-d345f55d-2610-408e-9f38-59729c1dcc76.jpeg)


![68861C47-E0D8-4489-9BE4-05BE7B7335B1_1_105_c](https://user-images.githubusercontent.com/70730021/222319257-bbd56d2d-1e19-451b-9d1b-b49572efe955.jpeg)



This was my attempt to run the containers outside of Gitpod 


![24112E20-E649-4E5F-A52C-EDC0E8B28FA1_1_105_c](https://user-images.githubusercontent.com/70730021/222319394-df717300-fb43-4257-a206-4d5efde23376.jpeg)


Contianer running after attemp as seen in Docker Desktop 

![9D443BF8-65FC-4497-894A-CC8A140F3EAE_1_105_c](https://user-images.githubusercontent.com/70730021/222319470-6d385df8-6af5-4aee-804b-2e91b38f9dfc.jpeg)


Learned that in Docker Desktop we are able to see the logs of our container as seen below 


![FD276DEA-7879-4C78-87CD-C99DA962FCD8_1_105_c](https://user-images.githubusercontent.com/70730021/222319555-c4898927-592c-4ff6-a4a9-81fd7364d7c5.jpeg)


I have already learned so much from this course, and I am looking forward to improving my journaling skills to better document my future learnings. 

Until next time,

Jasmin
