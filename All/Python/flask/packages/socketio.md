# Socket IO

9/24/23 requires 3.6+

```bash
pip install flask-socketio
pip install eventlet #seems to just use it if installed
```

### Setup

```python
from flask import Flask, render_template
from flask_socketio import SocketIO

app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret!'
socketio = SocketIO(app)

if __name__ == '__main__':
    socketio.run(app)
```

In factories can do

```python
socketio = SocketIO()
# then
socketio.init_app(app, cors_allowed_origins="*")
```

In other folder

- If no namespace, uses global namespace
- 'message' and 'json' special events to listen to for unnamed events
  - Use `send` for these sepcial events and `emit` for custom

```python
from flask import session
from flask_socketio import send, emit, join_room, leave_room
from app.extensions import socketio

@socketio.on('connect')
def test_connect(auth):
    emit('my response', {'data': 'Connected'})

@socketio.on('disconnect')
def test_disconnect():
    print('Client disconnected')

@socketio.on('my event', namespace='/test')
def handle_my_custom_namespace_event(json):
    print('received json: ' + str(json))
    
@socketio.on('message')
def handle_message(message):
    send(message)

@socketio.on('json')
def handle_json(json):
    send(json, json=True)

def ack():
    print('message was received!')

#default emits on namespace
@socketio.on('my event', namespace='/test')
def handle_my_custom_event(json):
    emit('my response', json, callback=ack, broadcast=True)    
    
@socketio.on('my event2')
def handle_my_custom_event2(json):
    emit('my response', ('foo', 'bar', json), namespace='/chat')
```

### Rooms

- all clients auto join a room with their `request.sid` name 

```python
from flask_socketio import join_room, leave_room

@socketio.on('join')
def on_join(data):
    username = data['username']
    room = data['room']
    join_room(room)
    send(username + ' has entered the room.', to=room)

@socketio.on('leave')
def on_leave(data):
    username = data['username']
    room = data['room']
    leave_room(room)
    send(username + ' has left the room.', to=room)
```



Send messages from a background function

```python
def some_function():
    socketio.emit('some event', {'data': 42})
```

