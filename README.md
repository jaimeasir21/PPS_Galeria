# Galeria

Aplicación de ejemplo para usar en práctica Deploy de contenedor Docker en EC2 AWS.

- Crear entrono virtual e Instalar dependencias
```
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip install -r requirements.txt 
```
- Lanzar la aplicación en local (por defecto puerto 5000)

    ```console
    (venv) $ python src/app.py 
    * Serving Flask app 'app'
    * Debug mode: on
    WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
    * Running on http://127.0.0.1:5000
    Press CTRL+C to quit
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 944-294-141
    127.0.0.1 - - [13/Feb/2023 10:30:32] "GET / HTTP/1.1" 200 -
    127.0.0.1 - - [13/Feb/2023 10:30:32] "GET /static/estilos.css HTTP/1.1" 304 -
    ...
    ``` 

- Parar la aplciación y lanzar la aplicación en local con `gunicorn` (por defecto puerto 8000, en otro puerto usar `--bind 0.0.0.0:5000`)

    ```console
    (venv) $ gunicorn --chdir src app:app --bind 0.0.0.0:5000
    [2023-02-13 10:32:50 +0100] [3863] [INFO] Starting gunicorn 20.1.0
    [2023-02-13 10:32:50 +0100] [3863] [INFO] Listening at: http://0.0.0.0:5000 (3863)
    [2023-02-13 10:32:50 +0100] [3863] [INFO] Using worker: sync
    [2023-02-13 10:32:50 +0100] [3864] [INFO] Booting worker with pid: 3864
    ```

- Crear una imagen con la aplicación  y lanzar container

    ```console
    $ docker build -t user_docker/testing .
    $ docker run -d p 80:5000  user_docker/testing
    $ curl localhost:80
    $ firefox localhost &
    ``` 

- Si diera error al hacer build de la imagen por problemas de red

    ```console
    systemctl restart NetworkManager.service
    sudo service docker restart
    ``` 



