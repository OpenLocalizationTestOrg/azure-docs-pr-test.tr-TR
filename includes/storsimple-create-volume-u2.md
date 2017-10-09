<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate bir birim
1. Merhaba aygıtta **Hızlı Başlangıç** sayfasında, **birim Ekle** toostart hello Birim Ekleme sihirbazının.
2. Hello ekleme Birim Sihirbazı altında **temel ayarları**:
   
   1. Biriminiz için bir **Ad** yazın.
   2. Hello Hello aşağı açılan listesinde seçin **kullanım türü** biriminiz için. Yerel garantilerin, düşük gecikme sürelerinin ve yüksek performansın gerektiği iş yükleri için **Yerel olarak sabitlenmiş** bir birim seçin. Diğer tüm veriler için **Katmanlı** bir birim seçin. Bu birimi arşiv verileri için kullanıyorsanız **Bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın**’ı işaretleyin. 
      
       Yerel olarak sabitlenmiş bir birim sıkı hazırlanmıştır ve hello birincil veri hello birimde yerel toohello aygıt kalır ve toohello buluta dağıtılmamasını sağlar.  Yerel olarak sabitlenmiş bir birim oluşturursanız, hello aygıt hello yerel katmanlarda kullanılabilir alanı denetler tooprovision hello hello hacmi istenen boyutu. yerel olarak sabitlenmiş bir birim oluşturma işleminin hello hello cihaz toohello bulut varolan veriler dağılmasını neden ve toocreate hello birim geçen hello süre uzun olabilir. Merhaba toplam süre sağlanan hello birim, kullanılabilir ağ bant genişliği ve hello veri aygıtınızda hello boyutuna bağlıdır. 
      
       Katmanlı birim ölçülü sayıda kaynak kullanarak sağlanır ve hızlı oluşturulabilir. Seçme **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** arşiv verileri değişiklikleri hello yinelenenleri kaldırma öbek boyutunu biriminiz için hedeflenen katmanlı birim için too512 KB. Bu alan işaretli değilse hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar.
   3. Merhaba belirtin **sağlanan kapasite** biriminiz için. Seçili hello birim türünü temel alan kullanılabilir hello kapasiteyi not edin. Merhaba, birim boyutu hello kullanılabilir alanı aşmamalıdır belirtilmiş.
      
       Yerel olarak sabitlenmiş birimleri too8.5 TB yedeklemek veya hello 8100 cihazda too200 TB katmanlı birimleri sağlayabilirsiniz. Merhaba büyük 8600 cihazında yerel olarak sabitlenmiş birimleri too22.5 TB yedeklemek veya too500 TB katmanlı birimleri sağlayabilirsiniz. Katmanlı birimlerin çalışma gerekli toohost hello hello cihazda yerel alan olduğu gibi yerel olarak sabitlenmiş birimlerin oluşturması katmanlı birimlerin sağlanması için kullanılabilir hello alanı etkiler. Bu nedenle, yerel olarak sabitlenmiş bir birim oluşturursanız, katmanlı birimlerin oluşturulması için gereken boş alan azalır. Benzer şekilde, katmanlı birim oluşturulduysa, yerel olarak sabitlenmiş birimlerin oluşturması için hello kullanılabilir alan azalır.
      
       8100 Cihazınızda 8,5 TB (izin verilen boyut sınırı) yerel olarak sabitlenmiş bir birim hazırlıyorsanız, hello aygıtta kullanılabilir tüm yerel hello alanı tükendi. Herhangi bir katmanlı birim gelen mümkün toocreate olmaz ve sonraki sürümleri beklenmediğini noktası hello aygıt toohost hello çalışma kümesi üzerinde hello yerel alan olduğunu katmanlı birim. Var olan katmanlı birimler kullanılabilir hello alanı de etkiler. Örneğin, zaten 106 TB boyutunda katmanlı birimlerin bulunduğu bir 8100 cihazınız varsa, yerel olarak sabitlenmiş birimlerin kullanabileceği yalnızca 4 TB’lık alan kalır.
      
       Merhaba aşağıdaki resimde gösterilmiştir hello **temel ayarları** yerel olarak sabitlenmiş bir birim için iletişim kutusu.
      
        ![Yerel birim ekleme](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Merhaba aşağıdaki resimde gösterilmiştir hello **temel ayarları** katmanlı birim için iletişim kutusu.
      
        ![Yerel birim ekleme](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Merhaba ok simgesine tıklayın ![ok simgesi](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello sonraki sayfa.
3. Merhaba, **ek ayarlar** iletişim kutusunda, yeni bir erişim denetimi kaydı (ACR) ekleyin:
   
   1. ACR’nize bir **Ad** verin.
   2. Altında **iSCSI başlatıcısı adı**, sağlayın hello iSCSI tam adını (IQN), Windows konağınızın. Merhaba IQN yoksa, çok Git[Get hello bir Windows Server konağının IQN'ini](#get-the-iqn-of-a-windows-server-host).
   3. Altında **bu birim için varsayılan yedekleme?**seçin hello **etkinleştirmek** onay kutusu. Merhaba varsayılan yedekleme 22:30 günde bir (aygıt saat) yürütülen ve bu birimin bir bulut anlık görüntüsü oluşturur bir ilke oluşturur.
      
      > [!NOTE]
      > Merhaba yedek burada etkinleştirildikten sonra geri alınamaz. Bu ayar tooedit hello birim toomodify gerekir.
      > 
      > 
      
      ![Birim ekle](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Merhaba onay simgesine tıklayın ![onay simgesi](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Bir birim belirtilen hello ile oluşturulan ayarlar.

