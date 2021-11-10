# discticket

Discord-Ticket is an npm package who allows you to create a perfectly working ticket system with buttons!.

## Installation

Use [node.js](https://nodejs.org/it/download/) to install discticket

```bash
npm install discticket
```

## Usage

```javascript
const discord = require('discord.js')
const client = new discord.Client({intents: [discord.Intents.FLAGS.GUILDS, discord.Intents.FLAGS.GUILD_MESSAGES]});
const { Ticket, TicketInteraction } = require('discticket')


client.on('messageCreate', async message => {
    if(message.author.bot) return;    

    if(message.content.startsWith('!deployticket')) {

    //here you can put whatever you want, I suggest making a permission filter
    const ticketembed = new Ticket({
        client: client,
        channel:client.channels.cache.get("CHANNEL ID"), //id of the channel where the ticket create embed should get sent
        configuration: {
            title: "Support Ticket", //default: Ticket Support
            description: "Press for support.", //default: Press the emoji to open a ticket
            buttonName: "Open Ticket", //default: Open Ticket
            color: "BLURPLE", //default: BLACK
            footer: "Powered by distickets", //default: Powered by discord-ticket
            openEmoji: "📖" //default: 📖
        }
      })

      ticketembed.create()

}})

client.on('interactionCreate', async interaction => {

    const ticketinter = new TicketInteraction({
        interaction: interaction,
        configuration: {
            openTitle: "Ticket Opened!", //default: Ticket Support
            openFooter: "powered by distickets",
            openDesc: `${interaction.user}, wait for a moderator to come!`, //default: Wait for a staffer
            openCategory: "ticket category id", //default: no one
            openColor: "BLURPLE", //default: BLACK
            ticketOpenTitle: "ERROR", //default = ERROR
            ticketOpenDescription: "You already have a ticket opened!", //default: You already have a ticket opened!
            ticketOpenFooter: `${interaction.guild.name}`, //default: server's name
            ticketOpenColor: "BLURPLE", //default: BLACK
            roleView: "role id", //id of the role allowed to see the tickets. 
            closeTitle: `Closing Ticket`, //default: CLosing Ticket
            closeDesc: `Ticket will close in 10s`, //adjust to match with closeTime
            closeTime: "10s", //default: 10s - use s for seconds, m for minutes, d for days
            closeButton: "Close ticket", //default: Close Ticket
            closeEmoji: "❎" //deafult: ❎ 
        }
    })
    ticketinter.onInteraction()
})



client.login('TOKEN')


```

## ScreenShots
![ticket create embed](https://cdn.discordapp.com/attachments/895253373689938010/908127608934395944/Screen_Shot_2021-11-11_at_8.54.17_am.png)

![Ticket Open](https://cdn.discordapp.com/attachments/895253373689938010/908127609471270952/Screen_Shot_2021-11-11_at_8.54.27_am.png)

![Ticket Close](https://cdn.discordapp.com/attachments/895253373689938010/908127609995530290/Screen_Shot_2021-11-11_at_8.54.40_am.png)
