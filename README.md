**winston-slack**

Winston Transport for Slack chat integration

Basic transport that works just like all other winston transports. Sends logged messages to a specified slack chat channel

Installation:

`$ npm install winston-slack`

Typical usage:

```
var winston = require('winston');
var logger = new( winston.Logger )({ //Winston setup
    transports: [
        new(winston.transports.Console)( {
                colorize: true,
                timestamp: true,
                json: true,
                prettyPrint: true,
                depth: 5,
                humanReadableUnhandledException: true,
                level: 'silly'
            } ),
        new( require('winston-slack').Slack )( {
                hookUrl: "https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX",
                username: "WinstonSlackBot",
                channel: "#yourchannel",
                icon_emoji: ':exclamation:',
                level: 'silly',
                handleExceptions : true,
            } )
    ]
});
```

**Required Options**

`hookUrl`: a Slack incoming webhook token (see. https://api.slack.com/incoming-webhooks/ )
`username`: name displayed in the chat channel. default "winston-slack"
`channel`: Channel the messages should show in

**Additonal options**

`icon_emoji:` Text WITH leading and trailing colon (see http://www.emoji-cheat-sheet.com/ )
`level`: Which logging levels should be sent (ignores lower levels)
`handleExceptions`: See https://github.com/winstonjs/winston#exceptions

You can also specify `customFormatter` as an option which takes 3 parameters and returns an updated message object. For example:

```
customFormatter: function( level, msg, meta ) {
    return { text: "_[" + level + "]_ *" + msg + '* ' + ( meta && Object.keys(meta).length != 0 ? ', JSON: ' + JSON.stringify(meta) : '' ),
                channel: winstonConfig.slack.channel,
                username: winstonConfig.slack.username
        }
}
```
