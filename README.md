V1: 
    run celery worker:
    (venv)$ celery -A main.celery worker --loglevel=info

    send some tasks to the worker:
    (venv)$ python
    >>> from main import app, divide
    >>> task = divide.delay(1, 2)


    We used the delay method to send a new message to the message broker. The worker process then picked up and executed the task from the queue.
    After releasing from the Enter key, the code finished executing while the divide task ran in the background.

    After we called the delay method, we get an AsyncResult instance, which can be used to check the task state along with the return value or exception details.

    Add a new task then print task.state and task.result

    run flower:
    (venv)$ celery -A main.celery flower --port=5555
    Navigate to http://localhost:5555


V2:

project folder. __init__.py file . create_app function - factory function that returns FastAPI application for us.

main.py - create FastAPI app using the above function.

create_celery is a factory function that configures and then returns a Celery app instance.
Rather than creating a new Celery instance, we used current_app so that shared tasks will work as expected.