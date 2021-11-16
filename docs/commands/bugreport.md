[Wilson's Documents Copyright (C) 2021 Wilson](/info/license)

### Bug Report Command
```js
const { CommandInteraction, MessageEmbed } = require("discord.js");

module.exports = {
    name: "bug_report",
    description: "Report any bugs or issues with the bot.",
    options: [
        {
            name: "type",
            description: "Choose type of bug.",
            type: "STRING",
            required: true,
            choices: [
                { name: "command", value: "Command" },
                { name: "event", value: "Event" },
                { name: "misc", value: "Misc" }
            ],
        },
        {
            name: "name",
            description: "Provide the name of the command, the event or the misc error.",
            type: "STRING",
            required: true
        },
        {
            name: "description",
            description: "Provide a description of the bug",
            type: "STRING",
            required: true
        }
    ],
    /**
     * 
     * @param {CommandInteraction} interaction 
     */
    async execute(interaction) {
        const { options } = require("discord.js");
        const type        = options.getString("type");
        const name        = options.getString("name");
        const description = options.getString("description");
        
        const response    = new MessageEmbed()
            .setTitle("Bug Report")
            .addFields(
                {name: "Type:", value: `${type}`, inline: true},
                {name: "Name:", value: `${name}`, inline: true},
                {name: "Description", value: `${description}`}
            );

        interaction.reply({embeds: [response]});
    }
}
```
