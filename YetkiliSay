const { MessageEmbed, Client, MessageActionRow, MessageButton } = require('discord.js');

module.exports = {
    conf: {
      aliases: ["ytsay"],
      name: "ysay"
    },
  
    run: async (client, message, args, embed) => {
      
       let emoji1 = client.emojis.cache.find(x => x.name === "yes") 
    let emoji2 = client.emojis.cache.find(x => x.name === "hayir") 
    
   if (!message.member.permissions.has("ADMINISTRATOR")) return message.react(`${emoji2}`)
      
 let adamlar = message.guild.members.cache.filter(admin => admin.roles.cache.has("YETKİLİ ID KOY")).filter(ses => !ses.voice.channel  && ses.presence && ses.presence.status != "offline")


const row = new MessageActionRow().addComponents(
new MessageButton().setCustomId("1").setLabel("Yetkili Say").setStyle("PRIMARY"),
new MessageButton().setCustomId("2").setLabel("Yetkili Dm At").setStyle("PRIMARY"),
new MessageButton().setCustomId("3").setLabel("İşlemi İptal Et").setStyle("DANGER")
);      


let sec = new MessageEmbed()
.setDescription(`Merhabalar ${message.member.toString()}, aşağıdan yetkilileri bilgilendirmek için butonları kullanabilirsin!

\` 1 \` __Yetkili Say__
\` 2 \` __Yetkili DM At__
\` 3 \` __İşlemi İptal Et!__   

`)
.setAuthor({ name: message.member.displayName, iconURL: message.member.displayAvatarURL({ dynamic: true }) })

 let msg = await message.channel.send({ embeds: [sec], components : [row] })


 var filter = (button) => button.user.id === message.author.id;
 let collector = await msg.createMessageComponentCollector({ filter, time: 60000 })

      collector.on("collect", async (button) => {

    if (button.customId === '1') {
     await button.deferUpdate();

   row.components[0].setDisabled(true) 
   row.components[1].setDisabled(true) 
   row.components[2].setDisabled(true)
 
    button.reply(`Sunucumuzda Aktif Olup Seste Olmayan **${adamlar.size}** Yetkili Bulunuyor!\n
\`Yetkililerin Listesi :\`\n${adamlar.map(member => member.toString()).join(`\n`)}`);

        }

    if (button.customId === '2') {
        await button.deferUpdate();

   row.components[0].setDisabled(true) 
   row.components[1].setDisabled(true) 
   row.components[2].setDisabled(true)
  
       button.reply({ content:`**${adamlar.size}** Adet Yetkiliye DM Aracılığı İle Haber Verilmeye Başlandı!`});
      
             let index = 0;
            adamlar.forEach(async member => {

                index += 1;
                await client.wait(index * 750);
                member.send({ content:`Merhabalar ${member.toString()}! Sunucumuzun Ses Aktifliğini Arttırmak İçin Public Seslere Veya Özel Odalara Geçebilir misin?`}).catch(err => message.channel.send({ content:`${member.toString()} Adlı Yetkiliye DM Aracılığıyla Ulaşamadım,Müsaitsen Public Seslere Veya Özel Odalara Geçebilir misin?`}));
    
                });

        }
        if (button.customId === '3') {
  
  await button.deferUpdate();
       
   row.components[0].setDisabled(true) 
   row.components[1].setDisabled(true) 
   row.components[2].setDisabled(true)

    msg.edit({
      embeds: [sec],
      components : [row]
    })

              

        }
            
                             
  });
}
}
