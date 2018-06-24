# PhPMqttClient
MQTT 3.1.1 Client with TSL support in PHP

Note that all calls are blocking until a timeout occurs. If you need some fancy async solution, you'll have to find another repo. 

This implementation works with [MQTT ver 3.1.1](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html) for QOS levels 0 and 1. QOS level 2 should work, but is experimental until better tested.

# Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

    php composer.phar require --prefer-dist karpy47/PhpMqttClient

or add

    "karpy47/PhpMqttClient": "*"

to the require section of your composer.json.

# Requirements

Should work with all recent PHP versions.

Code developed and running in production using PHP v7.0.27 (previously also PHP v5.6.27)

# Basic Usage

    $client = new MQTTClient('mqtt-server.domain.com', 8162);
    $client->setAuthentication('mqtt-server.username','mqtt-server.password');
    $client->setEncryption('cacerts.pem');
    $success = $client->sendConnect(12345);  // set your client ID
    if ($success) {
        $client->sendSubscribe('topic1');
        $client->sendPublish('topic2', 'Message to all subscribers of this topic');
        $messages = $client->getPublishMessages();  // now read and acknowledge all messages waiting
        foreach ($messages as $message) {
            echo $message['topic'] .': '. $message['message'] . PHP_EOL;
        }
        $client->sendDisconnect();    
    }
    $client->close();
    
# Credits

Thanks to [bluerhinos/phpMQTT](https://github.com/bluerhinos/phpMQTT) and [McFizh/libMQTT](https://github.com/McFizh/libMQTT).

# License

Released under the MIT License. Please see [License File](LICENSE) for more information.
