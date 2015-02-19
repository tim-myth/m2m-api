# m2m-api
This project provides API documentation and code samples for PeopleNet's M2M platform.

## API Documentation
See the [m2m-api wiki](https://github.com/PeopleNet/m2m-api/wiki) for API documentation.

## Sample Code
The m2m-api project contains sample MQTT publish and subscribe code.

### Java Sample
The Java sample code is located at [samples/java](samples/java).

The sample consists of an MQTT publisher and an MQTT subscriber application.

By default, the publisher application publishes five separate MQTT messages containing the current time to the topic *peoplenet/samples*.

The subscriber application subscribes to the same topic and prints the message contents to the console.

#### Running the Java Sample
To run the samples, first clone the project from github.
```
git clone https://github.com/PeopleNet/m2m-api.git
```
*Note, this requires git to be installed locally. If git is not installed on your system, it can be downloaded [here](http://git-scm.com/downloads).*

Next, from the samples/java/subscriber directory, run the following.
```
gradlew run
```
This will start the sample MQTT subscriber. The console should display a log similar to the following.
```
Feb 19, 2015 4:48:50 PM com.peoplenet.m2m.sample.subscriber.Subscriber init
INFO: Initializing MQTT subscriber...
Feb 19, 2015 4:48:50 PM com.peoplenet.m2m.sample.subscriber.Subscriber subscribe
INFO: MQTT connection established.
Feb 19, 2015 4:48:51 PM com.peoplenet.m2m.sample.subscriber.Subscriber subscribe
INFO: Successfully subscribed to Subscription [topic=peoplenet/samples, qos=AT_MOST_ONCE]
Feb 19, 2015 4:48:51 PM com.peoplenet.m2m.sample.subscriber.Subscriber waitForDelay
INFO: Waiting for messages until program termination.
```

Now, start the publisher to send messages. From the samples/java/publisher directory run the following.
```
gradlew run
```
The publisher console should log as follows.
```
Feb 19, 2015 4:53:11 PM com.peoplenet.m2m.sample.publisher.Publisher init
INFO: Initializing MQTT publisher.
Feb 19, 2015 4:53:11 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: MQTT connection established.
Feb 19, 2015 4:53:11 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Successfully published [Thu Feb 19 16:53:11 CST 2015] to [peoplenet/samples]
Feb 19, 2015 4:53:12 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Successfully published [Thu Feb 19 16:53:12 CST 2015] to [peoplenet/samples]
Feb 19, 2015 4:53:13 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Successfully published [Thu Feb 19 16:53:13 CST 2015] to [peoplenet/samples]
Feb 19, 2015 4:53:14 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Successfully published [Thu Feb 19 16:53:14 CST 2015] to [peoplenet/samples]
Feb 19, 2015 4:53:15 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Successfully published [Thu Feb 19 16:53:15 CST 2015] to [peoplenet/samples]
Feb 19, 2015 4:53:16 PM com.peoplenet.m2m.sample.publisher.Publisher publish
INFO: Publishing complete.
Feb 19, 2015 4:53:16 PM com.peoplenet.m2m.sample.publisher.Publisher shutdown
INFO: Publisher shutting down...
Feb 19, 2015 4:53:16 PM com.peoplenet.m2m.sample.publisher.Publisher shutdown
INFO: Publisher shutdown complete.
```
This displays each message that was sent from the publisher. Now, switching back to the subscriber's console, the output should look similar to the following.
```
Feb 19, 2015 4:53:11 PM com.peoplenet.m2m.sample.subscriber.Subscriber publishReceived
INFO: Received: Thu Feb 19 16:53:11 CST 2015
Feb 19, 2015 4:53:12 PM com.peoplenet.m2m.sample.subscriber.Subscriber publishReceived
INFO: Received: Thu Feb 19 16:53:12 CST 2015
Feb 19, 2015 4:53:13 PM com.peoplenet.m2m.sample.subscriber.Subscriber publishReceived
INFO: Received: Thu Feb 19 16:53:13 CST 2015
Feb 19, 2015 4:53:14 PM com.peoplenet.m2m.sample.subscriber.Subscriber publishReceived
INFO: Received: Thu Feb 19 16:53:14 CST 2015
Feb 19, 2015 4:53:15 PM com.peoplenet.m2m.sample.subscriber.Subscriber publishReceived
INFO: Received: Thu Feb 19 16:53:15 CST 2015
```
As you can see, the subscriber received five separate messages from the publisher.

To shutdown the consumer, simply use <ctrl-c> from the command line.

#### Java Sample Configuration
The publisher and subscriber are each configured via their own mqtt.properties file contained within the project.
* [samples/java/publisher/src/main/resources/mqtt.properties](samples/java/publisher/src/main/resources/mqtt.properties)
* [samples/java/subscriber/src/main/resources/mqtt.properties](samples/java/subscriber/src/main/resources/mqtt.properties).

##### Credentials
Note, the default *mqtt.properties* files are configured to use the freely available mosquito broker located at *test.mosquito.org*. Unlike the PeopleNet M2M broker, the mosquito broker does not require any security credentials.

##### ClientId
There is a chance for clientId conflicts using the default mqtt.properties. If you notice the clients being disconnected frequently it could be that you're conflicting with someone else using the same default clientId. In this case, feel free to update the clientId in each mqtt.properties file to be unique for your personal tests.
