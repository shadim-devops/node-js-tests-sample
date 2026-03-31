# Jenkins Docker Agents

## Description
Jenkins integrated with Docker to run pipelines using dynamic agents.

## Stages
1. System Info  
2. Check ENV  

## Features
- dynamic Docker agents  
- automatic container creation  
- pipeline execution in container  
- auto cleanup after job  

## Configuration
- Docker API: tcp://192.168.229.150:4243  
- Image: jenkins/inbound-agent  
- Label: docker-agent  

## Result
Pipeline executed successfully inside Docker container.