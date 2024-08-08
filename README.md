# alın lazım olur

const Discord = require('discord.js')
const { permissionsEmbed, TickEmbed } = require('../../client/embed.js');

module.exports = {
name: 'seviye',
aliases: ['rank'],

async execute(client, message, args) {

if(!args[0]) {
require('dotenv').config();
const embed = new Discord.EmbedBuilder()
.setColor(process.env.MAIN_COLOR)
.setDescription(`# <:levelup4:1269802908833157191> ${client.user.username} Seviye Sistemi`)
.addFields(
{ name: `<:levelup1:1269802981969105088> Seviye Kanalı İçin:`, value: `${process.env.PREFIX}level [<:text_channel:1267138418349965355>KanalEtiket]`, inline: true },
{ name: `<:levelup:1269802991108624544> Seviye Komutları:`, value: `${process.env.PREFIX}level (*eğer sistem aktifse*)\n${process.env.PREFIX}level-top\n${process.env.PREFIX}level-sistem`/*, inline: true*/ },
{ name: `<:soru:1269805673982590986> Nasıl Çalışır?`, value: `birisi mesaj yazdığında seviye atlayacak ve sıralamada gözükücek böylece sunucularda yarışlar olucak.` },
)
await message.channel.send({ embeds: [embed] })
}

if (args[0] && args[0].includes('<#') && args[0].includes('>')) {
    if (!message.member.permissions.has(Discord.PermissionFlagsBits.Administrator)) {
        return message.channel.send(permissionsEmbed(`# <:cancel:1266880050494705685> Bir hata aldım!\nMerhaba **${message.author.username}**, malesefki <:alert:1266881899192647803> **yönetici** yetkiniz bulunmadığından komutuna erişemiyorsunuz.`)).then(async (a) => {setTimeout(async () => {a.delete()}, 10000)})
    }

    let kanal = message.mentions.channels.first();
    if (!kanal) return message.channel.send({ embeds: [
    new Discord.EmbedBuilder()
    .setColor(process.env.ERROR_COLOR)
    .setDescription(`<:close:1269596239498842163> Üzgünüm, attığın şey kanal değil veya bu sunucudan değil.`)
    ]}).then(async (a) => {setTimeout(async () => {a.delete()}, 10000)})

    const embed = new Discord.EmbedBuilder()
    .setColor(process.env.SUCCESS_COLOR)
    .setDescription(`# <:levelup1:1269802981969105088> Başarıyla Tamamlandı!\n\n<:filess:1269802953309552732> Başarıyla **Seviye Kanal**'ını <#${kanal.id}> olarak seçtin!`)
    message.channel.send({ embeds: [embed] }).then(async (a) => {setTimeout(async () => {a.delete()}, 10000)})
}

if (args[0] === 'text') {
}

},
};
