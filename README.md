# homeworkit-nginx-docker-compose-python-localip

HomeWork IT :
1. Create a private repo on github.
2. Create an app.py (web app) that prints the local IP to the browser (on HTTP - port 80).
3. Create a load balancer based on a docker nginx image exposed on port 9090.
4. Create a docker compose that runs 3 instances of the app you created + the load
balancer.
5. Open browser and check http://localhost:9090, verify you see different IP each refresh.

app.py:

import redis
from flask import Flask
import socket

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

hostname=socket.gethostname()   
IPAddr=socket.gethostbyname(hostname) 

@app.route('/')
def ip():
    ip= IPAddr
    return 'My Local IP Address {}' .format(ip)

if __name__ == '__main__':
    app.run(host="0.0.0.0",port=80,debug=True,threaded=True)

