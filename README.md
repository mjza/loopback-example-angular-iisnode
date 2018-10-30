# loopback-example-angular-iisnode

Loopback is a grate library. But if you want to use it inside a Windows host like Azur that have `iisnode` as their `Node.JS` engine, then you will be faced with so many problems. In this code which is a fork from offical [loopback-example-angular](https://github.com/strongloop/loopback-example-angular) I will try to show you how to run this example inside the windows host.
My host controll panel is the `Pleks Onyx`. Also My explanation will be reflected after the offical read me text that explanes how to use this code in your local machin.

# A) How to run offical `loopback-example-angular` in your local machine. 

```
$ git clone https://github.com/strongloop/loopback-example-angular.git
$ cd loopback-example-angular
$ npm install
$ node . # then browse to localhost:3000
```

A simple todo list using AngularJS on the client-side and LoopBack on the
server-side.

## Prerequisites

### Tutorials

- [Getting started with LoopBack](https://github.com/strongloop/loopback-getting-started)
- [Tutorial series, step 1](https://github.com/strongloop/loopback-example#the-basics)

### Knowledge of

- [Angular](https://angularjs.org/)
- [Angular Resource](https://docs.angularjs.org/api/ngResource/service/$resource)
- [AngularUI Router](https://github.com/angular-ui/ui-router)
- [Bootstrap](http://getbootstrap.com/)
- [Bower](http://bower.io/)
- [LoopBack](http://loopback.io/)
- [LoopBack AngularJS SDK](http://loopback.io/doc/en/lb2/AngularJS-JavaScript-SDK.html)
- [LoopBack models](http://loopback.io/doc/en/lb2/Defining-models.html)
- [LoopBack middleware](http://loopback.io/doc/en/lb2/Defining-middleware.html)

## Procedure

### Create the application

#### Application information

- Name: `loopback-example-angular`
- Directory to contain the project: `loopback-example-angular`

```
$ slc loopback loopback-example-angular
... # follow the prompts
$ cd loopback-example-angular
```

### Create the `Todo` model

#### Model information

- Name: `Todo`
  - Data source: `db (memory)`
  - Base class: `PersistedModel`
  - Expose over REST: `Yes`
  - Custom plural form: *Leave blank*
  - Properties:
    - `content`
      - String
      - Required

```
$ slc loopback:model Todo
... # follow the prompts
```

### Configure the vendor directory

In the project root, create [`.bowerrc`](https://github.com/strongloop/loopback-example-angular/blob/master/.bowerrc).

>Bower installs packages in `bower_components` by default, but we reconfigure
this to `client/vendor` to make [importing files into `index.html`](https://github.com/strongloop/loopback-example-angular/blob/master/client/index.html#L33-L37)
more convenient.

### Install client-side dependencies

From the project root, run:

```
$ bower install angular angular-resource angular-ui-router bootstrap
```

### Create the home page

Create [`index.html`](https://github.com/strongloop/loopback-example-angular/blob/master/client/index.html) in the [`client`](https://github.com/strongloop/loopback-example-angular/blob/master/client) directory.

### Create the main stylesheet

Create a [`css` directory](https://github.com/strongloop/loopback-example-angular/blob/master/client/css) to store stylesheets.

```
$ mkdir client/css
```

In this directory, create [`styles.css`](https://github.com/strongloop/loopback-example-angular/blob/master/client/css/styles.css).

### Serve static assets from the `client` directory

Delete `/server/boot/root.js`.

Add static middleware to the [`files` section in `middleware.json`](https://github.com/strongloop/loopback-example-angular/blob/master/server/middleware.json#L23-L27)
.

### Create `app.js`

Create a [`js` directory](https://github.com/strongloop/loopback-example-angular/blob/master/client/js) to hold scripts files.

```
$ mkdir client/js
```

In this directory, create [`app.js`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/app.js).

>Notice we declare [`lbServices`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/app.js#L3) as a dependency. We
will generate this file using the `lb-ng` command in a later step.

### Create `todo.html`

Create a [`views`](https://github.com/strongloop/loopback-example-angular/blob/master/client/views) to store view templates.

```
$ mkdir client/views
```

In this directory, create [`todo.html`](https://github.com/strongloop/loopback-example-angular/blob/master/client/views/todo.html).

### Create `controllers.js`

Create a [`controllers`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/controllers) directory to store controller
files.

```
$ mkdir client/js/controllers
```

In this directory, create [`todo.js`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/controllers/todo.js).

### Generate `lb-services.js`

Create a [`services` directory](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/services) to store service files.

```
$ mkdir client/js/services
```

`lb-ng` is automatically installed along with the `slc` command-line tool (ie.
when you ran `npm install -g strongloop`). `lb-ng` takes two arguments: the
path to [`server.js`](https://github.com/strongloop/loopback-example-angular/blob/master/server/server.js) and the path
to the [generated services file](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/services/lb-services.js).
[`lb-services.js`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/services/lb-services.js) is an Angular service
used to interact with LoopBack models.

Create [`lb-services.js`](https://github.com/strongloop/loopback-example-angular/blob/master/client/js/services/lb-services.js) using the `lb-ng`
command.

```
$ lb-ng server/server.js client/js/services/lb-services.js
```

### Run the application

From the project root, enter `node .` and browse to [`localhost:3000`](http://localhost:3000)
to view the application.

---

[More LoopBack examples](https://loopback.io/doc/en/lb3/Tutorials-and-examples.html)

---

# B) How to deploy `loopback-example-angular` to our remote production host which has `iisnode`???

Uptil now what ever you red was original text from the official `loopback-example-angular` example code. From now I will try to explain how to deploy this code to a remote host for your end users.

You don't need to fork or clone my code. Just keep it beside of your code for comparision. 

I will illustrate from very bigining, this toturial is based on `Pleks Onyx` control panel, but the configuration can be used for any other iisnode like Microsoft Azur as well.

![Create the website space](./figures/01.JPG)
      
![Initial files](./figures/02.JPG)

![content of web.config file](./figures/03.JPG)

![Delete redundant files](./figures/04.JPG)

![Upload and extract files](./figures/05.JPG)

![List of extracted files. Delete original zip file.](./figures/06.JPG)

![Activate Node.js on the site.](./figures/07.JPG)

![run NPM install on the site](./figures/08.JPG)

![You must see the success message.](./figures/09.JPG)

![Content of node_module after installation](./figures/10.JPG)

![The error page that can be seen before fix.](./figures/11.JPG)

![Content of start.js file](./figures/12.JPG)

![Change the `Application start file address` and start the node.js again](./figures/13.JPG)

![Looklike of the page after adding start.js file to the root folder.](./figures/14.JPG)

![Looklike of the page after changing the web.config file at the root folder.](./figures/15.JPG)

![Success REST POST request](./figures/16.JPG)

![Success REST DELETE request](./figures/17.JPG)







