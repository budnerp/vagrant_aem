# Dev log
https://github.com/kmurugulla/aem-vagrant
https://tecadmin.net/install-oracle-java-8-ubuntu-via-ppa/

https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/project-setup.html

http://192.168.33.12:4502/system/console/slinglog

https://github.com/ksurendra/aem-as-a-service



## AEM manual, raw installation guide
Upload `AEM_6.5_Quickstart.jar` and `license.properties` into `/home/vagrant/`
```
cd /home/vagrant/ 
sudo mkdir /opt/aem
sudo mkdir /opt/aem/author
sudo mkdir /opt/aem/publish
sudo cp AEM_6.5_Quickstart.jar /opt/aem/author/aem-author-p4502.jar
sudo cp AEM_6.5_Quickstart.jar /opt/aem/publish/aem-publish-p4503.jar
sudo cp license.properties /opt/aem/author/
sudo cp license.properties /opt/aem/publish/
cd /opt/aem
sudo chown -R vagrant:vagrant .
sudo chmod -R 0777 .
ls -la
cd author
java -jar aem-author-p4502.jar -unpack
cd ../publish
java -jar aem-publish-p4503.jar -unpack
cd /
/opt/aem/author/crx-quickstart/bin/start
/opt/aem/publish/crx-quickstart/bin/start
```

wait and check in browser
 
Publish: http://192.168.33.12:4503/

Author: http://192.168.33.12:4502/

Credentials admin:admin
