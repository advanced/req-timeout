req-timeout
===========

set , reset and clear request timeout for connect and express

Usage
-----

req-timeout is a middleware so you need to add it in your chain.

```javascript
var express = require('express'),
    timeOut = require('req-timeout'), 
    app = express();
    
// timeout the request at 1 seconds
app.configure('development',function(){
  app.use(timeOut(1000));
});

// timeout the request at 3 seconds
app.configure('production',function(){
  app.use(timeOut(3000));
});

app.use(app.router);

app.get('/slow',function(req,res){
  setTimeout(function(){
    res.send('too slow to actually matter, I will timeout');  
  },3500);
})

app.get('/fast',function(req,res){
  res.send('should be AOK');
})

app.get('/reset', function(req,res) {
  req.resetTimeOut(4000)
	setTimeout(function() {
		res.send('should be OK, my time has been extended');
	}, 3500);
})

app.get('/clear', function(req,res) {
	req.clearTimeout()
	setTimeout(function() {
		res.send('should be OK, timeout has been cleared');
	}, 3500);
})

app.listen(3000);
```
