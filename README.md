const Discord = require('discord.js');
const client = new Discord.Client();

const ytdl = require('ytdl-core');

const cheerio = require('cheerio');

const request = require('request');

const token = 'NzMzNzM0OTkyNjk3NDkxNDg2.XxMkAw.bcMXrlqUU6K0PrK51wHyCEMPZ8E';

const PREFIX = '!' ;

var queue = new Map();

client.on('ready', () => {
    console.log('DyNa Online for YOU BOSS !');
})




client.on('message', message=>{
    
    let args = message.content.slice(PREFIX.length).split(" ");

    switch(args[0]){
        case 'ping':
            message.channel.send('pong!')
            break;
        case 'website':
            message.channel.send('http://www.youtube.com/c/DyNaofficial')
            break;
        case 'bilgi':
            message.channel.send('DyNa#5598 tarafından inşa edildim.Dilersen !komutlar ile birçok komuta erişim sağlayabilirsin.')
            break;
        case 'selam':
            message.channel.send('Merhabalar efendim')
            break;
        case 'sil':
            if(!args[1]) return message.reply('Bana bir sayı ver dostum kaç tane sileyim ?')
            message.channel.bulkDelete(args[1]);
            break;
        case 'embed':
            const embed = new Discord.MessageEmbed()
            .setTitle('Kullanıcı bilgileri')
            .addField('Kullanıcı adı', message.author.username)
            message.channel.send(embed);
        break;
        case 'pp' :
            message.channel.send(message.author.displayAvatarURL());
        break;
        case 'image' :
            image(message);

        break;
    }
});

function image(message){

    var options = {
        url: "http://results.dogpile.com/serp?qc=images&q=" + "dogs",
        method: "GET",
        headers: {
            "Accept": "text/html",
            "User-Agent": "Chrome"
        }
    }; 

    request(options, function(error, response, responseBody){
        if (error) {
            return;
        }

        $ = cheerio.load(responseBody);

        var links = $(".image a.link");

        var urls = new Array(links.length).fill(0).map((v, i) => links.eq(i).attr("href"));

        console.log(urls);
        if (!urls.length) {

            return;
        }

        // Send result
        message.channel.send( urls[Math.floor(Math.random() * urls.length)]);
    });
}


client.login(token);
