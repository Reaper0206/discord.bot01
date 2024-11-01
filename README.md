
import discord
from discord.ext import commands
import youtube_dl

# Bot'un prefixi
bot = commands.Bot(command_prefix='!')

# Müzik için ayarları yapılandır
ytdl_format_options = {
    'format': 'bestaudio/best',
    'postprocessors': [{
        'type': 'audio/ffmpeg',
        'preferredcodec': 'mp3',
        'preferredquality': '192',
    }],
}

ffmpeg_options = {
    'options': '-vn',
}

@bot.event
async def on_ready():
    print(f'Bot olarak giriş yapıldı: {bot.user}')

@bot.command()
async def merhaba(ctx):
    await ctx.send('Merhaba! Nasılsın?')

@bot.command()
async def müzik(ctx, *, url):
    voice_channel = ctx.author.voice.channel
    if voice_channel:
        voice_client = await voice_channel.connect()
        
        ytdl = youtube_dl.YoutubeDL(ytdl_format_options)
        info = ytdl.extract_info(url, download=False)
        url = info['formats'][0]['url']
        
        voice_client.play(discord.FFmpegPCMAudio(url, **ffmpeg_options))
    else:
        await ctx.send("Önce bir ses kanalına katılmalısın!")

@bot.command()
async def dur(ctx):
    voice_client = ctx.guild.voice_client
    if voice_client.is_playing():
        voice_client.stop()
    await voice_client.disconnect()

# Tokeninizi buraya yapıştırın
bot.run('TOKENİNİZİ_BURAYA_YAPIŞTIRIN')




#merhaba komutu, kullanıcıya basit bir merhaba mesajı gönderir.
#müzik komutu, belirtilen URL'den müzik çalar. Kullanıcının bir ses kanalında olması gerekmektedir.
#dur komutu ise müziği durdurur ve botu ses kanalından çıkarır.
import random

@bot.command()
async def meme(ctx):
    memeler = [
        "https://i.imgflip.com/30b1gx.jpg",  # Meme 1
        "https://i.imgflip.com/30b1h5.jpg",  # Meme 2
        "https://i.imgflip.com/30b1j9.jpg",  # Meme 3
        "https://i.imgflip.com/30b1lz.jpg",  # Meme 4
        "https://i.imgflip.com/30b1mx.jpg",  # Meme 5
        "https://i.imgflip.com/30b1n6.jpg",  # Meme 6
        "https://i.imgflip.com/30b1n9.jpg",  # Meme 7
        "https://i.imgflip.com/30b1o2.jpg",  # Meme 8
        "https://i.imgflip.com/30b1o6.jpg",  # Meme 9
        "https://i.imgflip.com/30b1o9.jpg"   # Meme 10
    ]

    meme_seçimi = random.choice(memeler)  # Rastgele bir meme seç
    await ctx.send(meme_seçimi)  # Seçilen meme'yi gönder

@bot.command()

async def çevre(ctx):
    ipuçları = [
        "1. Plastik kullanımını azaltmak için yeniden kullanılabilir çantalar kullanın.",
        "2. Geri dönüşüm kutularını doğru kullanarak atıkları ayırın.",
        "3. Yerel gıda pazarlarından alışveriş yaparak gıda taşımacılığını azaltın.",
        "4. Elektronik aletlerinizi tamir ettirin, yeni almak yerine onarmayı tercih edin.",
        "5. Su tasarrufu için kısa duşlar alın ve suyu açık bırakmamaya özen gösterin.",
        "6. Enerji tasarruflu ampuller kullanarak enerji tüketimini azaltın.",
        "7. Toplu taşıma veya bisiklet kullanarak karbon ayak izinizi azaltın.",
        "8. Atıklarınızı kompostlayarak organik atıkları değerlendirin.",
        "9. Yırtılan kıyafetlerimizi şorta,tişörte çevirmek.",
        "10.Aynı ayakkabıyı almamalıyız.",
        "11.Yere tükürmemek.",                                               
        "12.Yiyebildiğimiz kadar yemek almak.",
        "13.Sigara izmaritlerini yere atmamalıyız.",
        "14.Mangal yaptıktan sonra ateşi söndürmeliyiz.",
    ]

    await ctx.send("\n".join(ipuçları))


#Discord sunucunuzda !çevre yazdığınızda, yukarıda belirtilen ipuçlarını alacaksınız.


@bot.event
async def on_message(message):
    if message.author == bot.user:
        return

    # Belirli kelimelere tepki verme
    if "merhaba" in message.content.lower():
        await message.channel.send("Merhaba! Nasılsın?")
    elif "nasılsın" in message.content.lower():
        await message.channel.send("Ben bir botum, ama seninle sohbet etmek güzel!")
    elif "güle güle" in message.content.lower():
        await message.channel.send("Güle güle! Umarım tekrar gelirsin!")

    await bot.process_commands(message)  # Diğer komutların işlenmesi için
@bot.event
async def on_message(message):
    if message.author == bot.user:
        return

    # Belirli kelimelere tepki verme
    if "selam" in message.content.lower():
        await message.channel.send("Selam! Nasılsın?")
    elif "iyi" in message.content.lower():
        await message.channel.send("Harika! Bugün ne yapmayı planlıyorsun?")
    elif "kötü" in message.content.lower():
        await message.channel.send("Üzgünüm, umarım daha iyi hissedersin.")
    elif "nerede" in message.content.lower():
        await message.channel.send("Nerede olduğunu bilmem zor, ama buradayım!")
    elif "en sevdiğin" in message.content.lower():
        await message.channel.send("En sevdiğim şeyler arasında sohbet etmek var!")
    elif "film" in message.content.lower():
        await message.channel.send("Hangi tür filmleri seversin?")
    elif "müzik" in message.content.lower():
        await message.channel.send("Müzik harika bir şey! Hangi tür müzik dinlersin?")
    elif "hobi" in message.content.lower():
        await message.channel.send("Hobilerin neler? Yeni bir şeyler öğrenmek her zaman güzel!")
    elif "kitap" in message.content.lower():
        await message.channel.send("Hangi tür kitapları seversin? Bir öneri ister misin?")
    elif "şaka" in message.content.lower():
        await message.channel.send("İşte bir şaka: İki domates yolda yürüyordu, biri ezildi! 😂")

    await bot.process_commands(message)  # Diğer komutların işlenmesi için


