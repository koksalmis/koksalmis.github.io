---
layout: post
title:  "How to make your own L4(TCP) Load Balancer?"
date:   2021-05-23 00:00:58 +0300
categories: jekyll update
---

Hi Everyone,

Today, I would like to write about Load Balancers. I will give a brief info about it like "What is it?", "What is used for?", "Types of Load Balancers(HTTP(L7), TCP(L4))" etc. Then we will make our Load Balancer in JAVA.

Firstly, What is Load Balancer? Load Balancer is a software, sometimes is a hardware to balance requests among your servers. Why we need? Imagine you have user.com and behind that website you have 4 servers. Let's say Server A, Server B, Server C, Server D. If all request goes to Server A, Server A may not serve to all request because it has limited CPU, Memory etc. So, to protect and optimize our resources we need a solution to balance requests which is load among our servers. Also, With Load Balancers we hide our servers from clients. This is a basic and fundamental reason why we need. But also there are other reasons like hiding your actually servers, security reasons etc. For more info I suggest [citrix's document](https://www.citrix.com/solutions/app-delivery-and-security/load-balancing/what-is-load-balancing.html#:~:text=Load%20balancing%20is%20defined%20as,server%20capable%20of%20fulfilling%20them.).

![Load Balancer]({{ "/assets/loadbalancer/loadbalancer.png" | absolute_url }})

So, we know what is Load Balancer but how it works? How it balance requests among our servers? What are load balancing algorithms? Here is the list of common load balancing algorithms;
* Round Robin
* Least Connection
* Adaptive(CPU/Memory)

In this blogpost I will show you Load Balancer which is impelemented Round Robin algorithm.

In Round Robin algorithm our load balancer will route each requests one by one to our actually servers in order. For example if we have 4 Servers(Server A, Server B, Server C and Server D). Our load balancer will route first request to Server A, second request to Server B, third request to Server C and fourth request to server D and repeat again that order.

So to do that I created a method that implements round robin algorithm to choose backed adress ports like below;

In this implementation, lets say all websites serves in localhost but different ports so I defined ports (Our Servers). Then when a requests come to load balancer, our load balancer route that requests to port which calculated in chooseBackendPort method. With this calculation requests will be routed same order like Server A, Server B, Server C, Server D.

```
public static int[] ports = new int[]{ 5001,5002,5003,5004 };

```

```
    public int chooseBackendPort() {
        //Round Robin
        int port = ports[(counter%ports.length)];
        System.out.printf("Counter is: %d, Chosed localhost:%d\n",counter,port);
        counter++;
        return port;
    }
```
So far, we implemented our load balancer's routing strategy. Now we need a server(in this case our load balancer) that accepts requests, open a connection to actual server, send bytes to that server and read bytes from that server. To impelement this flow we use [java.net](https://docs.oracle.com/javase/8/docs/api/java/net/package-summary.html) like below;

* Open a ServerSocket port 8080 to listen requests
* When a requests come, chooseBackendPorts, then open a connection with chosed port
* Copy incoming request's inputStream to openned connection's outputStream (Send Request)
* Copy openned connection's inputStream to incoming request's outputStream (Read Response)

```
import org.apache.commons.io.IOUtils;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.net.SocketTimeoutException;


public class LoadBalancer extends Thread {

    private ServerSocket serverSocket; // Creates a server socket to listen 
    public static int[] ports = new int[]{5001,5002,5003,5004};
    private int counter;

    public LoadBalancer(int port) throws IOException {
        serverSocket = new ServerSocket(port);
    }
    public void run() {
        while(true) {
            try {
                System.out.println("Waiting for client on port " +
                        serverSocket.getLocalPort() + "...");
                Socket server = serverSocket.accept(); // If a requests come to server it accepts
                proxy(chooseBackendPort(),server); // with out routing strategy we route request to chosed backend servers

            } catch (SocketTimeoutException s) {
                System.out.println("Socket timed out!");
                break;
            } catch (IOException e) {
                e.printStackTrace();
                break;
            }
        }
    }

    public int chooseBackendPort() {
        //Round Robin
        int port = ports[(counter%ports.length)];
        System.out.printf("Counter is: %d, Chosed localhost:%d\n",counter,port);
        counter++;
        return port;
    }

    public void proxy(int backendPort, Socket socket) throws IOException {
        Socket newSocket = new Socket("localhost", backendPort);
        Thread thread = new Thread(){
            public void run(){
                try {
                    IOUtils.copy(socket.getInputStream(),newSocket.getOutputStream()); // Send Request
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        thread.start();
        Thread threadForOppositeDirection = new Thread(){
            public void run(){
                try {
                    IOUtils.copy(newSocket.getInputStream(),socket.getOutputStream()); // Read Response
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        };
        threadForOppositeDirection.start();
    }
}
```
As you can see in ``` proxy ``` method we create 2 thread to copy(via apache [IOUtils](https://commons.apache.org/proper/commons-io/apidocs/org/apache/commons/io/IOUtils.html)) bytes from load balancer to chosed backend server and vice versa to send requests and read responses.


Now we can test our load balancer, to test it I created 4 simple HTTP Server then I start my load balancer and run command below several times and watch how requests routed to backend servers. Here is a short demo video.
```
curl localhost:8080
```

[![IMAGE ALT TEXT](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/BJc4qExn2Sc "L4(TCP) Load Balancer")


Thank You.
Enes Köksalmış

