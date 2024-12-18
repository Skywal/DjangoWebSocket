
## Start Redis container
docker run -it -d --rm --name redis -p 6379:6379 redis

# Check communication with redis layer

python manage.py shell

>>> import channels.layers
>>> from asgiref.sync import async_to_sync
>>> channel_layer = channels.layers.get_channel_layer()
>>> async_to_sync(channel_layer.send)('test_channel', {'message': 'hello'})  # send message to a test channel through the channel layer
>>> async_to_sync(channel_layer.receive)('test_channel')  # retrieve message from the channel layer

should see `{'message': 'hello'}`