## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Kasa kimlik bilgileri tooauthenticate hello Azure Backup hizmeti ile kullanma
Merhaba şirket içi sunucu (Windows İstemcisi veya Windows Server veya Data Protection Manager sunucu) toobe veri tooAzure yedekleyebilirsiniz önce bir yedekleme kasası ile kimlik doğrulaması gerekir. Merhaba kimlik doğrulaması, "kimlik bilgileri kasası" kullanılarak gerçekleştirilir. Kasa kimlik bilgileri Hello kavramı benzer toohello Azure PowerShell ile kullanılan bir "yayımlama ayarları" dosyasının kavramdır.

### <a name="what-is-hello-vault-credential-file"></a>Merhaba kasa kimlik bilgileri dosyası nedir?
Merhaba kasa kimlik bilgileri dosyası, her bir yedekleme kasası için hello portal tarafından oluşturulan bir sertifikadır. Merhaba portal sonra hello ortak anahtar toohello erişim denetimi Hizmeti'nden (ACS) yükler. Merhaba sertifikasının özel anahtarı Hello kullanılabilir toohello kullanıcı bir giriş hello makine kayıt iş akışı olarak belirtilmiş olan hello iş akışının parçası olarak yapılır. Bu hello makine toosend yedekleme verilerini tanımlanan tooan kasaya hello Azure Backup hizmeti kimliğini doğrular.

Merhaba kasa kimlik bilgileri yalnızca hello kayıt iş akışı sırasında kullanılır. Kasa kimlik bilgileri dosyasının gizliliğinin tehlikeye hello hello kullanıcının sorumluluk tooensure olur. Bir kullanıcının hello elinizde kalırsa hello kasa kimlik bilgileri dosyası diğer makinelere karşı kullanılan tooregister olabilir hello aynı kasası. Merhaba yedekleme verilerini toohello müşteriye ait olan bir parola kullanılarak şifrelenir gibi ancak var olan yedekleme verilerinin gizliliği tehlikeye giremez. toomitigate bu sorunu kasa kimlik bilgileri 48hrs tooexpire ayarlanır. Kez – herhangi bir sayıda yedekleme kasası hello kasa kimlik bilgilerini yükleyebilirsiniz, ancak yalnızca hello son kasa kimlik bilgilerini hello kayıt iş akışı sırasında geçerlidir.

### <a name="download-hello-vault-credential-file"></a>Merhaba kasa kimlik bilgilerini indirin
Merhaba kasa kimlik bilgilerini hello Azure portal güvenli bir kanaldan aracılığıyla yüklenir. Hello Azure Backup hizmeti hello sertifikasının özel anahtarı Merhaba farkında değildir ve hello özel anahtarı hello portalı veya hello hizmetinde kalıcı yapılmaz. Aşağıdaki adımları toodownload hello kasa kimlik bilgileri dosyası tooa yerel makine hello kullanın.

1. İçinde toohello oturum [Yönetim Portalı](https://manage.windowsazure.com/)
2. Tıklayın **kurtarma Hizmetleri** hello sol gezinti bölmesinde ve hangi oluşturduğunuz select hello yedekleme kasası. Merhaba bulut simgesi tooget toohello üzerinde hello yedekleme kasası görünümü Hızlı Başlangıç'ı tıklatın.
   
   ![Hızlı Bakış](./media/backup-download-credentials/quickview.png)
3. Merhaba hızlı başlangıç sayfasında, tıklatın **indirme kasa kimlik bilgileri**. Merhaba portal indirme için kullanılabilir hale hello kasa kimlik bilgilerini oluşturur.
   
   ![İndir](./media/backup-download-credentials/downloadvc.png)
4. Merhaba portal hello kasa adı ve hello geçerli tarih kullanan bir kasa kimlik bilgisi oluşturur. Tıklatın **kaydetmek** toodownload hello kasa kimlik bilgileri toohello Yerel hesabın indirmeleri klasör ya da hello Farklı Kaydet'i seçin hello kasa kimlik bilgileri için bir konum menü toospecify kaydedin.

### <a name="note"></a>Not
* Merhaba kasa kimlik bilgileri makinenizden erişilebilen bir konuma kaydedildiğinden emin olun. Bir dosya paylaşımı/SMB depolanıyorsa hello erişim izinlerini denetleyin.
* Merhaba kasa kimlik bilgileri dosyası yalnızca hello kayıt iş akışı sırasında kullanılır.
* Merhaba kasa kimlik bilgileri dosyası 48hrs sonra süresi dolar ve hello portalından indirilebilir.
* Azure Backup toohello başvuran [SSS](../articles/backup/backup-azure-backup-faq.md) hello iş akışındaki herhangi bir sorunuz için.

