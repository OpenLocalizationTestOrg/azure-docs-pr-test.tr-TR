<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>1. adım: bir aygıt toochange hello hizmeti veri şifreleme anahtarını hello Klasik Azure portalı, yetkilendirme
Genellikle, hello Aygıt Yöneticisi bu hello Hizmet Yöneticisi bir cihaz toochange hizmeti veri şifreleme anahtarları yetkilendirmek ister. Merhaba Hizmet Yöneticisi ardından hello aygıt toochange hello anahtarı yetkilendirecek.

Bu adım hello Klasik Azure portalı gerçekleştirilir. Merhaba Hizmet Yöneticisi bir cihaz yetkili uygun toobe hello cihazlar görüntülenen listesinden seçebilirsiniz. yetkili toostart hello hizmet verileri şifreleme anahtarı değiştirin ardından işlem hello aygıttır.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Hangi cihazların olabilir toochange hizmeti veri şifreleme anahtarları yetkili?
Bir aygıt hello yetkili tooinitiate hizmeti veri şifreleme anahtarı değişiklikleri kullanılabilmesi için öncelikle aşağıdaki ölçütleri karşılamalıdır:

* Merhaba cihaz çevrimiçi toobe hizmeti veri şifreleme anahtarı değişiklik yetkilendirme için uygun olmalıdır.
* Aynı aygıt yeniden 30 dakika sonra hello anahtar değiştirirseniz değil başlatıldı hello yetki verebilir.
* Merhaba anahtar değişikliği hello daha önceden yetkili aygıt tarafından başlatılmamış olması koşuluyla farklı bir cihaz yetki verebilir. Merhaba yeni cihaz yetkilendirildikten sonra hello eski aygıt hello değişiklik başlatamaz.
* Merhaba hizmet verileri şifreleme anahtarı Hello geçişi işlemi devam ederken bir aygıtı yetkilendirilemiyor.
* Başkalarının olmamasına karşın bazı hello hizmetine kayıtlı hello cihazların Merhaba şifrelemeyi gezinirken bir aygıtı yetki verebilir. Böyle durumlarda, hello uygun hello hello hizmet verileri şifreleme anahtarı değişikliği tamamladınız olanları aygıtlardır.

> [!NOTE]
> Hello Klasik Azure portalı, StorSimple sanal cihaz hello olabilir aygıtlar listesinde gösterilmez toostart hello anahtar değişikliği yetkili.
> 
> 

Adımları tooselect aşağıdaki hello gerçekleştirmek ve bir cihaz tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği yetkisi verin.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize aygıt toochange hello anahtarı
1. Merhaba hizmet panosu sayfasında, tıklatın **değişiklik hizmeti veri şifreleme anahtarı**.
   
    ![Değişiklik hizmeti şifreleme anahtarı](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. Merhaba, **değişiklik hizmeti veri şifreleme anahtarı** iletişim kutusunda, seçin ve bir cihaz tooinitiate hello hizmet verileri şifreleme anahtarı değişikliğe izin vermek. Merhaba aşağı açılan liste yetkilendirilebilir tüm hello uygun aygıtı yok.
3. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>2. adım: StorSimple tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği için Windows PowerShell'i kullanın
StorSimple cihaz StorSimple hello arabirimde yetkili için bu adımı Windows PowerShell hello gerçekleştirilir.

> [!NOTE]
> Merhaba anahtar geçişi tamamlanana kadar hiçbir işlem Merhaba, StorSimple Yöneticisi hizmetiniz, Klasik Azure portalı gerçekleştirilebilir.
> 
> 

Merhaba cihaz seri Konsolu tooconnect toohello Windows PowerShell arabirimini kullanıyorsanız, hello aşağıdaki adımları gerçekleştirin.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello hizmet verileri şifreleme anahtarı değiştirme
1. Seçenek 1 toolog tam erişimle seçin.
2. Merhaba komut satırına aşağıdakini yazın:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Merhaba cmdlet'i başarıyla tamamlandıktan sonra yeni bir hizmet verileri şifreleme anahtarı alır. Kopyalayın ve bu anahtarı kullanmak için bu işlem 3. adımında kaydedin. Bu anahtar olacaktır hello StorSimple Yöneticisi hizmetine kayıtlı cihazlar kalan tüm hello tooupdate kullanılır.
   
   > [!NOTE]
   > Bu işlem, StorSimple cihaz yetkilendirme dört saat içinde başlatılmalıdır.
   > 
   > 
   
   Bu yeni anahtar hello hizmetine kayıtlı toohello gönderilen toobe tooall hello cihazları hizmetten daha sonra gönderilir. Bir uyarı sonra hello hizmet panosunda görüntülenir. Hello hizmet hello kayıtlı cihazlarda tüm hello işlemleri devre dışı bırakır ve hello Aygıt Yöneticisi ardından diğer cihazları tooupdate hello hizmeti veri şifreleme anahtarını hello gerekir. Ancak, hello g/ç (ana bilgisayar veri toohello bulut gönderme) kesilmiş olabilir değil.
   
   Tek bir cihazı kayıtlı tooyour hizmet varsa hello geçiş işlemi tamamlanmıştır ve hello sonraki adımı atlayabilirsiniz. Birden çok aygıtları kayıtlı tooyour hizmetiniz varsa, toostep 3 devam edin.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>3. adım: hello hizmet verileri şifreleme anahtarı başka StorSimple cihazlar üzerinde güncelleştir
Birden çok aygıtları kayıtlı tooyour StorSimple Yöneticisi hizmetiniz varsa bu adımları hello Windows PowerShell arabiriminde StorSimple Cihazınızı gerçekleştirilmesi gerekir. 2. adımda elde ettiğiniz hello anahtarı: StorSimple tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği için Windows PowerShell'i kullanın kullanılan tooupdate tüm hello kalan StorSimple cihaz StorSimple Yöneticisi hizmeti hello ile kayıtlı olması gerekir.

Adımları tooupdate hello hizmet verileri şifreleme aygıtınızda aşağıdaki hello gerçekleştirin.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello hizmet verileri şifreleme anahtarı
1. Windows PowerShell için StorSimple tooconnect toohello konsolunu kullanın. Seçenek 1 toolog tam erişimle seçin.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Makalesinde aldığınız hello hizmet verileri şifreleme anahtarı sağlayan [2. adım: StorSimple tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği için Windows PowerShell'i kullanın](#to-initiate-the-service-data-encryption-key-change).

