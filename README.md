#AMQP Pika Extension for Flask
This extension provides a simple way to expose an AMQP channel per request over a per thread connection to an AMQP server.

##Initializing the AMQP object
Simply initialize the AMQP instance with the app and a Pika connection params object.

	from flask import Flask
	from flask.ext.amqp import AMQP
	import pika

	app = Flask(__name__)
	amqp = AMQP()
	amqp.init_app(app, pika.ConnectionParameters(
							host='amqp host', //amqp.server.com
					 credentials=pika.PlainCredentials('username','password'), //username and password of amqp user
							port=5672, //amqp server port
					virtual_host='vhost' //amqp vhost
				))
	
##Using the AMQP object
Use the amqp object you created and get a channel.

	amqp.channel.basic_publish(exchange='exchange',routing_key='routing_key',body='message')
		
Flask AMQP will create a channel per request and take care of closing it for you on request end.