#### <a name="toocreate-a-virtual-device"></a>toocreate sanal cihazı
1. Toohello Hello Azure portal, Git **StorSimple Yöneticisi** hizmet.
2. Toohello Git **aygıtları** sayfası. Tıklatın **sanal cihaz Oluştur** hello hello sonundaki **aygıtları** sayfası.
3. Merhaba, **sanal cihaz Oluştur iletişim kutusu**, aşağıdaki ayrıntılara hello belirtin.
   
    ![StorSimple sanal cihaz oluşturma](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Ad** – sanal cihazınız için benzersiz bir ad.
   2. **Model** -hello sanal aygıt hello modelini seçin. Bu alan, yalnızca Update 2 veya sonraki bir sürümünü çalıştırıyorsanız kullanılabilir. 8010 cihaz modeli 30 TB Standart Depolama sunarken 8020 modeliyse 64 TB Premium Storage sunar. 8010’u belirtin
   3. toodeploy öğe düzeyinde alma senaryolarını yedeklerden. 8020 toodeploy yüksek performanslı seçin, düşük gecikme iş yükleri veya olağanüstü durum kurtarma için ikincil cihaz olarak kullanılır.
   4. **Sürüm** -hello hello sanal cihazın sürümünü seçin. 8020 cihaz modeli seçiliyse sürüm alanı hello toohello kullanıcı sunulmaz. Bu seçenek eksik tüm fiziksel hello varsa bu hizmetle kaydedilen cihazlar güncelleştirme 1 (veya sonrası) çalıştırıyor. Bu alan yalnızca güncelleştirme öncesi 1 karışımı varsa ve güncelleştirme 1 fiziksel cihazların kayıtlı hello ile aynı sunulan hizmet. Hello hello sanal cihazın sürümünü yapabilecekleriniz hangi fiziksel cihazın belirleyecek devredileceğini veya buradan kopyalanacağını, onu hello sanal cihazın uygun bir sürümünü oluşturmanız önemlidir. Seçin:
      
      * Version Update 0.3, Update 0.3 veya önceki sürümleri çalıştıran fiziksel cihazdan devrederseniz veya DR. 
      * Version Update 1, Update 1 (veya sonraki sürümler) çalıştıran fiziksel cihazdan devrederseniz veya kopyalarsınız. 
   5. **Sanal ağ** – bu sanal cihazla toouse istediğiniz bir sanal ağ belirtin. Premium Storage (Update 2 veya sonraki sürümler) kullanılıyorsa, Premium depolama hesabı hello ile desteklenen bir sanal ağ seçmelisiniz. Desteklenmeyen hello sanal ağlar hello açılan listede gri olacaktır. Desteklenmeyen sanal ağ seçerseniz bir uyarı alırsınız. 
   6. **Sanal cihaz oluşturma için depolama hesabı** – sağlama sırasında bir depolama hesabı toohold hello görüntüsünü hello sanal cihazı seçin. Bu depolama hesabını hello olmalıdır hello sanal cihazı ve sanal ağ ile aynı bölgeye. Bu veri depolama için hello fiziksel veya sanal aygıt hello tarafından kullanılmamalıdır. Varsayılan olarak, yeni depolama hesabı bu amaçla oluşturulur. Ancak, bu kullanım için uygun bir depolama hesabı zaten olduğunu biliyorsanız, bunu hello listesinden seçebilirsiniz. Premium sanal aygıt oluşturuluyorsa hello açılır listeden yalnızca Premium depolama hesapları görüntülenir. 
      
      > [!NOTE]
      > Merhaba sanal cihaz yalnızca hello Azure storage hesaplarıyla çalışabilir. (Yani hello fiziksel cihaz için desteklenir) diğer bulut hizmet sağlayıcılarının Amazon, HP ve OpenStack gibi hello StorSimple sanal cihazı için desteklenmez.
      > 
      > 
   7. Merhaba sanal cihazda depolanan hello verileri bir Microsoft Veri merkezinde barındırılacağını anlamak hello onay işareti tooindicate'ı tıklatın. Yalnızca bir fiziksel cihaz kullandığınızda, şifreleme anahtarınızın cihazınızla tutulur; Bu nedenle, Microsoft şifresini çözemez. 
      
       Sanal cihaz kullandığınızda, hello şifreleme anahtarını ve hello şifre çözme anahtarı Microsoft Azure'da depolanır. Daha fazla bilgi için bkz. [sanal cihaz kullanımıyla ilgili güvenlik konuları](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Merhaba onay simgesi toocreate hello sanal aygıt'ı tıklatın. Merhaba aygıt sağlanan yaklaşık 30 dakika toobe sürebilir.
      
      ![StorSimple sanal cihaz oluşturma aşaması](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

