# Hosting a Node.js Server Example

## Overview

This example is designed to help you get familiarized with running Node.js on a BrightSign player. It demonstrates how to run a simple Node.js server directly on the player. Additionally, it introduces tools and configurations that go beyond the basics covered in starter examples.

The core Node.js application is defined in `app.js`, which uses a BrightSign-specific library to retrieve and log device information. Alongside the JavaScript code, you'll find the `autorun.brs` file, which instructs the player to execute the bundled application.

## Building and Running the Application

### Step 1: Install Dependencies
Ensure that Node.js is installed on your machine. From your project directory, install the necessary dependencies by running the following command:

```bash
npm install
```

Next, build and bundle the application:

```bash
npm run build
```

### Step 2: Transfer Files to the Player

#### Manual Transfer
After the application is bundled, you need to transfer the required files to your BrightSign player:
- Copy the `bundle.js` file from the `dist` directory.
- Place the `bundle.js` file in the `dist` directory and the `autorun.brs` file at the root of the SD card.
- Insert the SD card into the player.

#### Automated Transfer Using Provided Bash Scripts
The BrightSign bash script(s) are contained in the `scripts/` directory. Follow the steps below to deploy built code to your player. 

Set the following environment variables:
```sh
export PLAYER="<IP address or hostname of the player>"
# e.g. export PLAYER="192.168.86.1"

# only needed when ldws password is set
export PLAYER_PW="<password, which is the serial number by default>"
# e.g. export PLAYER_PW="abcd"
```

To actually put code on your player:
```sh
npm run cp
```

If you are confident the code will compile with webpack, you can combine building the app and deploying the app with:
```sh
npm run put
```

If you are not confident the code will compile with webpack, you should first build the app separately and check for any errors:
```sh
npm run build
```

After ensuring the build is successful, you can then deploy the app:
```sh
npm run cp
```

Or to deploy the development version of your code:
```sh
npm run put:dev
```

### Step 3: Access the Server
Once the player is running, you can access the Node.js server from a web browser. Make sure your computer is connected to the same network as the BrightSign player. In the browser, navigate to the player’s IP address using port 13131 (as configured in `app.js`):

```
http://<player-ip>:13131
```

You should now be able to view the server’s output and interact with the Node.js application running on the player.

## Testing and mocking

This example is equipped with basic mocking to make testing easier with local development. In the `__mocks__` directory, there is a `deviceinfo.js` file which defines mock values when the application is run in a development environment.
To run the test(s) located in `App.test.js`, execute the following:
```bash
npm run test
```