@bot.event
async def on_message(message):
    if message.author == bot.user:
        return

    # Belirli kelimelere tepki verme
    if "günaydın" in message.content.lower():
        await message.channel.send("Günaydın! Bugünün harika geçsin!")
    elif "iyi akşamlar" in message.content.lower():
        await message.channel.send("İyi akşamlar! Günün nasıl geçti?")
    elif "hayır" in message.content.lower():
        await message.channel.send("Tamam, başka bir konuda konuşmak istersen buradayım!")
    elif "hava" in message.content.lower():
        await message.channel.send("Hava durumu hakkında bir şeyler duydun mu? Hangi hava durumunu seversin?")
    elif "yemek" in message.content.lower():
        await message.channel.send("Yemek yapmak harika bir hobi! En sevdiğin yemek nedir?")
    elif "tatil" in message.content.lower():
        await message.channel.send("Tatil planların var mı? Nereye gitmek istersin?")
    elif "teknoloji" in message.content.lower():
        await message.channel.send("Teknoloji dünyası sürekli değişiyor! Hangi gadget'lara meraklısın?")
    elif "spor" in message.content.lower():
        await message.channel.send("Spor yapmak sağlıklı bir alışkanlık! Hangi sporu yapıyorsun?")
    elif "doğa" in message.content.lower():
        await message.channel.send("Doğayı seviyorum! En sevdiğin doğal yer neresi?")
    elif "öneri" in message.content.lower():
        await message.channel.send("Öneri almak güzel! Hangi konuda öneri istersin?")

    await bot.process_commands(message)  # Diğer komutların işlenmesi için
@bot.event
async def on_message(message):
    if message.author == bot.user:
        return

    # Belirli kelimelere tepki verme
    if "selam" in message.content.lower():
        await message.channel.send("Selam! Nasılsın?")
    elif "ne yapıyorsun" in message.content.lower():
        await message.channel.send("Ben buradayım, seninle sohbet etmek için bekliyorum!")
    elif "sıkıldım" in message.content.lower():
        await message.channel.send("Sıkılmak zor! Bir şeyler yapalım, ne hakkında konuşmak istersin?")
    elif "favori" in message.content.lower():
        await message.channel.send("Favori şeylerin neler? Benim favorim sohbet etmek!")
    elif "bana bir şey söyle" in message.content.lower():
        await message.channel.send("Hayatta en önemli şey, sevdiğin şeyleri yapmaktır!")
    elif "kütüphane" in message.content.lower():
        await message.channel.send("Kütüphaneler harika! Hangi kitapları seviyorsun?")
    elif "tarih" in message.content.lower():
        await message.channel.send("Tarih, çok ilginç bir konu! Hangi tarihi olayları merak edersin?")
    elif "seyahat" in message.content.lower():
        await message.channel.send("Seyahat etmek harika bir deneyim! En sevdiğin yer neresi?")
    elif "belgesel" in message.content.lower():
        await message.channel.send("Belgeseller bilgilendirici olabilir! Hangi konularda belgesel izlersin?")
    elif "motivasyon" in message.content.lower():
        await message.channel.send("İşte bir motivasyon sözü: 'Başlamak, başarmanın yarısıdır!'")

    await bot.process_commands(message)  # Diğer komutların işlenmesi için
import math
import re

@bot.command()
async def hesapla(ctx, *, ifade: str):
    # Geçerli matematik işlemleri için bir regex kullanıyoruz
    if re.match(r'^[\d\+\-\*\/\.\(\) \sinotlg]+$', ifade):
        try:
            # İfade yerine daha güvenli bir değerlendirme yapalım
            sonuc = eval(ifade.replace('sin', 'math.sin')
                                 .replace('cos', 'math.cos')
                                 .replace('tan', 'math.tan')
                                 .replace('log', 'math.log'))
            await ctx.send(f"Sonuç: {sonuc}")
        except Exception as e:
            await ctx.send("Hesaplama sırasında bir hata oluştu.")
    else:
        await ctx.send("Lütfen geçerli bir matematik ifadesi girin.")
import re

@bot.command()
async def hesapla(ctx, *, ifade: str):
    # Geçerli matematik işlemleri için bir regex kullanıyoruz
    if re.match(r'^[\d\+\-\*\/\.\(\) ]+$', ifade):
        try:
            # İfadeyi değerlendiriyoruz
            sonuc = eval(ifade)
            await ctx.send(f"Sonuç: {sonuc}")
        except Exception as e:
            await ctx.send("Hesaplama sırasında bir hata oluştu.")
    else:
        await ctx.send("Lütfen geçerli bir matematik ifadesi girin.")
@bot.command()
async def devre(ctx):
    mesaj = (
        "Basit Bir Elektrik Devresi Yapımı:\n"
        "1. **Malzemeler:**\n"
        "- 1 adet pil (örneğin 9V)\n"
        "- 1 adet ampul (örneğin 5V)\n"
        "- 2 adet iletken tel\n"
        "- 1 adet anahtar (isteğe bağlı)\n\n"
        
        "2. **Bağlantı Adımları:**\n"
        "- Pilin pozitif (+) kutbunu bir iletken tel ile ampulün bir ucuna bağlayın.\n"
        "- Ampulün diğer ucunu diğer bir iletken tel ile pilin negatif (-) kutbuna bağlayın.\n"
        "- İsterseniz devreyi açıp kapamak için bir anahtar ekleyebilirsiniz. Anahtar, pil ile ampul arasındaki bağlantıyı keser.\n\n"
        
        "3. **Devreyi Test Edin:**\n"
        "- Bağlantıları kontrol edin ve anahtarı açın. Ampul yanıyorsa devre başarılı bir şekilde yapılmıştır!"
    )
    
    await ctx.send(mesaj)
