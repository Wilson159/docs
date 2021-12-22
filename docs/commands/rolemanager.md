[Wilson's Documents Copyright (C) 2021 Wilson](/info/license)

### Role Manager
(Special thanks to KevinFoged#1138 for refactoring)
```js
//  GNU General Publice Lisence v3.0
//  Credit to: Wilson#0159 on Discord.
//  Removal of this header breaches the license agreement.
//  For more info, refer to the license page linked at the top.

const { CommandInteraction, MessageEmbed } = require("discord.js");

module.exports = {
    name: "role",
    description: "Manage a user's roles.",
    permission: "MANAGE_ROLES",
    options: [
        {
            name: "role",
            description: "Provide a role to add or remove.",
            type: "ROLE",
            required: true,
        },
        {
            name: "target",
            description: "Provide a user to manage.",
            type: "USER",
            required: false,
        },
    ],
    /**
     * @param {CommandInteraction} interaction
     */
    async execute(interaction) {
        const { options } = interaction;
        const role        = options.getRole("role");
        const target      = options.getMember("target") || interaction.member;
        const embed       = new MessageEmbed()
                            .setColor(`#${interaction.guild.roles.cache.get(role.id).color.toString(16)}`)
                            .setTitle("🎭 Role Management 🎭");

        embed.setDescription(target.roles.cache.has(role.id) ? `Removed the ${role} role from ${target}.` : `Added the ${role} role to ${target}.`);
        target.roles.cache.has(role.id) ? target.roles.remove(role) : target.roles.add(role);
        const message = await interaction.reply({embeds: [embed], fetchReply: true});
        setTimeout(() => message.delete().catch(() => {}), 5000);
    }
}
```
