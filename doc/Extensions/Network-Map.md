source: Extensions/Network-Map.md
path: blob/master/doc/

# Network Map

LibreNMS has the ability to show you a network map based on:

- xDP Discovery
- MAC addresses

By default, both are are included but you can enable / disable either
one using the following config option:

```php
$config['network_map_items'] = array('mac','xdp');
```

Either remove mac or xdp depending on which you want.
XDP is based on FDP, CDP and LLDP support based on the device type.

A global map will be drawn from the information in the database, it is
worth noting that this could lead to a large network map. Network maps
for individual devices are available showing the relationship with
other devices. Also you can Build Device Groups and those Device
Groups can be drawn with Network Map.

# Network Map Configurator

This link will show you all the options and explain what they
do. [Link](https://visjs.github.io/vis-network/docs/network/)
You may also access the dyanamic configuration interface [example
here](https://visjs.github.io/vis-network/examples/network/other/configuration.html)
from within LibreNMS by adding the following to config.php

```php
$config['network_map_vis_options'] = '{
  "configure": { "enabled": true},
}';
```

## Note

You may want to disable the automatic page refresh while you're
tweaking your configuration, as the refresh will reset the dynamic
configuration UI to the values currently saved in config.php This can
be done by going clicking on the Settings Icon then Refresh Pause.

## Configurator Output

Once you've achieved your desired map appearance, click the generate
options button at the bottom to be given the necessary parameters to
add to your config.php file. You will need to paste the genrated
config into config.php the format will need to look something like
this. Note that the configuartor will output the config with `var options`
you will need strip that out and at the end of the config you need to
add in `}';` see the example below.

```php
$config['network_map_vis_options'] = '{
  "nodes": {
    "borderWidthSelected": null,
    "color": {
      "highlight": {},
      "hover": {}
    },
    "font": {
      "size": 24,
      "strokeWidth": null
    },
    "shapeProperties": {
      "borderRadius": null
    },
    "size": null
  },
  "edges": {
    "font": {
      "size": 19,
      "align": "top"
    },
    "smooth": {
      "forceDirection": "none"
    }
  },
  "physics": {
      "forceAtlas2Based": {
      "gravitationalConstant": -200,
      "centralGravity": 0.005,
      "springLength": 600,
      "springConstant": 0.09,
      "avoidOverlap": 0.29
    },
    "minVelocity": 0.92,
    "solver": "forceAtlas2Based"
  }
   
}';
```

![Example Network Map](/img/networkmap.png)
