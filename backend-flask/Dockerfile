FROM python:3.10-slim-buster

# Inside Container 
# Make a new folder 
WORKDIR /backend-flask

# Outside Container -> Inside Container 
# this contains the libraries we want to install to run the app
COPY requirements.txt requirements.txt

#Inside Container 
#Install the python libraries used for the app 
RUN pip3 install -r requirements.txt

# Outside Container -> Inside Container 
# . (peroid) means everything in the current directory 
# . First peroid  /backend-flask(outside container)
# second peroid /backend-flask(inside container )
COPY . .

#Set Enviroment variables (env vars)
#Inside Container and will remain set when the container is running 
ENV FLASK_ENV=development

EXPOSE ${PORT}

#CMD(Command)
#python3 -m flask run --host=0.0.0.0 --port=4567
#"python3", "-m"(to use flask module) , "flask", "run", "--host=0.0.0.0", "--port=4567"
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
