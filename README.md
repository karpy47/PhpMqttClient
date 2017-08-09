# php-mqtt-client
MQTT 3.1.1 Client with TSL support in PHP

# Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

    php composer.phar require --prefer-dist karpy47/php-mqtt-client

or add

    "karpy47/php-mqtt-client": "*"

to the require section of your composer.json.

# Requirements

Should work with all recent PHP versions.

Code developed and running in production using PHP v5.6.27

Not tested on PHP v7, please report back!

# Basic Usage

    $client = new MQTTClient('mqtt-server.domain.com', 8162);
    $client->setAuthentication'mqtt-server.username','mqtt-server.password');
    $client->setEncryption('cacerts.pem');
    $success = $client->sendConnect(12345);  // set your client ID
    if ($success) {
        $client->sendSubscribe('topic1');
        $client->sendPublish('topic2');
        $messages = $client->getPublishMessages();
        foreach ($messages as $message) {
            echo $message['topic'] .': '. $message['message'] . PHP_EOL;
        }
        $client->sendDisconnect();    
    }
    $client->close();
    
# Credits

Thanks to bluerhinos/phpMQTT and McFizh/libMQTT.

# License

Released under the MIT License.
