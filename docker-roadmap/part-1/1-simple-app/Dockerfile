# video link : https://www.youtube.com/watch?v=fSmLiOMp2qI&ab_channel=HarkiratSingh

FROM node:20
#  this is the base image we are using for the application
# can be ubuntu , alpin , debian etc


WORKDIR /usr/src/app
# this is the path where the app is going to be installed 

COPY . .
#this copy all the source into the container from the directory where the docker file is

# left one shows what you want to copy and the right one shows where you want to copy.

RUN npm install
# you just copy the source code into the container not the node modules , so running this command is imp as it install the node modules and other dependencies and stuff 

EXPOSE 3000
#port which we want to expose for the container 

CMD ["node", "index.js"]
# this run when you run the container from the image , where as run is runned when the image is pulled or created .


# now to convert this dockerfile into an image , you runn the command 
# docker build . -t test-app 
# --> this command will create the image for the application and tag it as test-app

# now too use the container with the port on your local machine
# docker run -p 3000:3000 test-app
# this map the port of local machine to the port of the container

# command you should know after this 
# docker build . -t <tag_name>
# docker run <tag_name>
# docker login
# docker push <tag_name>
# docker pull <tag_name>

