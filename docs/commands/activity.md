[Wilson's Documents Copyright (C) 2021 Wilson](/info/license)

?> Replace *your_id_here* with your ID in order to stop random people changing your bot's activity.

### Activity Command
```js
//  Credit to: Wilson#0159 on Discord
//  This header message cannot be removed
//  Refer to the license page linked at the top

const { Client, MessageEmbed, CommandInteraction } = require('discord.js');

module.exports = {
    name: 'activity',
    description: 'Sets the activity for the bot. (Only for devs)',
    options: [
        {
            name: 'type',
            description: 'Choose between adding or removing the role from member.',
            type: 'STRING',
            required: true,
            choices: [
                {name: 'add', value: 'add'},
                {name: 'remove', value: 'remove'},
            ],
        },
        {
            name: 'activity',
            description: 'Choose the activity.',
            type: 'STRING',
            required: false,
            choices: [
                { name: 'WATCHING', value: 'WATCHING'},
                { name: 'PLAYING', value: 'PLAYING' },
                { name: 'LISTENING', value: 'LISTENING' },
            ],
        },
        {
            name: 'text',
            description: 'Enter activity text.',
            type: 'STRING',
            required: false,
        },
    ],
    /**
     * @param {CommandInteraction} interaction 
     * @param {client} Client
     */
    async execute(interaction, client) {
        if (interaction.member.id === "your_id_here") {
            const type     = interaction.options.getString('type');
            const activity = interaction.options.getString('activity');
            const text     = interaction.options.getString('text');

            switch (type) {
                case 'add':
                        client.user.setActivity({ type: `${activity}`, name: `${text}` });
                        interaction.reply({ content: `Done!`, ephemeral: true });
                    break;
                case 'remove': {
                        client.user.setPresence({ activity: null });
                        interaction.reply({ content: `Done!`, ephemeral: true });
                    break;
                }
            }
        }
    },
};
```
