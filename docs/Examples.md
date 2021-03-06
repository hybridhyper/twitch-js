# Examples

## Browser

1.  Add the following to your HTML:
    ```html
    <script src="https://unpkg.com/twitch-js@1.2.5/dist/twitch-js.min.js" />
    ```
2.  Include the following JavaScript:
    ```js
    // To get started with this example, specify a channel with which to connect.
    const channel = 'schmoopiie';

    // In this example, TwitchJS is included via a <script /> tag, so we can access
    // the library from window.
    const TwitchJS = window.TwitchJS;

    // Define client options.
    var options = {
      options: {
        // Debugging information will be outputted to the console.
        debug: true
      },
      connection: {
        reconnect: true,
        secure: true
      },
      // If you want to connect as a certain user, provide an identity here:
      // identity: {
      //   username: 'Schmoopiie',
      //   password: 'oauth:a29b68aede41e25179a66c5978b21437',
      // },
      channels: [`#${channel}`]
    };

    const client = new TwitchJS.client(options);

    // Add listeners for events, e.g. a chat event.
    client.on('chat', (channel, userstate, message, self) => {
      // You can do something with the chat message here ...
      console.info({ channel, userstate, message, self });
    });

    // Finally, connect to the Twitch channel.
    client.connect();
    ```
To see this code in action, see this [Codesandbox](https://codesandbox.io/s/z24j801k2p).

## Node

1.  Add TwitchJS to your project:
    ```bash
    npm install --save twitch-js
    ```
2.  Include the following JavaScript:
    ```js
    // Require the TwitchJS library.
    const TwitchJS = require('twitch-js');

    // Setup the client with your configuration; more details here:
    // https://github.com/twitch-apis/twitch-js/blob/master/docs/Chat/Configuration.md
    const options = {
      channels: ["#isak_"],
      // Provide an identity
      // identity: {
      //   username: "Isak_",
      //   password: "oauth:a29b68aede41e25179a66c5978b21437"
      // },
    };

    const client = new TwitchJS.client(options);

    // Add chat event listener that will respond to "!command" messages with:
    // "Hello world!".
    client.on('chat', (channel, userstate, message, self) => {
      console
        .log(`Message "${message}" received from ${userstate['display-name']}`);

      // Do not repond if the message is from the connected identity.
      if (self) return;

      if (options.identity && message === '!command') {
        // If an identity was provided, respond in channel with message.
        client.say(channel, 'Hello world!');
     }
    });

    // Finally, connect to the channel
    client.connect();
    ```
To see this code in action, see this [RunKit](https://npm.runkit.com/twitch-js).