@bot.command()
async def tarif(ctx):
    tarifler = (
        "İşte bazı yemek ve tatlı tarifleri:\n\n"
        
        "1. **Kısır**:\n"
        "- **Malzemeler**: İnce bulgur, domates, salatalık, biber, nar ekşisi, limon suyu, zeytinyağı, tuz, karabiber, maydanoz.\n"
        "- **Hazırlık**: Bulguru sıcak su ile ıslatın. 10 dakika bekledikten sonra doğranmış sebzeleri ekleyin. Sosu hazırlayıp karıştırın. Soğuk servis yapın.\n\n"

        "2. **Mercimek Köftesi**:\n"
        "- **Malzemeler**: Kırmızı mercimek, ince bulgur, soğan, domates salçası, biber salçası, yeşil soğan, maydanoz, limon suyu, baharatlar.\n"
        "- **Hazırlık**: Mercimekleri haşlayın, bulguru ekleyin ve karıştırın. Soğanı kavurun, salçaları ekleyin. Karışımı yoğurun, şekil verin ve soğuk servis yapın.\n\n"

        "3. **Sütlaç**:\n"
        "- **Malzemeler**: Pirinç, süt, şeker, vanilya, nişasta, tarçın.\n"
        "- **Hazırlık**: Pirinci haşlayın, sütü ve şekeri ekleyin. Kaynadıktan sonra nişastayı ekleyin ve karıştırın. Kaselere dökün, soğutun ve üzerine tarçın serpin.\n\n"

        "4. **Çikolatalı Kek**:\n"
        "- **Malzemeler**: Un, kakao, şeker, yumurta, süt, sıvı yağ, kabartma tozu.\n"
        "- **Hazırlık**: Tüm malzemeleri karıştırıp yağlanmış kek kalıbına dökün. 180°C'de 30-35 dakika pişirin. Soğuduktan sonra dilimleyin.\n\n"

        "5. **Zeytinyağlı Enginar**:\n"
        "- **Malzemeler**: Enginar, zeytinyağı, limon, havuç, bezelye, tuz.\n"
        "- **Hazırlık**: Enginarları temizleyip, limonlu suda bekletin. Zeytinyağında havuç ve bezelyeyi soteleyin, enginarları ekleyin ve pişirin.\n\n"

        "6. **Tavuk Sote**:\n"
        "- **Malzemeler**: Tavuk göğsü, biber, soğan, sarımsak, tuz, karabiber, zeytinyağı.\n"
        "- **Hazırlık**: Tavukları küp küp doğrayın. Zeytinyağında soğan ve sarımsağı kavurun, ardından tavukları ekleyin. Biberleri ekleyip pişirin.\n\n"

        "7. **Fırın Patates**:\n"
        "- **Malzemeler**: Patates, zeytinyağı, tuz, biberiye.\n"
        "- **Hazırlık**: Patatesleri doğrayıp zeytinyağı ve baharatlarla karıştırın. Fırında 200°C'de 30-40 dakika pişirin.\n\n"

        "8. **Baklava**:\n"
        "- **Malzemeler**: Yufka, ceviz, tereyağı, şeker, su, limon.\n"
        "- **Hazırlık**: Yufkaları tereyağı ile kat kat dizin. Cevizleri serpiştirin. Üzerine şeker ve su ile hazırlanan şerbeti dökün.\n"
    )
    
    await ctx.send(tarifler)

@bot.command()
async def youtube(ctx):
    await ctx.send("YouTube'a gitmek için buraya tıklayın: https://www.youtube.com")
@bot.command()
async def carpim(ctx):
    carpim_tablosu = "Çarpım Tablosu:\n\n"
    
    for i in range(1, 11):
        carpim_tablosu += f"{i}:\t" + "\t".join(str(i * j) for j in range(1, 11)) + "\n"
    
    await ctx.send(carpim_tablosu)
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

