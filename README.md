# Linux-FTP-Server_project
Linux FTP Server Project - Built and configured an FTP Server on Linux to upload and download files between client and server systems using IP-based communication. Configured user access, file permissions, and tested secure file transfer between multiple virtual machines in a Linux environment.

How to Configure FTP Server? 
# dnf install vsftpd -y 
# vim /etc/vsftpd/vsftpd.conf 
# Allow anonymous FTP? 
anonymous_enable=YES  -->      
anon_upload_enable=YES  -->      
:wq 
(to replace YES) 
(Uncomment this to allow the anonymous FTP user to upload files) 
# mkdir /var/ftp/{download,upload} 
# touch /var/ftp/download/foo.1.0.1-el10.x86_64.rpm 
# touch /var/ftp/download/bar.1.0.1-el10.x86_64.rpm 
# chown -R ftp:ftp /var/ftp/download 
# chmod –R 777 /var/ftp/upload 
# getsebool -a | grep ftp 
# setsebool -P ftpd_anon_write on 
# setsebool -P ftpd_full_access on 
# systemctl restart vsftpd 
# systemctl enable vsftpd 
# firewall-cmd --permanent --add-service=ftp 
# firewalld-cmd --reload ------------------------------------------------------------------------------------------------------------------------------------ 
FTP Client Access 
# dnf install ftp -y 
root@localhost:~# ftp 192.168.0.254 
Name (192.168.0.254:root): ftp 
Password: 
230 Login successful. 
ftp> ls 
drwxr-xr-x    2 14      
 50             
226 Directory send OK. 
ftp> cd download 
ftp> ls -rw-r--r--    1 14      -rw-r--r--    1 14      
 50              
 50              
226 Directory send OK. 
84 Feb 24 10:58 download 
0 Feb 24 10:50 foo.1.0.1-el10.x86_64.rpm 
0 Feb 24 10:50 bar.1.0.1-el10.x86_64.rpm 
ftp> get   foo.1.0.1-el10.x86_64.rpm                         
ftp> cd .. 
ftp> cd upload     
ftp > put /etc/hosts hosts       
ftp> bye                                      
(download file) 
(go-to upload directory) 
(upload file) 
(exit) 
