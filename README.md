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