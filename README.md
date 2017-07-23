## Notes: 

  
## Creating public folder  

```bash
app.use (express.stactic('app/public');
```
  
  
## Automation of workflow  

#### Auto Update the server
```bash
sudo npm install -g nodemon  
```

**Then server :  nodemon -e css,ejs,js,json --watch app**

```Note: In package.json=> "start":"nodemon app/app.js" => then HIT npm start```


#### Auto Update the page 
```bash
sudo npm install --save reload
```

Then in app.js, add at the top : 
```bash
var reload =require('reload');

reload (server,app);
```

In index.js and all the other routes at the end of the page:   
```bash 
<script src="/reload/reload.js"> </script>
```

#### Working with views (Installing a templating engine): 

```bash 
EJS (Embeddable Javascript)

app.set('view engine',???)
app.set('view',???)

```
Real code(Setting the templating engine):  
```bash
app.set('view engine','ejs');
app.set('view','app/views');
```
   
Hence, rendering index.js, ROUTES:   
```bash
router.get('/',function(req,res){
res.render ('index');     
});
```
  
```bash
res.render('index',{
	pageTitle: 'Home',
	pageID: 'home'
});  
```

**INCLUDING VARIABLE IN TEMPLATE**  
```bash
<title>ROux Meetup-- <%= pageTitle %></title>
<body id= "<%= pageTitle %>"> </body>
```
  
  
**Setting global varaibles :**  
```bash   
app.locals.siteTitle = 'Roux Meetups';
```
  
**Which Can Be Used As:**
```bash
 <title> <%= siteTitle %> </title>
```
  

### Conditionals and loops:    
  
#### Conditionals:    
<% if(typeof artwork !== "undefined") { %>
	<script src="/js/pixgrid.js"> </script>
<% } %>
```  
  
  
### ROUTER:  
```bash
router.get('/',function (req,res){
	var data =req.app.get('appData');
	var pagePhotos = [];

	res.render('index',{
		pageTitle: 'Home',
		pageID: 'home'
		});
});  
  
  
data.speakers.forEach(function(item){
	pagePhotos = pagePhotos.concat(item.artwork);
});

res.render('index',{
	pageTitle:'Home',
	artwork: pagePhotos,
	pageID: 'home'
});
```

In the view, 
```bash
<% if (artwork.length>0){
	for (i=0;i<artwork.length;i++){%>
	<img src="/images/artwork/<%= artwork[i]%>" alt="Artwork <%= i%>">
<%	}
%>
```
  

### Creating partials through includes (LAYOUTS):  
`views/partials/contents and template`
```bash 
<head><% include partials/template/head.ejs %></head>
```  


```bash 
<% speakers.forEach(function(item){ %>

// HTML stuff 
<h3 class="speakerslist-title"> <%= item.title %></h3>
	

});

```

#### Setting up a regular route:  
### Feedback (Route):
```bash
var express= require('express');
var router = express.Router();

router.get('/feedback', function(req,res){
	
	res.render('index',{
		pageTitle:'Feedback',
		pageID : 'home'
		});
});

module.exports = router; 
```
In app.js route:  
```bash
app.use(require('./routes/feedback'));
```

### Handling POST request:  
- verbs: GET, POST, DELETE, UPDATE
- POST: Send data
- Handle submit with jquery
- Use body-parser middleware (To handle formatting of the request)
- Use fs to save data permanently

```bash
var bodyParser = require ('body-parser');
var fs = require ('fs');


router.use(bodyParser.json());
router.use(bodyParser.urlencoded({extended: false}));

router.post('/api',function(req,res){
	feedbackdata.unshift(req.body);
	fs.writeFile('app/data/feedback.json',JSON.stringify(feedbackData),'utf8',function(err){
		console.log (err);
	});
	res.json(feedbackData);
});
```  

### Handling DELETE method:  
```bash
	router.delete('/api/:id',function(req,res){
		feedbackData.splice(req.params.id,1);
		fs.writeFile('app/data/feedback.json',JSON.stringify(feedbackData),'utf8',function(err){
			console.log(err);
		});
		res.json(feedbackData);
	});
```