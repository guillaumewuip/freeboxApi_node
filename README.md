freeboxApi_node
===============

A NodeJS module for the new Freebox OS API.

Please read also the doc : http://dev.freebox.fr/sdk/os.

*Please consider it as a draft.*

Start
------

```
  var freebox = require('./freebox/freebox'); 

  freebox.connect();
  
  freebox.on('ready', function(box) {
  
    //Some stuff
  
  });
```


Declare the app to the Freebox
------------------------------
Before doing anything, you need to declare the app to the Freebox. A message will be prompt on the lcd screnn asking the user to accept or deny.

```freebox.register();```

On can save app_token, track_id and status by listening at :

```freebox.on('registered', function(params) {
  console.log(params);
});```


Downloads
--------- 

