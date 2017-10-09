#### <a name="toocreate-a-cloud-appliance"></a>toocreate bulut uygulaması

1. Toohello Hello Azure portal, Git **StorSimple Aygıt Yöneticisi'ni** hizmet.
2. Toohello Git **aygıtları** dikey. Merhaba hizmet Özet dikey penceresinde Hello komut çubuğu'ndan tıklatın **oluşturma bulut uygulaması**.
    ![StorSimple bulut gereci oluşturma](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. Merhaba, **oluşturma bulut uygulaması** dikey penceresinde, aşağıdaki ayrıntılara hello belirtin.
   
    ![StorSimple bulut gereci oluşturma](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Ad**: Bulut gereciniz için benzersiz bir ad.
   2. **Model** -hello bulut uygulaması hello modelini seçin. 8010 cihazlar 30 TB Standart Depolama sunarken 8020 cihazlar 64 TB Premium Depolama sunar. 8010 toodeploy öğe düzeyinde alma senaryolarını yedeklerden belirtin. 8020 toodeploy yüksek performans, düşük gecikme iş yükleri, seçin veya olağanüstü durum kurtarma için ikincil cihaz olarak kullanın.
   3. **Sürüm** -hello bulut uygulaması hello sürümünü seçin. Merhaba sürüm kullanılan toocreate hello bulut uygulaması hello sanal disk görüntüsü toohello sürümüne karşılık gelir. Hello hello bulut sürümü hangi fiziksel Gereci belirler yük devri veya kopyası cihaza olmasından hello bulut uygulaması uygun bir sürümünü oluşturmanız önemlidir.
   4. **Sanal ağ** – bu bulut uygulaması ile toouse istediğiniz bir sanal ağ belirtin. Premium Storage kullanıyorsanız, Premium depolama hesabı hello ile desteklenen bir sanal ağ seçmelisiniz. Desteklenmeyen hello sanal ağlar hello açılan listede gri görünür. Desteklenmeyen bir sanal ağı seçerseniz bir uyarı alırsınız.
   5. **Alt ağ** -hello sanal ağı seçili temel alarak, hello açılır listeden ilişkili hello alt ağları görüntüler. Bir alt ağ tooyour bulut uygulaması atayın.
   6. **Depolama hesabı** – sağlama sırasında hello bulut uygulaması bir depolama hesabı toohold hello yansımasını seçin. Bu depolama hesabını hello olmalıdır hello bulut uygulaması ve sanal ağ ile aynı bölgeye. Bu veri depolama için hello fiziksel veya hello bulut uygulaması tarafından kullanılmamalıdır. Varsayılan olarak, bu amaca yönelik olarak yeni bir depolama hesabı oluşturulur. Ancak, bu kullanım için uygun bir depolama hesabı zaten olduğunu biliyorsanız, bunu hello listesinden seçebilirsiniz. Premium bulut uygulaması oluşturuyorsanız, hello açılır listeden Premium Storage hesapları yalnızca görüntüler.
      
      > [!NOTE]
      > Merhaba bulut uygulaması yalnızca hello Azure storage hesaplarıyla çalışabilir.
    
   7. Merhaba bulut uygulaması üzerinde depolanan hello verilerin Microsoft Veri merkezinde barındırılır anlamak hello onay kutusunu tooindicate seçin.
       * Yalnızca bir fiziksel cihaz kullandığınızda, şifreleme anahtarınızın cihazınızla tutulur; Bu nedenle, Microsoft şifresini çözemez.

       * Bulut uygulaması kullandığınızda hello şifreleme anahtarını ve hello şifre çözme anahtarı Microsoft Azure'da depolanır. Daha fazla bilgi edinmek için bkz. [bulut gereci kullanımıyla ilgili güvenlik konuları](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Tıklatın **oluşturma** tooprovision hello bulut uygulaması. Merhaba aygıt sağlanan yaklaşık 30 dakika toobe sürebilir. Merhaba bulut uygulaması başarıyla oluşturulduğunda size bildirilir. TooDevices dikey penceresine gidin ve toodisplay hello bulut uygulaması cihazların Merhaba listesini yeniler. Merhaba Gereci Hello durumudur **yukarı tooset hazır**.
      
      ![StorSimple bulut uygulaması hazır tooset ayarlama](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

