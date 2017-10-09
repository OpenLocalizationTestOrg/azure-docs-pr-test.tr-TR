<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd StorSimple 8000 serisi güncelleştirme 1.0 depolama hesabı
1. Merhaba StorSimple Yöneticisi hizmet giriş sayfasında hizmetinizi seçin ve çift tıklayın. Bu toohello sürecek **Hızlı Başlangıç** sayfası. Select hello **yapılandırma** sayfası.
2. **Depolama hesabı ekleyin/düzenleyin**’e tıklayın.
3. Merhaba, **depolama hesabı Ekle/Düzenle** iletişim kutusu, tıklatın **yeni Ekle**.
4. Merhaba, **sağlayıcı** alanında, select hello uygun bulut hizmeti sağlayıcısı. desteklenen hello sağlayıcılarıdır Azure, Amazon S3, Amazon S3 RRS, HP ve Openstack'tir. Merhaba kimlik bilgilerini ve hello depolama hesabıyla, bulut hizmet sağlayıcılarının ilişkili hello konumunu belirtin. kimlik bilgileri için sunulan hello alanları belirttiğiniz hello bulut hizmeti sağlayıcısına bağlı olarak farklı olacaktır. 
   
   * Azure bulut hizmeti sağlayıcısı olarak seçtiyseniz, hello tedarik **adı** ve hello birincil **erişim tuşu** Microsoft Azure depolama hesabınız için. Bir Azure hesabı için başlangıç konumu otomatik olarak doldurulur.
     
        ![Azure depolama hesabı ekleme](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Amazon S3 veya Amazon S3-RRS seçtiyseniz, kullanımı kolay bir **Depolama Hesabı adı**, **Erişim Tuşu** ve **Gizli Anahtar** verin. Amazon S3 ve Amazon S3-rrs için aşağıdaki konumlardan hello desteklenir:
     
     * ABD Standart
     * ABD Batı (Oregon)
     * ABD Batı (Kuzey California)
     * AB (İrlanda)
     * Asya Pasifik (Singapur)
     * Asya Pasifik (Sidney)
     * Asya Pasifik (Tokyo)
     * Güney Amerika (Sao Paulo)
       
       ![Amazon depolama hesabı ekleme](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Bulut hizmeti sağlayıcısı olarak HP seçtiyseniz, kullanımı kolay bir **Depolama Hesabı adı**, **Kiracı Kimliği**, **Kullanıcı Adı** ve **Parola** verin. HP için aşağıdaki konumlardan hello desteklenir:
     
     * ABD Doğu
     * ABD Batı
       
       ![HP depolama hesabı ekleme](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Bulut hizmet sağlayıcısı olarak **Openstack** seçtiyseniz bir **Konak Adı**, **Erişim Tuşu** ve **Gizli Anahtar** verin.
     
     > [!NOTE]
     > Azure dışında tüm hello bulut hizmeti sağlayıcıları için kolay bir ad izin verilir. Kullanımı kolay farklı adlar kullanın ve aynı kimlik bilgilerini ayarla hello ile birden fazla depolama hesabı oluşturun.
     > 
     > 
     
        ![Openstack depolama hesabı ekleme](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Seçin **SSL modunu etkinleştir** toocreate cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal. Clear hello **SSL modunu etkinleştir** yalnızca özel bir bulutta işlem yapıyorsanız kutuyu.
   
   > [!NOTE]
   > Sağlayıcınız olarak HP kullanıyorsanız SSL her zaman etkin olacaktır.
   > 
   > 
6. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Merhaba depolama hesabı başarıyla oluşturulduktan sonra size bildirilecek.
7. Yeni depolama hesabı oluşturuldu hello hello üzerinde gösterileceği **yapılandırma** altında sayfa **depolama hesapları**. Tıklatın **kaydetmek** toosave hello yeni depolama hesabı. Onayınız istendiğinde **Tamam**’a tıklayın.

