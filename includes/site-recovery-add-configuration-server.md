1. Merhaba birleşik Kurulum yükleme dosyasını çalıştırın.
2. İçinde **başlamadan önce**seçin **yükleme hello yapılandırma sunucusu ve işlem sunucusu**.

    ![Başlamadan önce](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. İçinde **üçüncü taraf yazılım lisansı**, tıklatın **kabul ediyorum** toodownload ve MySQL yükleme.

    ![Üçüncü taraf yazılım](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. İçinde **kayıt**seçin hello kasadan indirdiğiniz hello kayıt anahtarı.

    ![Kayıt](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. İçinde **Internet ayarlarını**, nasıl hello yapılandırma sunucusunda çalışan sağlayıcı üzerinden Site Recovery tooAzure bağlanır hello hello Internet belirtin.

   a. Şu anda hello makinede ayarlanır hello proxy ile tooconnect istiyorsanız seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.

   b. Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **tooAzure Site Recovery bir proxy sunucu olmadan doğrudan bağlan**.

   c. Merhaba mevcut proxy kimlik doğrulaması gerektiriyorsa veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız seçin **özel proxy ayarlarıyla Bağlan**.

     * Özel bir ara sunucu kullanırsanız, toospecify başlangıç adresi, bağlantı noktası ve kimlik bilgileri gerekir.
     * Bir proxy sunucu kullanıyorsanız, zaten açıklanan hello URL'lere izin [Önkoşullar](#prerequisites).

     ![Güvenlik duvarı](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. İçinde **Önkoşul denetimi**, Kurulum yükleme çalışabildiğinden emin bir onay toomake çalıştırılır. Merhaba hakkında bir uyarı görünürse **genel zaman eşitleme denetimi**, hello bundan hello sistem saati doğrulayın (**tarih ve saat** ayarları) olan hello aynı hello saat dilimi.

    ![Ön koşullar](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. İçinde **MySQL yapılandırma**, yüklü olan toohello MySQL server örneğinde günlüğe kaydetme için kimlik bilgileri oluşturun.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. İçinde **ortam ayrıntıları**tooreplicate VMware Vm'lerini oluşturacağız olup olmadığını seçin. Varsa, Kurulum Powerclı 6.0 yüklü olduğunu denetler.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. İçinde **yükleme konumu**burada tooinstall hello ikili dosyaları istediğiniz ve hello önbellek depolamak seçin. Seçtiğiniz hello sürücü en az 5 GB kullanılabilir disk alanı olması gerekir, ancak en az 600 GB boş alana sahip bir önbellek sürücüsü kullanmanızı öneririz.

    ![Yükleme konumu](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. İçinde **Ağ Seçimi**, hangi hello yapılandırma sunucusu gönderir hello dinleyicisini (ağ bağdaştırıcısı ve SSL bağlantı noktası) belirtin ve çoğaltma verileri alan. Bağlantı noktası 9443, göndermek ve çoğaltma trafiğini almak için kullanılan hello varsayılan bağlantı noktası olmakla birlikte, ortam gereksinimleri Bu bağlantı noktası numarası toosuit değiştirebilirsiniz. Toplama toohello bağlantı 9443, biz de bir web sunucusu tooorchestrate çoğaltma işlemleri tarafından kullanılan bağlantı noktası 443'ü açın. Bağlantı noktası 443 gönderirken ya da çoğaltma trafiğini alırken için kullanmayın.

    ![Ağ seçimi](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. İçinde **Özet**, hello bilgileri gözden geçirin ve tıklayın **yükleme**. Yükleme tamamlandığında bir parola oluşturulur. Çoğaltmayı etkinleştirdiğinizde bu parola gerekli olacaktır; bu yüzden kopyalayıp güvenli bir yerde saklayın.

    ![Özet](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Kayıt tamamlandıktan sonra hello sunucu üzerinde hello görüntülenir **ayarları** > **sunucuları** dikey penceresinde hello kasası.
