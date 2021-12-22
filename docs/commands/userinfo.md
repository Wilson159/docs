[Wilson's Documents Copyright (C) 2021 Wilson](/info/license)

?> You will need to add the following code to your **Commands.js**, replacing the existing *Missing Description* section.
```js
if (!command.type && !command.description)
return Table.addRow(command.name, '🔸', 'Missing Description');
```
### Slash Command
(Special thanks to KevinFoged#1138 for refactoring and random colour part)
```js
//  GNU General Publice Lisence v3.0 - https://www.gnu.org/licenses/gpl-3.0.en.html
//  Credit to: Wilson#0159 on Discord.
//  Removal of this header breaches the license agreement.
//  For more info, refer to the license page linked at the top.

const { CommandInteraction, MessageEmbed } = require("discord.js");

module.exports = {
    name: "userinfo",
    description: "Displays the userinfo of the specified target.",
    options: [
        {
            name: "target",
            description: "Select the target.",
            type: "USER",
            required: false
        }
    ],
    /**
     * @param {CommandInteraction} interaction 
     */
    async execute(interaction) {
        const target = interaction.options.getMember("target") || interaction.member;
        await target.user.fetch();
        
        const response = new MessageEmbed()
            .setColor(target.user.accentColor || "RANDOM")
            .setAuthor(target.user.tag, target.user.avatarURL({dynamic: true}))
            .setThumbnail(target.user.avatarURL({dynamic: true}))
            .setImage(target.user.bannerURL({dynamic: true, size: 512}) || "")
            .addFields(
                {name: "ID", value: target.user.id},
                {name: "Joined Server", value: `<t:${parseInt(target.joinedTimestamp / 1000)}:R>`, inline: true},
                {name: "Account Created", value: `<t:${parseInt(target.user.createdTimestamp / 1000)}:R>`, inline: true},
                {name: "Roles", value: target.roles.cache.map(r => r).join(" ").replace("@everyone", "") || "None"},
                {name: "Accent Colour", value: target.user.accentColor ? `#${target.user.accentColor.toString(16)}` : "None"},
                {name: "Banner", value: target.user.bannerURL() ? "** **" : "None"}
            );
            
        interaction.reply({embeds: [response], ephemeral: true})
    }
}
```
### Context Menu
(Special thanks to KevinFoged#1138 for refactoring and random colour part)
```js
//  Credit to: Wilson#0159 on Discord.
//  Removal of this header breaches the license agreement.
//  For more info, refer to the license page linked at the top.

const { MessageEmbed, ContextMenuInteraction } = require("discord.js");

module.exports = {
    name: "User Info",
    type: "USER",

    /**
     * @param {ContextMenuInteraction} interaction 
     */
    async execute(interaction) {
        const target = await interaction.guild.members.fetch(interaction.targetId)
        await target.user.fetch();
        
        const response = new MessageEmbed()
            .setColor(target.user.accentColor || "RANDOM")
            .setAuthor(target.user.tag, target.user.avatarURL({dynamic: true}))
            .setThumbnail(target.user.avatarURL({dynamic: true}))
            .setImage(target.user.bannerURL({dynamic: true, size: 512}) || "")
            .addFields(
                {name: "ID", value: target.user.id},
                {name: "Joined Server", value: `<t:${parseInt(target.joinedTimestamp / 1000)}:R>`, inline: true},
                {name: "Account Created", value: `<t:${parseInt(target.user.createdTimestamp / 1000)}:R>`, inline: true},
                {name: "Roles", value: target.roles.cache.map(r => r).join(" ").replace("@everyone", "") || "None"},
                {name: "Accent Colour", value: target.user.accentColor ? `#${target.user.accentColor.toString(16)}` : "None"},
                {name: "Banner", value: target.user.bannerURL() ? "** **" : "None"}
            );
            
        interaction.reply({embeds: [response], ephemeral: true})
    }
}
```
