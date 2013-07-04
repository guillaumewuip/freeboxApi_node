FreeboxOS Api - NodeJS module
===============

A NodeJS module for the new FreeboxOS API.

Please read also the doc : http://dev.freebox.fr/sdk/os.

*Please consider it as a draft.*

freebox.connect();
------
You can start to use the module with these lines of code :

```
  var freebox = require('./freebox/freebox'); 

  freebox.connect();
  
  freebox.on('ready', function(box) {
  
    //Some stuff
  
  });
  
```

You could also pass params. For example if you want to specifiy the address of the box, or if you alredy have an app_token for your app.

```
freebox.connect({
  'ip'        : 'mafreebox.freebox.fr', (optional)
  'port'      : 80, (optional)
  'app_token' : '012345', (optional)
  'track_id'  : '12' (optional)
});
```


freebox.register();
------------------------------
Before doing anything, you need to declare the app to the Freebox. A message will be prompt on the lcd screen asking the user to accept or deny.

```
freebox.register();
```

On can save appToken, trackId and status by listening at :

```
freebox.on('registered', function(params) {
  console.log(params);
});
```

Stats
-------
### freebox.stats(db, date_start, date_end, precision, fields, next)
Echo freebox's stats. Example :
```
freebox.stats(temp, null, null, null, null, function(msg) {
  console.log(msg);
});
```
date_start, date_end, precision and fields are optional.
Please see http://dev.freebox.fr/sdk/os/rrd/ for all the options.

Downloads
--------- 

### freebox.downloadsStats(next)
Echo download stats with :
```
freebox.downloadsStats(function(msg){
  console.log(msg);
});
```

### addDownloads(url, dir, recursive, username, password, archive_password, next)

'Url' can be multiple. In this case, they have to be separated by a new line delimiter "\n" as below.
```
freebox.addDownloads(
  "http://blog.baillet.eu/public/ciel-bleu-sans-avion-20100417-imgis5346.jpg\nhttp://www.8alamaison.com/wp-content/uploads/2013/04/z2354-carton-rouge3.gif",
  null, false, null, null, null,
  function(msg) {
    console.log(msg);
  }
 );
```

### downloads(id, action, params, next)
You can manage download.   
With no id submitted it returns the entire downloads list.
With an id you can manage the selected download.

Actions :
- read (default)
- log
- udpate (needs 'params', see below)
- delete
- deleteAndErase (delete the download and erase the files downloaded)   

```
freebox.downloads(2, udpate, {"io_priority": "high","status": "stopped"}, function(msg){
  console.log(msg);
});
```

Calls
-----
### freebox.calls(next);
Return all the calls save in the box.
```
freebox.calls(function(msg){
  console.log(msg);
});
```

### freebox.call(id, action, params, next)
Manage a call.
Actions :
- Read (default)
- update
- delete

Example : read a specific call
```
freebox.call(1, 'read', null, function(msg) {
  console.log(msg);
});
```
Example : update a call :
```
freebox.call(1, 'update', {'new' : false}, function(msg) {
  console.log(msg);
});
```







