# Часть 1: Теория
1) [Основы docker](https://youtu.be/2LKrD8VRyg4)
2) [Docker Images](https://youtu.be/nKnmoJauQKw)
3) [Multistage Build; docker compose](https://youtu.be/W7ku22XUFUc)

# Часть 2: Практика
## Простые задачи (docker compose не требуется)
1) Запустить в docker приложение на python
```python
from flask import Flask
import sys
import os

app = Flask(__name__)

@app.route('/')
def index():
    python_version = sys.version
    current_directory = os.getcwd()
    return f"Версия Python: {python_version}\nТекущая директория: {current_directory}"

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```
Проверка
```bash
anestesia@projects-dev:~$ curl 127.0.0.1:5000
Версия Python: 3.9.2 (default, Mar 20 2025, 02:07:39)
[GCC 10.2.1 20210110]
Текущая директория: /home/anestesia/python
```
2) Запустить в docker приложение на golang
```golang
package main

import (
    "fmt"
    "log"
    "net/http"
    "time"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
    if r.URL.Path != "/" {
        http.Error(w, "404 Not Found", http.StatusNotFound)
        return
    }

    currentTime := time.Now().Format(time.RFC3339)
    greeting := "Hello!"

    fmt.Fprintf(w, "Current time: %s\n%s", currentTime, greeting)
}

func main() {
    http.HandleFunc("/", helloHandler)

    fmt.Println("Server started on 9100")
    log.Fatal(http.ListenAndServe(":9100", nil))
}
```
Проверка
```bash
anestesia@projects-dev:~/golang$ curl 127.0.0.1:9100/
Current time: 2025-04-12T03:22:10Z
Hello!
```
3) Запустить в docker приложение на nodejs
- server.js
```node
const http = require('http');
const os = require('os');
const childProcess = require('child_process');

const getNodeVersion = () => {
    return childProcess.execSync('node -v').toString().trim();
};

const getOSVersion = () => {
    return os.type() + ' ' + os.release();
};

const server = http.createServer((req, res) => {
    const nodeVersion = getNodeVersion();
    const osVersion = getOSVersion();

    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(`Версия Node.js: ${nodeVersion}\nВерсия ОС: ${osVersion}`);
});

server.listen(3000, () => {
    console.log('Сервер запущен на порту 3000');
});
```
- package.json
```json
{
  "name": "node-info-app",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "anestesia",
  "license": "ISC",
  "dependencies": {
    "express": "^4.21.1"
  },
  "scripts": {
	  "start": "node server.js"
  }
}
```
Проверка
```bash
anestesia@projects-dev:~/node-server$ curl 127.0.0.1:3002
Версия Node.js: v23.11.0
Версия ОС: Linux 5.10.0-19-amd64
```
## Средние задачи
1) Запустить с помощью docker compose приложение [counter](https://github.com/AnastasiyaGapochkina01/simple-visits-count-app)
2) Запустить с помощью docker compose приложение [cache](https://github.com/AnastasiyaGapochkina01/simple-cache-app)
3) Запустить с помощью docker compose приложение [autoshop manager](https://github.com/AnastasiyaGapochkina01/autoshop-manager-API)
