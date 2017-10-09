1. Hello Azure Site kurtarma UnifiedSetup.exe başlatma
2. İçinde **başlamadan önce**seçin **ek işlem sunucuları tooscale dağıtım çıkışı eklemek**.

  ![İşlem sunucusu ekleme](./media/site-recovery-add-process-server/ps-page-1.png)

3. İçinde **yapılandırma sunucusu ayrıntılarını**hello hello yapılandırma sunucusu IP adresini belirtin ve parola hello.

  ![İşlem sunucusu ekleme 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. İçinde **Internet ayarlarını**, nasıl hello yapılandırma sunucusu üzerinde çalışan sağlayıcı üzerinden Site Recovery tooAzure bağlanır hello hello Internet belirtin.

  ![İşlem sunucusu ekleme 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Şu anda hello makinede ayarlanır hello proxy ile tooconnect istiyorsanız seçin **var olan ara sunucu ayarlarıyla Bağlan**.
   * Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **bir proxy sunucu olmadan doğrudan bağlan**.
   * Merhaba mevcut proxy kimlik doğrulaması gerektiriyorsa veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız seçin **özel proxy ayarlarıyla Bağlan**.

     * Özel bir ara sunucu kullanırsanız, toospecify başlangıç adresi, bağlantı noktası ve kimlik bilgileri gerekir.
     * Bir proxy sunucu kullanıyorsanız, zaten izin erişim toohello hizmeti URL'leri.

5. İçinde **Önkoşul denetimi**, Kurulum yükleme çalışabildiğinden emin bir onay toomake çalıştırılır. Merhaba hakkında bir uyarı görünürse **genel zaman eşitleme denetimi**, hello bundan hello sistem saati doğrulayın (**tarih ve saat** ayarları) olan hello aynı hello saat dilimi.

     ![İşlem sunucusu ekleme 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. İçinde **ortam ayrıntıları**tooreplicate VMware Vm'lerini oluşturacağız olup olmadığını seçin. Çoğaltacaksanız, kurulum PowerCLI 6.0’ın yüklü olup olmadığını denetler.

     ![İşlem sunucusu ekleme 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. İçinde **yükleme konumu**burada tooinstall hello ikili dosyaları istediğiniz ve hello önbellek depolamak seçin. Seçtiğiniz hello sürücü en az 5 GB kullanılabilir disk alanı olması gerekir, ancak en az 600 GB boş alana sahip bir önbellek sürücüsü kullanmanızı öneririz.
     ![İşlem sunucusu ekleme 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. İçinde **Ağ Seçimi**, hangi hello yapılandırma sunucusu gönderir hello dinleyicisini (ağ bağdaştırıcısı ve SSL bağlantı noktası) belirtin ve çoğaltma verileri alan. Bağlantı noktası 9443, göndermek ve çoğaltma trafiğini almak için kullanılan hello varsayılan bağlantı noktası olmakla birlikte, ortam gereksinimleri Bu bağlantı noktası numarası toosuit değiştirebilirsiniz. Toplama toohello bağlantı 9443, biz de bir web sunucusu tooorchestrate çoğaltma işlemleri tarafından kullanılan bağlantı noktası 443'ü açın. Bağlantı noktası 443’ü çoğaltma trafiği göndermek veya almak için kullanmayın.

     ![İşlem sunucusu ekleme 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. İçinde **Özet**, hello bilgileri gözden geçirin ve tıklayın **yükleme**. Yükleme tamamlandığında bir parola oluşturulur. Çoğaltmayı etkinleştirdiğinizde bu parola gerekli olacaktır; bu yüzden kopyalayıp güvenli bir yerde saklayın.

     ![İşlem sunucusu ekleme 7](./media/site-recovery-add-process-server/ps-page-8.png)
