# ahoyDTU-homeassistant-telegraf-influxdb-grafana

After having installed the home assisant OS, hassio, you can add addons via the settings.

Install mosquitto broker, influx, grafana and the file editor (for configuring yaml and config files)

Since hassio doesn't support telegraf offically, use https://github.com/sabuto/hassio-telegraf and follow his install instructions.

# Setting up Mqtt (mosquitto broker)

Make a new user in home assistant - for example mqtt-user (make sure the first option to login is checked)

Go to settings > devices and add the mqtt integration

Configure as shown below

<img width="472" alt="Bildschirmfoto 2023-08-03 um 08 29 59" src="https://github.com/RootLinus/ahoyDTU-homeassistant-telegraf-influxdb-grafana/assets/107202338/b5cff4e5-207b-4323-a609-09feb14675e7">

Now switch to Ahoy DTU > settings > mqtt

<img width="1244" alt="Bildschirmfoto 2023-08-03 um 08 33 30" src="https://github.com/RootLinus/ahoyDTU-homeassistant-telegraf-influxdb-grafana/assets/107202338/5a0a0494-ee49-41b6-938b-0c132db70dd4">

After executing send and saving the setting, listening for the topic # (all) should give outputs from ahoy DTU > mqtt

# Setting up Mqtt > Telegraf > Influxdb

Create a database and user in Influxdb (give user all permissions)

Edit the /config/configuration.yaml file with this repos file

Since the Telegraf Repo doesn't support any output to Influxdb, we'll have to add this functionality in a custom config file

Create one in for example /config/telegraf/telegraf.config

Copy paste the template from this repos telegraf.config file (just edit in your Database name, passwd, ip adress) and save

In home assistant > addon > telegraf > configure, make sure to enable custom config and give the right path

Start telegraf, switch to protocol to see errors (debug mode is true in the custom config)

As long as the right topic was given in the config file, output should be visible

The protocol should now look like this

<img width="837" alt="Bildschirmfoto 2023-08-03 um 08 54 49" src="https://github.com/RootLinus/ahoyDTU-homeassistant-telegraf-influxdb-grafana/assets/107202338/d4da432c-d99c-4a38-af18-0dd0fcf9289a">

By looking at the measurements and key fields in influxdb, you should now see the outputs that telegraf write

# Setting up Influxdb > Grafana

Under the left bar > Administration > data sources add a data source

Default URL is http://a0d7b954-influxdb:8086

Set Influxdb Database, User, Passwd

Set method to GET

Save and test

# By setting up a new Dashboard in Grafana, you should now be able to visualise all outputs from Ahoy DTU
