# ansible_demo  
ansible Test from Docker  

## forkey(create public、private Key)  
docker build -t keygen-container .  
#mount current folder in windows cmd to get public、private Key in comtainer ~/.ssh/  
docker run -it --rm -v %cd%:/key keygen-container:1.0 /bin/sh  
cp ~/.ssh/* /key  
#copy public Key to build_ansible_client folder  
#copy public、private Key to build_ansible_alpine folder 
  
#if you don't want use forkey so you can use command in docker-compose after docker-compose up -d   
docker exec -it compose_master_1 /bin/sh   
#in  container use command  
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@nod1  
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@nod2  
  
## build_ansible_alpine(ansible control)  
docker build -t ansible/control:1.0 .  
  
## build_ansible_client(ansible remote client)  
docker build --build-arg PASSWORD=P@ssw0rd -t ansible/client:1.0 .  
  
## compose(docker-compose)  
#must be in this folder use the command  
docker-compose up -d  
  
#if you want close  
docker-compose down  
  
## commanf.txt  
this is a comment some command  
