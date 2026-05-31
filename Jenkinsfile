pipeline {
 agent {
 node {
 label 'dockerhost-build-server'
 }
 }
 tools {
 maven 'maven-3.9.6'
 }
 stages {
 stage('Packaging') {
 steps {
 echo 'Packaging..'
 sh 'mvn clean package'
 }
 }
 stage('Copying war file') {
 steps {
 echo 'Copying war file..'
 sh 'mv target/*.war .'
 }
 }
 stage('cleanup') {
 steps {
 sh 'docker system prune -a --volumes --force --filter "label=devops-web-projectserver"'
 }
 }
 stage('build image') {
 steps {
 sh 'docker build -t <nombre de usuario>/devops-web-project:v1 --label devops-webproject-server .'
 }
 }
 stage('run container') {
 steps {
 sh 'docker run -d --name devops-web-project-server --label devops-web-projectserver -p 8081:8080 <nombre de usuario>/devops-web-project:v1'
 }
 }
 }
 } 
