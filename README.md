# Task-M-
Creating Vm using Command line and using start up scripts in it 

Metadata is "data that provides information about other data",[1] but not the content of the data, such as the text of a message or the image itself. There are many distinct types of metadata, including


What is matadata in GCE? 
Google Cloud Platform provides a metadata server that knows details about your App Engine instance, such as its containing project ID, service accounts, and tokens used by the service accounts. You can access this data using simple HTTP requests: no client libraries are required.

Why it's is used in GCE? 
The metadata server provides information about a VMs scheduling option through the scheduling/ metadata directory entry and the maintenance-event attribute. You can use these metadata values to notify you when a maintenance event is about to happen so that you can prepare your environment for the event.

What is a startup script?? 
A startup script is a file that performs tasks during the startup process of a virtual machine (VM) instance. Startup scripts can apply to all VMs in a project or to a single VM. Startup scripts specified by VM-level metadata override startup scripts specified by project-level metadata, and startup scripts only run when a network is available. This document describes how to use startup scripts on Linux VM instances. For information about how to add a project-level startup script, see gcloud compute project-info add-metadata.


While creating an instances through the command line we can develope the equivalent command line from the GCP console. While developing we have to enter the start up script to udate the system. 
The script is as follows in the bin bash :


#! /bin/bash![IMG-20211008-WA0006](https://user-images.githubusercontent.com/92073589/136561305-7d61526d-3934-443c-97c7-b07b56584188.jpg)

 apt update
 apt -y install apache2
 cat <<EOF > /var/www/html/index.html
 <html><body><p>Linux startup script added directly.</p></body></html>

This will update the system instance while creating the instance through command line. 
Then while creating the instance we can add on  more scripts to make them vm more flexible. 
Like for example we can delete, stop, create, start the instance from there itself. For that a startup script is needed. The script is as follows :
![IMG-20211008-WA0006](https://user-images.githubusercontent.com/92073589/136561114-0cb4fe59-6936-43a1-a94d-0c8e9508b0b1.jpg)

#!/bin/bash
var='please enter your choice'
options= ("opt1-Delete" "opt2-Stop" "opt3-start" "quit")
select opt in "${options[@]}"
do
case $opt in
"opt1-Delete")
echo "choose 1"
gcloud compute instances delete ayan
echo "your instance is deleted"

"opt2-Stop")
echo "choose 2"
gcloud compute instances stop ayan
echo "instance stopped"
;;
"opt3-start")
echo "choose 3"
gcloud compute instances start ayan
echo "instance started"
;;
"quit")
break
;;
*)echo "invaild option";;
esac
done
![Screenshot_2021-10-07-20-22-51-052_cn wps moffice_eng](https://user-images.githubusercontent.com/92073589/136562691-b9d975b9-6a25-480d-aa97-d27ace42a6fb.jpg)


This script will create the following options in the instance like to delete, stop, start, create a particular instance.
