# Electron #
Basically, a stand-alone web page.



## How to get started from scratch ##
1. Install npm
2. In your new project's folder, run `npm init`
3. Create a new file in project root directory called 'package.json' and add the following to it:

        {
          "name"    : "my-app",
          "version" : "0.1.0",
          "main"    : "main.js"
        }

4. Create a different new file in the project root directory called 'main.js', add the following:

        var app = require('app');  // Module to control application life.
        var BrowserWindow = require('browser-window');  // Module to create native browser window.

        // Report crashes to our server.
        require('crash-reporter').start();

        // Keep a global reference of the window object, if you don't, the window will
        // be closed automatically when the JavaScript object is GCed.
        var mainWindow = null;

        // Quit when all windows are closed.
        app.on('window-all-closed', function() {
          // On OS X it is common for applications and their menu bar
          // to stay active until the user quits explicitly with Cmd + Q
          if (process.platform != 'darwin') {
            app.quit();
          }
        });

        // This method will be called when Electron has finished
        // initialization and is ready to create browser windows.
        app.on('ready', function() {
          // Create the browser window.
          mainWindow = new BrowserWindow({width: 800, height: 600});

          // and load the index.html of the app.
          mainWindow.loadUrl('file://' + __dirname + '/index.html'); //__

          // Open the devtools.
          mainWindow.openDevTools();

          // Emitted when the window is closed.
          mainWindow.on('closed', function() {
            // Dereference the window object, usually you would store windows
            // in an array if your app supports multi windows, this is the time
            // when you should delete the corresponding element.
            mainWindow = null;
          });
        });

5. Create one last file in the project root directory called 'index.html' with the following code:

        <!DOCTYPE html>
        <html>
          <head>
            <title>Hello World!</title>
          </head>
          <body>
            <h1 align="center">Hello World!</h1>
            We are using io.js <script>document.write(process.version)</script>
            and Electron <script>document.write(process.versions['electron'])</script>.
          </body>
        </html>

6. Now that the three files are created, run `./node-modules/.bin/electron .` (note the space and period at the end)


### How to have an 'easier' start ###
If you would just like to run 'npm start' to run your project, then add the following code to your 'package.json'. Make sure it keeps the valid JSON format.

    "scripts": {
      "start": "electron ."
    }



## Electron snippets ##

###  Create a menu ###

    var remote = require('remote') // Needed when off the main process.
    var ipc = require('ipc')
    var Menu = require('menu')

    var menu = Menu.buildFromTemplate([]
      {
        label: 'My App Name',
        submenu: [
          {
            label: 'My Prefs',
            click: function() {
              ipc.send('show-prefs')
            }
          }
        ]
      }
    ])

    // In main.js's app.on('ready', ...)
    var prefsWindow = new BrowserWindow({
      width: 400,
      height: 400,
      show: false
    })
    prefsWindow.loadUrl('file://' + __dirname + '/prefs.html') //__

    // Also in main.js
    var ipc = require('ipc')
    ipc.on('show-prefs', function() {
      prefsWindow.show();
    })

More info, including hiding the extra window: [Multi Window Electron Desktop Apps](https://www.youtube.com/watch?v=K-H2amwQ_pU)


### Packaging and Distributing Electron Desktop Apps ###
[More info](https://www.youtube.com/watch?v=dz5SnmBzBXc)

Windows still not prime-time yet. - 2015-05-05

1. Run `npm install electron-packager` --save-dev



## JavaScript snippets ##

### Read a file ###

    var fs = require('fs')
    var contents = fs.readFileSync('./package.json', 'utf8')
    alert(contents)



## Further Resources ##
- [Official Electron site](http://electron.atom.io/)
- [GitHub: Electron Sample Apps](https://github.com/hokein/electron-sample-apps)

### Example Usage ###
- [Mancy](http://www.mancy-re.pl/): "Cross platform JavaScript REPL application based on Electron and React"
