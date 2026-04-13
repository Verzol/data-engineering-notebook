# image base ma Dockerfile se build theo
FROM ubuntu

# working directory
WORKDIR /src

# install python
RUN apt-get update
RUN apt-get -y install python3

# install python libraries
RUN apt-get -y install python3-sklearn

# copy python file
COPY iris_classification.py ./iris_classification.py

# run python file
CMD ["python3", "iris_classification.py"]