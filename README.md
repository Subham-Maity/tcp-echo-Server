# EXPERIMENT NAME:** TCP Echo server Programming using C/JAVA

**PROGRAM:  SERVER SIDE**
```
import java.net.\*;   import java.io.\*;

class MyServer1{

public static void main(String args[])throws IOException{

ServerSocket ss=new ServerSocket(3333);   System.out.println("Waiting for client");

Socket s=ss.accept();   System.out.println("Connection accepted"); System.out.println("Talk to client, stop to quit");

DataInputStream din=new DataInputStream(s.getInputStream());

DataOutputStream dout=new DataOutputStream(s.getOutputStream());

BufferedReader br=new BufferedReader(new InputStreamReader(System.in));

String str="",str2="";   while(!str.equals("stop")){

str=din.readUTF();   System.out.println("Client says: "+str);   str2=br.readLine();   dout.writeUTF(str2);

dout.flush();

}

din.close();   s.close();   ss.close();

}

}
```
**CLIENT SIDE**
```
import java.net.\*;

import java.io.\*;

class MyClient1{

public static void main(String args[])throws IOException{

Socket s=new Socket("localhost",3333);  System.out.println("Connected"); System.out.println("Talk to server, stop to quit");

DataInputStream din=new DataInputStream(s.getInputStream());

DataOutputStream dout=new DataOutputStream(s.getOutputStream());

BufferedReader br=new BufferedReader(new InputStreamReader(System.in));

String str="",str2="";   while(!str.equals("stop")){

str=br.readLine();

dout.writeUTF(str);

dout.flush();

str2=din.readUTF();

System.out.println("Server says: "+str2);   }

dout.close();   s.close();

}

}
```
==================================== C programming =====================================

**SOURCE CODE:**

**SERVER:**
```
#include<stdio.h>

#include<netinet/in.h>

#include<netdb.h>

#define SERV\_TCP\_PORT 5035

int main(int argc,char\*\*argv)

{

int sockfd,newsockfd,clength;

struct sockaddr\_in serv\_addr,cli\_addr;

char buffer[4096];

sockfd=socket(AF\_INET,SOCK\_STREAM,0); serv\_addr.sin\_family=AF\_INET; serv\_addr.sin\_addr.s\_addr=INADDR\_ANY; serv\_addr.sin\_port=htons(SERV\_TCP\_PORT);

printf("\nStart");

bind(sockfd,(struct sockaddr\*)&serv\_addr,sizeof(serv\_addr)); printf("\nListening...");

printf("\n");

listen(sockfd,5);

clength=sizeof(cli\_addr);

newsockfd=accept(sockfd,(struct sockaddr\*)&cli\_addr,&clength); printf("\nAccepted");

printf("\n");

read(newsockfd,buffer,4096);

printf("\nClient message:%s",buffer); write(newsockfd,buffer,4096);

printf("\n"); close(sockfd); return 0;

}
```
**CLIENT:**
```
#include<stdio.h>

#include<sys/types.h>

#include<sys/socket.h>

#include<netinet/in.h>

#include<netdb.h>

#define SERV\_TCP\_PORT 5035

int main(int argc,char\*argv[])

{

int sockfd;

struct sockaddr\_in serv\_addr;

struct hostent \*server;

char buffer[4096];

sockfd=socket(AF\_INET,SOCK\_STREAM,0); serv\_addr.sin\_family=AF\_INET; serv\_addr.sin\_addr.s\_addr=inet\_addr("127.0.0.1"); serv\_addr.sin\_port=htons(SERV\_TCP\_PORT);

printf("\nReady for sending...");

connect(sockfd,(struct sockaddr\*)&serv\_addr,sizeof(serv\_addr)); printf("\nEnter the message to send\n");

printf("\nClient: ");

fgets(buffer,4096,stdin);

write(sockfd,buffer,4096);

printf("Serverecho:%s",buffer);

printf("\n");

close(sockfd);

return 0;

} 
```