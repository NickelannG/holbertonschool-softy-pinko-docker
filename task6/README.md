6. Scale Horizontally


Congratulations! You’ve got a proxy server that routes to either a static-content server or to an API server for dynamic data. This works well, for now…but what would happen if traffic to your site spiked up dramatically to where your API server becomes too flooded with requests to be able to respond quickly? In this case, we would like to add a second API server and load-balance all requests between those two servers. Luckily, with Nginx and Docker, this is a simple flag when running docker-compose up!

For this task, make a copy of the task5 directory and name it task6. Your goal is to launch your Docker containers such that you have 2 (or more) API servers. Nginx will act as a load-balance between them so that every request goes to the next API server using the Round-Robin load-balancing algorithm.

Create a new file in the task6 directory named 2-api-servers.txt and put in the exact docker-compose command used to spin up two API servers, instead of just one. Note: for this task, the checker will assume that you named your back-end server back-end and your file must end with a newline Your output should look like this:


Terminal:
```
[+] Running 4/0
 ⠿ Container task6-back-end-2   Created                                                                                    0.0s
 ⠿ Container task6-back-end-1   Created                                                                                    0.0s
 ⠿ Container task6-front-end-1  Created                                                                                    0.0s
 ⠿ Container task6-proxy-1      Created                                                                                    0.0s
Attaching to task6-back-end-1, task6-back-end-2, task6-front-end-1, task6-proxy-1
task6-back-end-2   |  * Serving Flask app 'api'
task6-back-end-2   |  * Debug mode: off
task6-back-end-2   | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
task6-back-end-2   |  * Running on all addresses (0.0.0.0)
task6-back-end-2   |  * Running on http://127.0.0.1:5252
task6-back-end-2   |  * Running on http://172.20.0.2:5252
task6-back-end-2   | Press CTRL+C to quit
task6-back-end-1   |  * Serving Flask app 'api'
task6-back-end-1   |  * Debug mode: off
task6-back-end-1   | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
task6-back-end-1   |  * Running on all addresses (0.0.0.0)
task6-back-end-1   |  * Running on http://127.0.0.1:5252
task6-back-end-1   |  * Running on http://172.20.0.3:5252
task6-back-end-1   | Press CTRL+C to quit
task6-front-end-1  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
task6-front-end-1  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
task6-front-end-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
task6-front-end-1  | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
task6-front-end-1  | 10-listen-on-ipv6-by-default.sh: info: /etc/nginx/conf.d/default.conf differs from the packaged version
task6-front-end-1  | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
task6-front-end-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
task6-front-end-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
task6-front-end-1  | /docker-entrypoint.sh: Configuration complete; ready for start up
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: using the "epoll" event method
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: nginx/1.25.1
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: OS: Linux 5.15.49-linuxkit
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker processes
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 27
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 28
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 29
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 30
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 31
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 32
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 33
task6-front-end-1  | 2023/06/15 19:52:22 [notice] 1#1: start worker process 34
task6-proxy-1      | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
task6-proxy-1      | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
task6-proxy-1      | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
task6-proxy-1      | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
task6-proxy-1      | 10-listen-on-ipv6-by-default.sh: info: /etc/nginx/conf.d/default.conf differs from the packaged version
task6-proxy-1      | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
task6-proxy-1      | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
task6-proxy-1      | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
task6-proxy-1      | /docker-entrypoint.sh: Configuration complete; ready for start up
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: using the "epoll" event method
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: nginx/1.25.1
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: OS: Linux 5.15.49-linuxkit
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker processes
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 28
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 29
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 30
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 31
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 32
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 33
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 34
task6-proxy-1      | 2023/06/15 19:52:23 [notice] 1#1: start worker process 35
```

If you go to the web page and reload it several times, your terminal output should look like this:

Terminal:
```
task6-back-end-1   | 172.20.0.5 - - [15/Jun/2023 19:53:55] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.5 - - [15/Jun/2023 19:53:57] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.5 - - [15/Jun/2023 19:53:58] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.5 - - [15/Jun/2023 19:53:58] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.5 - - [15/Jun/2023 19:53:59] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.5 - - [15/Jun/2023 19:54:00] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.5 - - [15/Jun/2023 19:54:00] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.5 - - [15/Jun/2023 19:54:01] "GET /api/hello HTTP/1.0" 200 -
```

Note how the back-end server that the Nginx load-balancer routed to goes between the two different back-end servers. Here is an example with 5 back-end servers:

Terminal:
```
task6-back-end-2   | 172.20.0.8 - - [15/Jun/2023 19:55:21] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-5   | 172.20.0.8 - - [15/Jun/2023 19:55:22] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.8 - - [15/Jun/2023 19:55:23] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-4   | 172.20.0.8 - - [15/Jun/2023 19:55:23] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-3   | 172.20.0.8 - - [15/Jun/2023 19:55:24] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.8 - - [15/Jun/2023 19:55:24] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-5   | 172.20.0.8 - - [15/Jun/2023 19:55:24] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.8 - - [15/Jun/2023 19:55:25] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-4   | 172.20.0.8 - - [15/Jun/2023 19:55:25] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-3   | 172.20.0.8 - - [15/Jun/2023 19:55:26] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-2   | 172.20.0.8 - - [15/Jun/2023 19:55:26] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-5   | 172.20.0.8 - - [15/Jun/2023 19:55:27] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-1   | 172.20.0.8 - - [15/Jun/2023 19:55:27] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-4   | 172.20.0.8 - - [15/Jun/2023 19:55:27] "GET /api/hello HTTP/1.0" 200 -
task6-back-end-3   | 172.20.0.8 - - [15/Jun/2023 19:55:28] "GET /api/hello HTTP/1.0" 200 -
```