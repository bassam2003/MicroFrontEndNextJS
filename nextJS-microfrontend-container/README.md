
To run this project type:

### `yarn start`

Runs the app .<br />
Open [http://localhost:3000] to view it in the browser.

### `yarn test`

Launches the test runner in the interactive watch mode.<br />

### `yarn build`

Builds the app 

Strategy

Before developing we have to let the container app know about the microfrontends. We used .env file to maintain the list of microfrontends.
All the microfrontends will run on different ports at the localhost. We used the following ports.
1. Container App: Port 3000
2. App1: Port 3001
3. App2: Port 3002
2. App3: Port 3003
3. App4: Port 3004
The .env file in the container app root level has the following content.

APP1_HOST=http://localhost:3001
APP2_HOST=http://localhost:3002
APP3_HOST=http://localhost:3003
APP4_HOST=http://localhost:3004

Sharing components between repositories is a big challenge.
We used Container app approach. I have developed the MessageApp1,  MessageApp2, MessageApp3, MessageApp4 components. 
The objective of this component is to listen to the message parameter and generate a result accordingly.

The Container app must know how to add microfrontends to the relevant section of the app.
Lets define the entry point and how to discover apps. We can use the asset-manifest.json created by the build scripts.

Main.js build scripts that will bundle the entire application. Render function and unmount function.
Render function name: render{AppName}
Unmount function name: unmount{AppName}


This MicroFrontend the component takes name, host as params. It will fetch the asset-manifest.json from the host and create a script object using the main.js file. Then use the render function to mount component.
App.js use this component to mount app1, app2, app3, and app4.
It reads the app servers form .env file, create several components using microfrontends, and render the routes.