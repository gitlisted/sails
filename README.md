![image_devInTub@2x.png](http://i.imgur.com/Tj9Nk.png) 

# Sails
Sails makes it easy to build custom, enterprise-grade Node.js apps. It is designed to resemble the MVC architecture from frameworks like Ruby on Rails, but with support for the more modern, data-oriented style of web app development.  It's especially good for building realtime features like chat.


# Installation

To install the latest stable release with the command-line tool:
```sh
sudo npm -g install sails
```


# Creating a New Sails Project

Create a new app
```sh
# Create the app
sails new testProject
```

Lift Sails
```sh
# cd into the new folder
cd testProject

# Fire up the server  
sails lift
```

The default port for Sails is 1337.  At this point if you visit <a href="http://localhost:1337/">http://localhost:1337/</a> You will see
the default index.html page.  Now, let's get Sails to tell us Hello.


# Hello, Sails!
To get Sails to say "Hello World!", you need only to define one controller with an action and define
one route. Lets start with the controller.

```sh
sails generate controller hello index
```

This will generate a file called `HelloController.js` in your app's `api/controllers` directory with one action, `index()`.

Now let's edit that action to send back the string `'Hello World!'`.

```javascript

var HelloController = {

	index: function(req, res) {
		res.send('Hello World!');
	}
}

module.exports = HelloController;
```

After you have added that, you will want to remove the default index.html page that shows at the
start of your application.

```sh
rm ui/public/index.html
```

We want the application to display this hello response when a request for the root "/" route
comes in. Go into the **/config/routes.js** file. Here you can manually define these mappings,
and here we will do so. Change the file to look like this.

```javascript
var routes = {
	'/': {
		controller: 'hello',
		action: 'index'
	}
}

module.exports = routes;
```

As you will see when working more with Sails, one great feature is that by default, you do not have
to define incoming routes to controller actions. This is talked more about in the 
<a href="https://github.com/balderdashy/sails/wiki/Routing">Routing page</a> of this wiki.

Finally, restart the server by going to your node terminal and pressing control+c. Then enter the
following.

```sh
sails lift
```

Now when you visit <a href="http://localhost:1337/">http://localhost:1337/</a> your browser should say **'Hello World!'**.


# Creating a Model
Creating a model is very easy with the command line tool. You can even define attributes and their
type by adding arguments at the end of the command. To generate a User model, enter the following:
```
sails generate model User
```

You will see that this creates a user model at **/api/model/User.js**.  Let's give her a name-- try uncommenting the name attribute so it looks more or less like this:

```javascript
var User = {
        attributes      : {
                name: 'STRING'
        }

};
module.exports = User;
```

# What's Better Than Scaffolding?  How About a free JSON API?

Sails API scaffolding is nothing like Rails scaffolding. HTML scaffolds just don't make sense for 
modern web apps! Instead, Sails automatically builds a RESTful JSON API for your models. Best of
all, it supports HTTP _and_ WebSockets! By default for every controller you create, you get the
basic CRUD operations created automatically.

For instance, after generating the User model above, if you visit `http://localhost:1337/user/create`, you'll see:
```json
{
  "createdAt": "2013-01-10T01:33:19.105Z",
  "updatedAt": "2013-01-10T01:33:19.105Z",
  "id": 1
}
```

That's it!  You just created a model in the database!  You can also `find`, `update`, and `destroy` users:

```
# List of all users
http://localhost:1337/user

# Find the user with id 1
http://localhost:1337/user/1

# Create a new user
http://localhost:1337/user/create?name=Fisslewick
(or send an HTTP POST to http://localhost:1337/user)

# Update the name of the user with id 1
http://localhost:1337/user/update/1?name=Gordo
(or send an HTTP PUT to http://localhost:1337/user/1)

# Destroy the user with id 1
http://localhost:1337/user/destroy/1
(or send an HTTP DELETE to http://localhost:1337/user/1)
```


## Additional Features
Sails does a few things other Node.js MVC frameworks can't do:
- Automatically generated JSON API for manipulating models means you don't have to write any backend code to build simple database apps
- Built-in authentication, role-based access control, and customizable policies assignable at the controller/action level
- Transport agnostic routing: Sails controllers also handle Socket.io / WebSocket messages!  This makes it much easier to send the server-originated or 'comet' notifications you need for features like chat, realtime analytics, and multiplayer games.
- Automatic asset minification with Rigging: Your UI code is automatically included in development mode, and minified into a simple, gzipped file in production.
  - Support for:
    - CoffeeScript
    - LESS
    - SASS / SCSS


To learn more, check out the documentation here: 
https://github.com/balderdashy/sails/wiki/_pages



Dependencies and Compatibility
--

Tested with node 0.8.1
Sails is built on the rock-solid foundations of ExpressJS and Socket.io.  







![icon_circlechart@2x.png](http://i.imgur.com/hXc06.png) 

Demo
--

*Try it in two browser windows*

http://sailsjs.com:1337/experiment#subcomponents

<!--
#### Code
https://github.com/balderdashy/sails-example
-->










![icon_circleheart@2x.png](http://i.imgur.com/liHPV.png) 
## Who Built This?

The Sails framework was developed by Mike McNeil (@mikermcneil) and is maintained by Balderdash (@balderdashy), a realtime web & mobile studio I started with Heather White (@hdesignsit) in Austin, TX.

After building a few realtime javascript apps and taking them into production, we realized that the  JavaScript development landscape is very much still the Wild West.  Over time, after trying lots of different methodologies (on the front end and the back), we decided to crystallize all of our best practices into this framework.  I hope it saves you some time :)







![icon_circlelightbulb@2x.png](http://i.imgur.com/eOFXn.png)  

License
--

Sails is built around so many great open-source technologies that it would never have crossed our minds to keep it proprietary.  We owe huge gratitude and props to TJ Holowaychuk (@visionmedia) and Guillermo Rauch (@guille) for the work they did, as well as the stewards of all the other open-source modules we use.  Sails could never have been developed without your tremendous contributions to the node community.


The MIT License (MIT)
--

Copyright © 2012-2013 Mike McNeil

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/8acf2fc2ca0aca8a3018e355ad776ed7 "githalytics.com")](http://githalytics.com/balderdashy/sails)
