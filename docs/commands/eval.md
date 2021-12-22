[Wilson's Documents Copyright (C) 2021 Wilson](/info/license)

!> Change "YOUR_ID_HERE" to be your Discord ID.

### Usage Examples
```
const test = "ddd"; console.log(test);   <-- outputs ddd in console
```

### Eval
```js
//  GNU General Publice Lisence v3.0
//  Credit to: Wilson#0159 on Discord.
//  Removal of this header breaches the license agreement.
//  For more info, refer to the license page linked at the top.

const { MessageEmbed, CommandInteraction } = require('discord.js');

module.exports = {
    name: 'eval',
    description: 'Runs JS code through the bot!',
    ownerOnly: true,
    options: [
        {
            name: 'code',
            description: 'javascript code',
            type: 'STRING',
            required: true,
        },
    ],
    /**
     * @param {Client} client
     * @param {CommandInteraction} interaction
     */
    async execute(interaction, client) {
        if(interaction.user.id != "YOUR_ID_HERE") return interaction.reply({content: "You can't use this!", ephemeral: true}) 
                                    // ^ Add your ID here
        const code = interaction.options.getString('code');

        let evaled = eval(code);
        if (typeof evaled !== 'string')
            evaled = require('util').inspect(evaled);

        if (evaled === 'undefined') {
            interaction.reply({
                embeds: [
                    new MessageEmbed()
                        .setTitle('⚠ Eval ⚠')
                        .setColor('RED')
                        .addField('Command:', `\`\`\`${code}\`\`\``),
                ],
                ephemeral: true
            });
        } else {
            interaction.reply({
                embeds: [
                    new MessageEmbed()
                        .setTitle('⚠ Eval ⚠')
                        .setColor('RED')
                        .addField('Command:', `\`\`\`${code}\`\`\``)
                        .addField('Result:', `\`\`\`${evaled}\`\`\``),
                ],
                ephemeral: true,
            });
        }
    },
};
```