pi_value = (
    "3.1415926535 8979323846 2643383279 5028841971 6939937510 5820974944 5923078164 0628620899 "
    "8628034825 3421170679 8214808651 3282306647 0938446095 5058223172 5359408128 4811174502 "
    "8410270193 8521105559 6446229489 5493038196 4428810975 6659334461 2847564823 3786783165 "
    "2712019091 4564856692 3460348610 4543266482 1339360726 0249141273 7245870066 0631558817 "
    "4881520920 9628292540 9171536436 7892590360 0113305305 4882046652 1384146951 9415116094 "
    "3305727036 5759591953 0921861173 8193261179 3105118548 0744623799 6274956735 1885752724 "
    "8912279381 8301194912 9833673362 4406566430 8602139494 6395224737 1907021798 6094370277 "
    "0539217176 2931767523 8467481846 7669405132 0005681271 4526356082 7785771342 7577896091 "
    "7363717872 1468440901 2249534301 4654958537 1050792279 6892589235 4201995611 2129021960 "
    "8640344181 5981362977 4771309960 5187072113 4999999837 2978049951 0597317328 1609631859 "
    "5024459455 3469083026 4252230825 3344685035 2619311881 7101000313 7838752886 5875332083 "
    "8142061717 7669147303 5982534904 2875546873 1159562863 8823537875 9375195778 1857780532 "
    "1712268066 0631558817 4881520920 9628292540 9171536436 7892590360 0113305305 4882046652 "
    "1384146951 9415116094 3305727036 5759591953 0921861173 8193261179 3105118548 0744623799 "
    "6274956735 1885752724 8912279381 8301194912 9833673362 4406566430 8602139494 6395224737 "
    "1907021798 6094370277 0539217176 2931767523 8467481846 7669405132 0005681271 4526356082 "
    "7785771342 7577896091 7363717872 1468440901 2249534301 4654958537 1050792279 6892589235 "
    "4201995611 2129021960 8640344181 5981362977 4771309960 5187072113 4999999837 2978049951 "
    "0597317328 1609631859 5024459455 3469083026 4252230825 3344685035 2619311881 7101000313 "
    "7838752886 5875332083 8142061717 7669147303 5982534904 2875546873 1159562863 8823537875 "
    "9375195778 1857780532 1712268066 0631558817 4881520920 9628292540 9171536436 7892590360 "
    "0113305305 4882046652 1384146951 9415116094 3305727036 5759591953 0921861173 8193261179 "
    "3105118548 0744623799 6274956735 1885752724 8912279381 8301194912 9833673362 4406566430 "
    "8602139494 6395224737 1907021798 6094370277 0539217176 2931767523 8467481846 7669405132 "
    "0005681271 4526356082 7785771342 7577896091 7363717872 1468440901 2249534301 4654958537 "
    "1050792279 6892589235 4201995611 2129021960 8640344181 5981362977 4771309960 5187072113 "
    "4999999837 2978049951 0597317328 1609631859 5024459455 3469083026 4252230825 3344685035 "
    "2619311881 7101000313 7838752886 5875332083 8142061717 7669147303 5982534904 2875546873 "
    "1159562863 8823537875 9375195778 1857780532 1712268066 0631558817 4881520920 9628292540 "
    "9171536436 7892590360 0113305305 4882046652 1384146951 9415116094 3305727036 5759591953 "
    "0921861173 8193261179 3105118548 0744623799 6274956735 1885752724 8912279381 8301194912 "
    "9833673362 4406566430 8602139494 6395224737 1907021798 6094370277 0539217176 2931767523 "
    "8467481846 7669405132 0005681271 4526356082 7785771342 7577896091 7363717872 1468440901 "
    "2249534301 4654958537 1050792279 6892589235 4201995611 2129021960 8640344181 5981362977 "
    "4771309960 5187072113 4999999837 2978049951 0597317328 1609631859 5024459455 3469083026 "
    "4252230825 3344685035 2619311881 7101000313 7838752886 5875332083 8142061717 7669147303 "
    "5982534904 2875546873 1159562863 8823537875 9375195778 1857780532 1712268066 0631558817 "
    "4881520920 9628292540 9171536436 7892590360 0113305305 4882046652 1384146951 9415116094 "
    "3305727036 5759591953 0921861173 8193261179 3105118548 0744623799 6274956735 1885752724 "
    "8912279381 8301194912 9833673362 4406566430 8602139494 6395224737 1907021798 6094370277 "
    "0539217176 2931767523 8467481846 7669405132 0005681271 4526356082 7785771342 7577896091 "
    "7363717872 1468440901 2249534301 4654958537 1050792279 6892589235 4201995611 2129021960 "
    "8640344181 5981362977 4771309960 5187072113 4999999837 2978049951 0597317328 1609631859 "
    "5024459455 3469083026 4252230825 3344685035 2619311881 7101000313 7838752886 5875332083 "
    "8142061717 7669147303 5982534904 2875546873 1159562863 8823537875 9375195778 1857780532 "
    "1712268066 0631558817 4881520920 9628292540 9171536436 7892590360 0113305305 4882046652 "
    "1384146951 9415116094 3305727036 5759591953 0921861173 8193261179 3105118548 0744623799 "
    "6274956735 1885752724 8912279381 
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def acılar(ctx):
    message = (
        "**Çokgenlerde Açıların Özellikleri:**\n"
        "1. **İç Açı:** Bir çokgenin iç kısmındaki açıları ifade eder. \n"
        "   - İç açıların toplamı: (n - 2) * 180° (n: çokgenin kenar sayısı)\n"
        "   - Örnek: 5 kenarlı bir çokgenin (pentagon) iç açıları toplamı: (5 - 2) * 180° = 540°\n"
        "\n"
        "2. **Dış Açı:** Birçok kenarın uzatılmasıyla oluşan dış açılardır.\n"
        "   - Dış açıların toplamı her zaman 360°'dir.\n"
        "   - Her dış açı, karşısındaki iç açı ile toplamı 180° olacak şekilde hesaplanır.\n"
        "\n"
        "**Çokgenlerin Merkez Açıları:**\n"
        "Her bir kenar için merkezde oluşan açıdır.\n"
        "   - Merkez açısı: 360° / n (n: çokgenin kenar sayısı)\n"
        "   - Örnek: 6 kenarlı bir çokgenin merkez açısı: 360° / 6 = 60°\n"
        "\n"
        "**Yarıçap ve Çap:**\n"
        "1. **Yarıçap (r):** Çemberin merkezinden çember üzerindeki bir noktaya olan mesafedir.\n"
        "2. **Çap (d):** Yarıçapın iki katıdır, yani d = 2r.\n"
        "3. **Çemberin Alanı (A):** A = π * r²\n"
        "4. **Çemberin Çevresi (C):** C = 2 * π * r\n"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def acılar(ctx):
    message = (
        "**Çokgenlerde Açıların Özellikleri**\n\n"
        
        "**1. İç Açı:**\n"
        "   - Bir çokgenin iç kısmındaki açıları ifade eder.\n"
        "   - İç açıların toplamı, formülle hesaplanır:\n"
        "     \n   **İç Açıların Toplamı:** (n - 2) * 180°  \n"
        "     (n: çokgenin kenar sayısı)\n"
        "   - Örnek: 5 kenarlı bir çokgenin (pentagon) iç açıları toplamı:\n"
        "     \n   **540°**  \n"
        
        "**2. Dış Açı:**\n"
        "   - Dış açılar, bir kenarın uzatılmasıyla oluşan açılardır.\n"
        "   - Her bir iç açının karşısında bir dış açı bulunur:\n"
        "     \n   **Dış Açıların Toplamı:** 360°\n"
        "   - Her dış açı ile karşısındaki iç açının toplamı:\n"
        "     \n   **İç Açı + Dış Açı = 180°**\n"
        "   - Örnek: 6 kenarlı bir çokgen (hexagon) için:\n"
        "     \n   Dış açı = 360° / 6 = 60°\n"
        
        "**3. Merkez Açı:**\n"
        "   - Çokgenin merkezinden geçen çizgi ile iki köşe arasında oluşan açıdır.\n"
        "   - Merkez açısı, çokgenin kenar sayısına bağlıdır:\n"
        "     \n   **Merkez Açısı:** 360° / n  \n"
        "   - Örnek: 8 kenarlı bir çokgenin merkez açısı:\n"
        "     \n   **45°**\n"
        
        "**Çember ve Daire ile İlgili Terimler**\n\n"
        
        "**1. Yarıçap (r):**\n"
        "   - Çemberin merkezinden çember üzerindeki bir noktaya olan mesafedir.\n"
        
        "**2. Çap (d):**\n"
        "   - Çemberin tam ortasından geçen ve çemberi iki eşit parçaya ayıran doğru parçasıdır.\n"
        "   - Çap, yarıçapın iki katıdır:\n"
        "     \n   **d = 2r**\n"
        
        "**3. Çemberin Alanı (A):**\n"
        "   - Çemberin iç kısmının alanıdır:\n"
        "     \n   **A = π * r²**\n"
        
        "**4. Çemberin Çevresi (C):**\n"
        "   - Çemberin dış kısmının uzunluğudur:\n"
        "     \n   **C = 2 * π * r**\n"
        
        "**Örnek Hesaplamalar:**\n"
        "1. 5 Kenarlı Bir Çokgen (Pentagon):\n"
        "   - İç Açı Toplamı: (5 - 2) * 180° = 540°\n"
        "   - Her İç Açı: 540° / 5 = 108°\n"
        "   - Dış Açı: 360° / 5 = 72°\n\n"
        
        "2. Çember:\n"
        "   - Yarıçap = 7 cm ise:\n"
        "   - Çap = 2 * 7 = 14 cm\n"
        "   - Alan = π * (7)² ≈ 154 cm²\n"
        "   - Çevre = 2 * π * 7 ≈ 44 cm\n"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def periyodik(ctx):
    message = (
        "**Periyodik Tablo**\n\n"
        "Periyodik tablo, elementlerin düzenli bir biçimde sıralandığı bir tablodur. Elementler, "
        "özelliklerine göre gruplara ve periyotlara ayrılır. İşte periyodik tablonun bazı önemli "
        "özellikleri:\n\n"
        
        "**1. Temel Bilgiler:**\n"
        "   - **Element:** Kimyasal bir madde olan ve atom numarasına göre sıralanan en küçük "
        "birim.\n"
        "   - **Atom Numarası:** Bir elementin çekirdeğindeki proton sayısını gösterir.\n"
        "   - **Simge:** Her elementin kısaltmasıdır (örneğin, O = Oksijen).\n"
        "   - **Ağırlık:** Elementin ortalama atom ağırlığıdır.\n\n"

        "**2. Periyotlar:**\n"
        "   - Periyodik tabloda yatay satırlara periyot denir. Her periyot, elementlerin "
        "elektron yapılarına göre düzenlenmiştir.\n"
        "   - Örneğin, 1. periyot H (Hidrojen) ve He (Helyum) elementlerini içerir.\n\n"

        "**3. Gruplar:**\n"
        "   - Dikey sütunlara grup denir. Gruplar, benzer kimyasal özelliklere sahip "
        "elementleri bir araya getirir.\n"
        "   - Örneğin, 1. grup alkali metaller, 17. grup halojenlerdir.\n\n"

        "**4. Element Grupları ve Özellikleri:**\n"
        "   - **Alkali Metaller (Grup 1):** Yumuşak, reaktif metaller (örneğin, Li, Na, K).\n"
        "   - **Toprak Alkali Metaller (Grup 2):** Daha az reaktif metaller (örneğin, Be, Mg, Ca).\n"
        "   - **Geçiş Metalleri (Gruplar 3-12):** Genellikle sert ve yüksek erime noktasına "
        "sahip metaller.\n"
        "   - **Halojenler (Grup 17):** Çok reaktif gazlar veya sıvılar (örneğin, F, Cl, Br).\n"
        "   - **Soy Gazlar (Grup 18):** Genellikle reaktif olmayan gazlar (örneğin, He, Ne, Ar).\n\n"

        "**5. Önemli Elementler:**\n"
        "   - **Hidrojen (H):** En hafif element ve en yaygın elementtir.\n"
        "   - **Karbon (C):** Organik yaşamın temel taşıdır.\n"
        "   - **Oksijen (O):** Yaşam için gerekli olan gazdır.\n"
        "   - **Demir (Fe):** Metal ve birçok bileşikte önemli bir elementtir.\n\n"

        "**6. Kullanım Alanları:**\n"
        "   - **Kimya:** Reaksiyonların anlaşılması ve bileşenlerin tanımlanması için.\n"
        "   - **Fizik:** Elementlerin fiziksel özellikleri ile ilgili çalışmalar için.\n"
        "   - **Biyoloji:** Canlı organizmalardaki elementlerin rolü hakkında bilgi sağlar.\n"
        "   - **Endüstri:** Metal ve bileşiklerin üretiminde kullanılır.\n\n"

        "**Periyodik Tablo:**\n"
        "```"
        " H  He\n"
        "Li Be          B  C  N  O  F  Ne\n"
        "Na Mg          Al Si P  S  Cl Ar\n"
        "K  Ca Sc Ti  V  Cr Mn Fe Co Ni Cu Zn Ga Ge As Se Br Kr\n"
        "Rb Sr Y  Zr Nb Mo Tc Ru Rh Pd Ag Cd In Sn Sb Te I  Xe\n"
        "Cs Ba La Hf Ta W  Re Os Ir Pt Au Hg Tl Pb Bi Po At Rn\n"
        "Fr Ra Ac Rf Db Sg Bh Hs Mt Ds Rg Cn Nh Fl Mc Lv Ts Og\n"
        "```"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def uzay(ctx):
    message = (
        "**Uzay Hakkında Bilgiler**\n\n"

        "**1. Uzay Nedir?**\n"
        "   - Uzay, evrenin tümünü kapsayan, boşluk olarak tanımlanan bir ortamdır. "
        "Atmosferin dışında, yıldızlar, gezegenler, galaksiler ve diğer gök cisimlerini içerir.\n\n"

        "**2. Evrenin Yapısı:**\n"
        "   - **Galaksiler:** Uzayda bulunan devasa yıldız, gaz ve toz bulutlarıdır. "
        "Örneğin, Samanyolu Galaksisi.\n"
        "   - **Yıldızlar:** Kendiliğinden enerji üreten gök cisimleridir. Güneşimiz bir yıldızdır.\n"
        "   - **Gezegenler:** Yıldızların etrafında dönen, kendi ışığı olmayan cisimlerdir. "
        "Örneğin, Dünya, Mars, Jüpiter.\n"
        "   - **Uydular:** Gezegenlerin etrafında dönen cisimlerdir. Ay, Dünya'nın doğal uydusudur.\n"
        "   - **Asteroitler ve Kuyruklu Yıldızlar:** Uzayda dolaşan daha küçük cisimlerdir.\n\n"

        "**3. Uzayda Fiziksel Özellikler:**\n"
        "   - **Boşluk:** Uzayda hava yoktur; dolayısıyla ses iletilemez.\n"
        "   - **Ağırlıksızlık:** Astronotlar uzayda ağırlıksızlık hissi yaşarlar.\n"
        "   - **Sıcaklık:** Uzayda sıcaklık, direkt güneş ışığına maruz kalmayan bölgelerde çok düşük olabilir.\n\n"

        "**4. Uzay Araştırmaları:**\n"
        "   - **Uydu ve Uzay Araçları:** Uzay araştırmaları için kullanılır. Örneğin, Hubble Uzay Teleskobu.\n"
        "   - **Astronotlar:** Uzayda araştırma yapmak üzere eğitilmiş uzmanlardır.\n"
        "   - **Uzay İstasyonları:** Uluslararası Uzay İstasyonu (ISS) gibi yapılar, bilimsel araştırmalar için kullanılır.\n\n"

        "**5. Uzay Zaman Teorisi:**\n"
        "   - **Görelilik Teorisi:** Albert Einstein tarafından geliştirilen bu teori, uzay ve zamanın birbiriyle bağlantılı olduğunu ifade eder.\n"
        "   - **Kara Delikler:** Çok yüksek kütleye sahip olan ve ışığı bile çekebilen bölgeler.\n"
        "   - **Büyük Patlama Teorisi:** Evrenin oluşumunu açıklayan en yaygın teoridir.\n\n"

        "**6. Uzayda Yaşam:**\n"
        "   - **Dışarıda Yaşam:** Mars, Europa (Jüpiter'in uydusu) gibi yerlerde yaşam izleri araştırılmaktadır.\n"
        "   - **Exoplanetler:** Başka yıldızların etrafında dönen gezegenler. Yaşam için uygun koşullara sahip olma ihtimalleri araştırılıyor.\n\n"

        "**7. Uzayda Seyahat:**\n"
        "   - **Uzay Mekiği ve Roketler:** İnsanları ve yükleri uzaya taşımak için kullanılan araçlar.\n"
        "   - **Seyahat Zorlukları:** Uzayda uzun süre kalmanın psikolojik ve fiziksel zorlukları vardır.\n\n"

        "**8. Uzay ve Bilim Kurgu:**\n"
        "   - Uzay, birçok bilim kurgu eserinde önemli bir tema olarak yer alır. Star Wars, Star Trek gibi seriler popülerdir.\n\n"

        "**9. Uzayın Gizemleri:**\n"
        "   - **Karanlık Madde:** Evrenin kütlesinin büyük bir kısmını oluşturduğu düşünülen, ancak doğrudan gözlemlenemeyen madde.\n"
        "   - **Karanlık Enerji:** Evrenin genişlemesini hızlandıran ve bilinmeyen bir enerji türüdür.\n\n"

        "**Uzay hakkında daha fazla bilgi edinmek isterseniz, uzayla ilgili kitaplar, belgeseller ve makaleler bulabilirsiniz!**"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def frekans(ctx):
    message = (
        "**Frekans Hakkında Bilgiler**\n\n"

        "**1. Frekans Nedir?**\n"
        "   - Frekans, bir olayın belirli bir zaman diliminde kaç kez tekrarlandığını ifade eder. "
        "Genellikle dalgaların, titreşimlerin veya seslerin ölçülmesinde kullanılır.\n"
        "   - Birimi Hertz (Hz) ile ölçülür; 1 Hz, bir saniyede bir döngüyü ifade eder.\n\n"

        "**2. Frekans ve Periyot Arasındaki İlişki:**\n"
        "   - Frekans (f) ile periyot (T) arasındaki ilişki:  \n"
        "     **f = 1 / T**  \n"
        "     - Burada T, bir döngünün tamamlanması için geçen süreyi ifade eder.  \n"
        "     - Yüksek frekans, kısa periyot; düşük frekans, uzun periyot demektir.\n\n"

        "**3. Farklı Türde Frekanslar:**\n"
        "   - **Ses Frekansı:** 20 Hz - 20 kHz aralığında duyulabilen ses dalgalarıdır.  \n"
        "   - **Radyo Frekansı:** 3 kHz - 300 GHz arasında değişen frekanslar, radyo dalgaları olarak bilinir.  \n"
        "   - **Işık Frekansı:** Görünür ışığın frekansı, yaklaşık 430 THz (terahertz) ile 750 THz arasında değişir.\n\n"

        "**4. Frekansın Özellikleri:**\n"
        "   - **Dalgalar:** Frekans, dalgaların özelliği olarak tanımlanır. Su dalgaları, ses dalgaları ve elektromanyetik dalgalar frekansa sahiptir.\n"
        "   - **Frekans Spektrumu:** Farklı frekansların bir arada bulunduğu aralıklara denir.  \n"
        "     - Örneğin, ses frekansı spektrumu, müzikteki tonların belirlenmesinde önemlidir.\n\n"

        "**5. Frekans ve Enerji İlişkisi:**\n"
        "   - Frekans arttıkça enerjinin de arttığı gözlemlenir.  \n"
        "   - Planck sabiti kullanılarak enerji (E) ile frekans (f) arasındaki ilişki:  \n"
        "     **E = h * f**  \n"
        "     - Burada h, Planck sabitidir.\n\n"

        "**6. Uygulama Alanları:**\n"
        "   - **Müzik:** Farklı nota frekansları, müziğin temelini oluşturur.  \n"
        "   - **Telekomünikasyon:** Radyo dalgaları, telefon ve internet iletişimi için kullanılır.  \n"
        "   - **Frekans Analizi:** Mühendislikte ve fiziksel bilimlerde sinyallerin analizi için kullanılır.\n\n"

        "**7. Örnekler:**\n"
        "   - A notasının frekansı: 440 Hz.\n"
        "   - Kısa dalga radyoları: 3 MHz - 30 MHz.\n"
        "   - Görünür ışık: 430 - 750 THz.\n\n"

        "**Frekans hakkında daha fazla bilgi için fizik ve mühendislik kaynaklarına göz atabilirsiniz!**"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def kuvvet(ctx):
    message = (
        "**Kuvvet Hakkında Bilgiler**\n\n"

        "**1. Kuvvet Nedir?**\n"
        "   - Kuvvet, bir nesne üzerinde etki yaratan ve nesnenin hareketini değiştirebilen bir etkidir. "
        "Newton'un hareket yasalarına göre, kuvvet nesnenin hızını, yönünü veya şeklini değiştirebilir.\n"
        "   - Kuvvetin birimi Newton (N) olarak tanımlanır. 1 Newton, 1 kg'lık bir kütleye 1 m/s²'lik bir ivme kazandıran kuvvet olarak tanımlanır.\n\n"

        "**2. Kuvvetin Temel Özellikleri:**\n"
        "   - **Vektörel Büyüklük:** Kuvvet, bir büyüklük ve yön içerdiği için vektör olarak temsil edilir.\n"
        "   - **Büyüklük:** Kuvvetin ne kadar büyük olduğunu belirtir (örneğin, 10 N).\n"
        "   - **Yön:** Kuvvetin hangi yönde etki ettiğini gösterir (örneğin, yukarı, aşağı, sağ, sol).\n\n"

        "**3. Kuvvet Türleri:**\n"
        "   - **Temas Kuvvetleri:** İki nesne arasında doğrudan temas gerektiren kuvvetlerdir. Örneğin:\n"
        "     - **Sürtünme Kuvveti:** İki yüzey arasında hareketi engelleyen kuvvet.\n"
        "     - **Normal Kuvvet:** Yüzeyin üzerine uygulanan kuvvet, genellikle dik yöndedir.\n"
        "   - **Uzaktan Etkileyen Kuvvetler:** Temas gerektirmeyen kuvvetlerdir. Örneğin:\n"
        "     - **Gravitasyon Kuvveti:** Kütleler arasında çekim kuvveti. Yer çekimi bu kuvvetin bir örneğidir.\n"
        "     - **Elektromanyetik Kuvvet:** Yükler arasında etki eden kuvvetler.\n\n"

        "**4. Newton'un Hareket Yasaları:**\n"
        "   - **Birinci Yasa (Eylemsizlik Yasası):** Bir nesne üzerine net bir kuvvet uygulanmadıkça, nesne ya hareketsiz kalır ya da sabit hızla hareket eder.\n"
        "   - **İkinci Yasa:** Net kuvvet (F), kütle (m) ile ivme (a) çarpımına eşittir:  \n"
        "     **F = m * a**\n"
        "     - Burada F, net kuvvet, m kütle, a ise ivmedir.\n"
        "   - **Üçüncü Yasa (Etki-Tepki Yasası):** Her kuvvetin eşit ve zıt bir tepki kuvveti vardır.  \n"
        "     - Örneğin, bir cismi iterseniz, cisim de sizi geri iter.\n\n"

        "**5. Kuvvetin Hesaplanması:**\n"
        "   - Kuvveti hesaplamak için, bir nesnenin kütlesini ve uygulanan ivmeyi bilmek gerekir.  \n"
        "   - Örnek: 10 kg'lık bir cisme 2 m/s²'lik bir ivme uygulandığında:  \n"
        "     **F = 10 kg * 2 m/s² = 20 N**\n\n"

        "**6. Uygulama Alanları:**\n"
        "   - **Mühendislik:** Yapıların tasarımı ve güvenliği için kuvvet analizi yapılır.\n"
        "   - **Fizik:** Kuvvet, hareketin ve dinamiğin temel unsurlarındandır.\n"
        "   - **Gündelik Hayat:** Nesneleri kaldırırken, itme veya çekme sırasında kuvvet kullanırız.\n\n"

        "**7. Kuvvetin Diğer Kavramlarla İlişkisi:**\n"
        "   - **Enerji:** Kuvvet, iş yapma kapasitesiyle ilişkilidir.  \n"
        "     - İş (W) = Kuvvet (F) * Mesafe (d) * cos(θ)  \n"
        "   - **Momentum:** Bir nesnenin kütlesi ile hızının çarpımıdır. Kuvvet, momentumun değişimini etkiler.\n\n"

        "**Kuvvet, doğanın temel bir özelliğidir ve çevremizdeki her şeyde etkisini gösterir. Daha fazla bilgi için fizik kaynaklarına başvurabilirsiniz!**"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def satranç(ctx):
    message = (
        "**Satranç Hakkında Bilgiler**\n\n"

        "**1. Satranç Nedir?**\n"
        "   - Satranç, iki oyuncu arasında oynanan stratejik bir masa oyunudur. "
        "Oyun, 64 kareden oluşan bir tahtada 16 taşla oynanır. Amaç, rakibin şahını mat etmektir.\n\n"

        "**2. Taşlar ve Hareketleri:**\n"
        "   - **Şah:** Her oyuncunun en önemli taşıdır. Şah, her yönde bir kare hareket edebilir.\n"
        "   - **Vezir:** En güçlü taş olup, her yönde sınırsız kare hareket edebilir.\n"
        "   - **Kale:** Yalnızca dikey ve yatay olarak hareket eder. Sınırsız kare hareket edebilir.\n"
        "   - **Fil:** Yalnızca çapraz yönde hareket eder. Sınırsız kare hareket edebilir.\n"
        "   - **At:** L şeklinde (iki kare bir yönde ve bir kare dik yönde) hareket eder. Diğer taşların üzerinden atlayabilir.\n"
        "   - **Piyon:** Yalnızca ileri doğru hareket eder. İlk hamlede iki kare, sonrasında bir kare hareket eder. Rakip taşını almak için çapraz hareket eder.\n\n"

        "**3. Oyun Kuralları:**\n"
        "   - Oyun, beyaz taşlarla başlar ve her oyuncu sırayla bir taş hareket ettirir.\n"
        "   - Eğer bir taş, rakip taşını tehdit ederse, o taş alınır ve tahtadan çıkar.\n"
        "   - **Mat:** Rakibin şahı tehdit altındaysa ve kaçış yolu yoksa, bu durum mat olarak adlandırılır ve oyun sona erer.\n"
        "   - **Beraberlik:** Oyun, belirli koşullar altında berabere bitebilir (örneğin, stalemate durumu).\n\n"

        "**4. Oyun Stratejileri:**\n"
        "   - **Gelişim:** Taşları oyunun başında etkili bir şekilde konumlandırmak önemlidir.\n"
        "   - **Merkez Kontrolü:** Tahtanın ortasını kontrol etmek, taşların hareketliliğini artırır.\n"
        "   - **Taşların Korunması:** Taşları savunmasız bırakmamaya dikkat edin.\n"
        "   - **Taktik ve Kombinasyonlar:** Rakibin hamlelerini öngörmek ve fırsatlar yaratmak için taktikler geliştirin.\n\n"

        "**5. Satranç Terminolojisi:**\n"
        "   - **Açılış:** Oyunun başlangıcında yapılan hamleler.\n"
        "   - **Taktik:** Rakibin taşlarını tehdit eden kısa süreli hamleler.\n"
        "   - **Pozisyon:** Tahtada mevcut taş konumları.\n"
        "   - **Endgame:** Oyun sonuna yaklaşırken taş sayısının azaldığı dönem.\n\n"

        "**6. Satranç Tarihçesi:**\n"
        "   - Satranç, kökenleri 6. yüzyıla kadar uzanan eski bir oyundur. Farklı kültürlerde çeşitli biçimlerde oynanmıştır.\n"
        "   - Modern satranç kuralları, 15. yüzyılda Avrupa'da şekillenmiştir.\n\n"

        "**7. Satranç Oyunları ve Şampiyonaları:**\n"
        "   - Dünya Satranç Şampiyonası, uluslararası düzeyde en prestijli satranç turnuvasıdır.\n"
        "   - FIDE (Dünya Satranç Federasyonu), satrançta uluslararası standartları belirler.\n\n"

        "**8. Satrançta Gelişim:**\n"
        "   - Satranç öğrenmek için kitaplar, online platformlar ve uygulamalar mevcuttur.\n"
        "   - Satranç bulmacaları ve taktik çalışmaları ile pratik yapılabilir.\n\n"

        "**Satranç, strateji ve zihinsel becerileri geliştiren keyifli bir oyundur. Daha fazla bilgi için satranç kitapları veya online kaynaklara göz atabilirsiniz!**"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

@bot.command()
async def yazımkuralları(ctx):
    message = (
        "**Türkçe Yazım Kuralları Hakkında Bilgiler**\n\n"

        "**1. Büyük Harf Kullanımı:**\n"
        "   - Cümlelerin ilk harfi büyük yazılır.\n"
        "   - Özel isimler (kişi, yer, kurum isimleri) büyük harfle başlar. Örnek: Ahmet, İstanbul.\n"
        "   - Kitap, dergi, gazete adları gibi özel isimler büyük harfle başlar. Örnek: Milliyet.\n\n"

        "**2. Noktalama İşaretleri:**\n"
        "   - **Nokta (.)**: Cümle sonlarında kullanılır.\n"
        "   - **Virgül (,)**: Cümle içinde sıralı unsurları ayırmak için kullanılır.\n"
        "   - **Soru İşareti (?)**: Soru cümlelerinin sonunda kullanılır.\n"
        "   - **Ünlem İşareti (!)**: Duygu veya vurgunun belirtildiği cümlelerin sonunda kullanılır.\n"
        "   - **Tırnak İşareti (‘ ’):** Alıntı veya özel ifadelerin belirtildiği yerlerde kullanılır.\n\n"

        "**3. Kelime Ayırma:**\n"
        "   - Bitişik yazılması gereken kelimeler: 'gözlük', 'kitaplık'.\n"
        "   - Ayrı yazılması gereken kelimeler: 'çok fazla', 'birçok'.\n\n"

        "**4. Kısaltmalar:**\n"
        "   - Kısaltmalar büyük harfle yazılır. Örnek: T.C. (Türkiye Cumhuriyeti).\n"
        "   - Kısaltmaların arkasına nokta konulması gereklidir. Örnek: A.B.D. (Amerika Birleşik Devletleri).\n\n"

        "**5. Bitiş Ekleri:**\n"
        "   - Bitiş ekleri, kelimenin sonuna bitişik yazılır. Örnek: kitap+lar = kitaplar.\n"
        "   - -ki, -dır, -dir gibi ekler ayrı yazılmaz. Örnek: doğrudur.\n\n"

        "**6. Yazım Yanlışları:**\n"
        "   - Yanlış yazım: 'bilgisayarım' → Doğru yazım: 'bilgisayarım'.\n"
        "   - Doğru yazım: 'her zaman', 'sadece'.\n\n"

        "**7. Sıfatların Kullanımı:**\n"
        "   - Sıfatlar, tanımladıkları isimlerden önce gelir. Örnek: güzel ev.\n"
        "   - Sıfatların bitişik yazılması gerekir. Örnek: mavi-kırmızı.\n\n"

        "**8. Bağlaçların Yazımı:**\n"
        "   - 've' bağlacı ayrı yazılır. Örnek: 'Ali ve Ayşe'.\n"
        "   - 'ile' bağlacı da ayrı yazılır. Örnek: 'Ahmet ile Mehmet'.\n\n"

        "**9. Sıralama ve Sayılar:**\n"
        "   - Sayılar kelimelerle birlikte yazılacaksa ayrı yazılmalıdır. Örnek: 'beş kitap', 'üç elma'.\n"
        "   - Rakamla yazılan sayılar ile kelimeler arasında nokta veya virgül kullanılır. Örnek: '10, 5'.\n\n"

        "**10. Özel İsimler:**\n"
        "   - Coğrafi terimler büyük harfle başlar. Örnek: 'Anadolu', 'Ege Denizi'.\n"
        "   - Kurum ve kuruluş isimleri de büyük harfle başlar. Örnek: 'Türk Dil Kurumu'.\n\n"

        "**Yazım kuralları, dilin doğru ve etkili kullanılmasını sağlar. Daha fazla bilgi için dil bilgisi kaynaklarına başvurabilirsiniz!**"
    )
    await ctx.send(message)

# Botu çalıştırma
bot.run('TOKEN')


