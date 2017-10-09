## <a name="download-install-and-register-hello-azure-backup-agent"></a>İndirme, yükleme ve hello Azure Yedekleme aracısı kaydedin
Hello Azure yedekleme kasası oluşturduktan sonra bir aracı her yedekleme veri ve uygulamaları sağlayan Windows makinelerinizi (Windows Server, Windows istemci, System Center Data Protection Manager sunucusu veya Azure yedekleme sunucusu makine) yüklü olmalıdır tooAzure.

1. İçinde toohello oturum [Yönetim Portalı](https://manage.windowsazure.com/)
2. Tıklatın **kurtarma Hizmetleri**seçeneğini belirleyip hello yedekleme kasası bir sunucuyla tooregister istiyor. Bu yedekleme kasası için Hello hızlı başlangıç sayfası görüntülenir.
   
    ![Hızlı başlangıç](./media/backup-install-agent/quickstart.png)
3. Merhaba Hello hızlı başlangıç sayfasında, tıklatın **için Windows Server veya System Center Data Protection Manager veya Windows İstemcisi** altında seçeneği **aracıyı indir**. Tıklatın **kaydetmek** toocopy, toohello yerel makine.
   
    ![Aracı Kaydet](./media/backup-install-agent/agent.png)
4. Merhaba Aracısı yüklendikten sonra çift MARSAgentInstaller.exe toolaunch hello yükleme hello Azure yedekleme Aracısı'nın tıklayın. Merhaba yükleme klasörü ve hello aracı için gereken geçici klasörü seçin. Belirtilen hello önbellek konumu hello yedekleme verilerini % 5'en az boş alan olması gerekir.
5. Bir proxy sunucu tooconnect toohello kullanırsanız, internet ' hello **Proxy Yapılandırması** ekranında, hello proxy sunucusu ayrıntılarını girin. Doğrulanmış bir proxy kullanıyorsanız, bu ekranda hello kullanıcı adı ve parola bilgilerinizi girin.
6. (Bu zaten mevcut değilse) hello Azure Yedekleme aracısı, .NET Framework 4.5 ve Windows PowerShell toocomplete hello yükleme yükler.
7. Merhaba Aracısı yüklendikten sonra hello tıklatın **tooRegistration devam** hello iş akışıyla düğmesi toocontinue.
   
   ![Kaydolma](./media/backup-install-agent/register.png)
8. Merhaba kasa kimlik bilgilerini ekranda, daha önce indirilen tooand select hello kasa kimlik bilgileri dosyası göz atın.
   
    ![Kasa kimlik bilgileri](./media/backup-install-agent/vc.png)
   
    Merhaba kasa kimlik bilgileri dosyası yalnızca 48 için geçerlidir (Merhaba portalından yüklendikten sonra) saat. Bu ekran ("dosya süresi doldu örneğin kasa kimlik bilgileri sağlandı") içinde herhangi bir hatayla karşılaşırsanız, oturum açma toohello Azure portal ve indirme hello kasa kimlik bilgileri dosyasını yeniden.
   
    Merhaba Kurulum uygulama tarafından erişilebilen bir konumda bu hello kasa kimlik bilgileri dosyası kullanılabilir olduğundan emin olun. Karşılaşırsanız ilgili hatalar erişim, bu makinede hello kasa kimlik bilgileri dosyası tooa geçici konuma kopyalayın ve hello işlemi yeniden deneyin.
   
    Geçersiz kasa kimlik bilgileri hata ("Örneğin geçersiz kasa kimlik bilgileri sağlandı") karşılaşırsanız hello dosya bozuk veya mu sahip hello yeni kimlik ilişkilendirilmemiş hello kurtarma hizmeti ile. Yeni bir kasa kimlik bilgileri dosyası hello portalından indirme hello işlemi yeniden deneyin. Bu hata genellikle Hello kullanıcı üzerinde hello tıklarsa görülür **indirme kasa kimlik bilgileri** hello Azure portalında, art arda seçeneği. Bu durumda, yalnızca hello ikinci kasa kimlik bilgilerini geçerli değil.
9. Merhaba, **şifreleme ayarı** ekran, bir parola oluşturabilir veya bir parola (en fazla 16 karakter) girin. Güvenli bir yerde toosave hello parolayı unutmayın.
   
    ![Şifreleme](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Merhaba, parola kaybolur veya unutulursa; Microsoft, hello yedekleme verilerini kurtarmak yardımcı olamaz. Merhaba son kullanıcı hello şifreleme parolası sahibi ve Microsoft hello son kullanıcı tarafından kullanılan hello parola görünürlüğe sahip değil. Lütfen bir kurtarma işlemi sırasında gerekli olduğu gibi hello dosyayı güvenli bir konuma kaydedin.
   > 
   > 
10. Merhaba tıkladığınızda **son** düğmesini tıklatın, hello makine başarıyla kaydettirildi toohello kasası ve olduğunuzda artık Azure tooMicrosoft yedekleme hazır toostart.
11. Microsoft Azure yedekleme tek başına kullanırken üzerinde hello tıklayarak hello kayıt iş akışı sırasında belirtilen hello ayarlarını değiştirebilir **özelliklerini değiştirme** hello Azure Backup mmc ek bileşeninde seçeneği.
    
    ![Özelliklerini değiştir](./media/backup-install-agent/change.png)
    
    Alternatif olarak, veri koruma Yöneticisi'ni kullanırken hello tıklayarak hello kayıt iş akışı sırasında belirtilen hello ayarları değiştirebileceğiniz **yapılandırma** seçerek seçeneği **çevrimiçi** hello altında **Yönetim** sekmesi.
    
    ![Azure Yedekleme'yi yapılandırın](./media/backup-install-agent/configure.png)

