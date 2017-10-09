Bu adımları tooinstall izleyin ve MongoDB Windows Server çalıştıran bir sanal makinede çalıştırın.

> [!IMPORTANT]
> Kimlik doğrulaması ve IP adresi bağlama gibi MongoDB güvenlik özellikleri varsayılan olarak etkin değildir. Güvenlik özellikleri, MongoDB tooa üretim ortamına dağıtmadan önce etkinleştirilmelidir.  Daha fazla bilgi için bkz: [güvenlik ve kimlik doğrulama](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Uzak Masaüstü kullanarak toohello sanal makineye bağlandıktan sonra Internet Explorer hello açın **Başlat** hello sanal makine menüsünde.
2. Select hello **Araçları** hello sağ üst köşesindeki düğmesini.  İçinde **Internet Seçenekleri**seçin hello **güvenlik** sekmesini tıklatın ve ardından hello seçin **Güvenilen siteler** simgesi ve son olarak hello tıklayın **siteleri** düğme. Ekleme *https://\*. mongodb.org* Güvenilen siteler toohello listesi.
3. Çok Git[yüklemeleri - MongoDB](https://www.mongodb.com/download-center#community).
4. Hello bulur **geçerli durağan sürümü** , **Community Server**seçin hello son **64-bit** hello Windows sütununda sürümü. Karşıdan yükle ve hello MSI yükleyicisi çalıştırın.
5. MongoDB genellikle C:\Program Files\MongoDB yüklenir. İçin ortam değişkenleri hello masaüstünde arayın ve hello MongoDB ikili dosyalarının yolu toohello PATH değişkeni ekleyin. Örneğin, C:\Program Files\MongoDB\Server\3.4\bin hello ikili dosyaları makinenizde bulabilirsiniz.
6. MongoDB veri ve günlük dizinleri hello veri diski oluşturma (sürücü gibi **F:**) adımları önceki hello oluşturuldu. Gelen **Başlat**seçin **komut istemi** tooopen bir komut istemi penceresi.  Şunu yazın:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun hello veritabanı, çalıştırın:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Tüm günlük iletilerini yönlendirilmiş toohello olan *F:\MongoLogs\mongolog.log* dosya mongod.exe sunucu başlar ve günlük dosyalarını preallocates gibi. Merhaba günlük dosyaları MongoDB toopreallocate için birkaç dakika sürer ve bağlantıları dinlemeyi Başlat. MongoDB örneğinizin çalışırken hello komut istemi bu görevde odaklanmış kalır.
8. toostart hello MongoDB yönetim kabuğunu açın başka bir komut penceresinde **Başlat** ve türü hello aşağıdaki komutlar:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    Merhaba veritabanı hello Ekle tarafından oluşturulur.
9. Alternatif olarak, bir hizmet olarak mongod.exe yükleyebilirsiniz:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Bir hizmeti yüklendi "Mongo VT" açıklaması ile MongoDB adlı. Merhaba `--logpath` seçeneği kullanılan toospecify bir günlük dosyası olması gerekir, bu yana hello hizmetini çalıştıran bir komut penceresinde toodisplay çıktısı yok.  Merhaba `--logappend` seçeneği belirtir hello hizmetinin yeniden başlatma çıkış tooappend toohello mevcut günlük dosyası neden olur.  Merhaba `--dbpath` seçeneği hello hello veri dizininin konumunu belirtir. Daha fazla hizmeti ile ilgili komut satırı seçenekleri için bkz [hizmeti ile ilgili komut satırı seçenekleri][MongoWindowsSvcOptions].

    toostart hello hizmeti, şu komutu çalıştırın:

        C:\> net start MongoDB
10. Böylece MongoDB yüklü ve çalışan, tooopen bir bağlantı noktası Windows Güvenlik Duvarı'nda gereksinim tooMongoDB uzaktan bağlanabilirsiniz.  Merhaba gelen **Başlat** menüsünde, select **Yönetimsel Araçlar** ve ardından **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**.
11. bir) Merhaba sol bölmesinde seçin **gelen kuralları**.  Merhaba, **Eylemler** bölmesinde sağ hello select **yeni kural...** .

    ![Windows Güvenlik Duvarı][Image1]

    b) içinde hello **yeni gelen kuralı Sihirbazı**seçin **bağlantı noktası** ve ardından **sonraki**.

    ![Windows Güvenlik Duvarı][Image2]

    c) select **TCP** ve ardından **belirli yerel bağlantı noktaları**.  ' I tıklatın ve "27017" (MongoDB dinlediği hello varsayılan bağlantı noktası) bir bağlantı noktası belirtin **sonraki**.

    ![Windows Güvenlik Duvarı][Image3]

    d) select **hello bağlantıya izin verme** tıklatıp **sonraki**.

    ![Windows Güvenlik Duvarı][Image4]

    e) tıklatın **sonraki** yeniden.

    ![Windows Güvenlik Duvarı][Image5]

    f) "MongoPort" gibi hello kuralı için bir ad belirtin ve tıklayın **son**.

    ![Windows Güvenlik Duvarı][Image6]

12. Merhaba sanal makineyi oluşturduğunuzda MongoDB için bir uç nokta yapılandırmadıysanız, bunu şimdi yapabilirsiniz. Merhaba güvenlik duvarı kuralı ve hello uç nokta toobe mümkün tooconnect tooMongoDB uzaktan ihtiyacınız var.

  Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)**, yeni bir sanal makine hello adına tıklayın ve ardından **uç noktaları**.

    ![Uç Noktalar][Image7]

13. **Ekle**'ye tıklayın.

14. Protokol "Mongo" adında bir uç nokta ekleyin **TCP**, her ikisi **ortak** ve **özel** bağlantı noktaları kümesi "27017" çok. Bu bağlantı noktası açmak, MongoDB toobe uzaktan erişim sağlar.

    ![Uç Noktalar][Image9]

> [!NOTE]
> başlangıç bağlantı noktası 27017 MongoDB tarafından kullanılan hello varsayılan bağlantı noktasıdır. Bu varsayılan bağlantı noktası hello belirterek değiştirebileceğiniz `--port` hello mongod.exe sunucu başlatırken parametresi. Merhaba Güvenlik Duvarı'nda aynı bağlantı noktası numarası hello ve yönergeleri önceki hello "Mongo" uç hello emin toogive olun.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
