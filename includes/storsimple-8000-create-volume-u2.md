<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate bir birim
1. Merhaba hello cihazları Tablo listesi hello gelen **aygıtları** dikey penceresinde, Cihazınızı seçin. **+ Birim ekle**’ye tıklayın.

    ![Yeni birim ekleme](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. Merhaba, **birim Ekle** dikey penceresinde:
   
   1. Merhaba **aygıt seçin** alanı, geçerli cihazınız ile otomatik olarak doldurulur.

   2. Merhaba aşağı açılan listeden hello birim kapsayıcısı tooadd bir birim gereken yeri seçin. 

   3.  Biriminiz için bir **Ad** yazın. Merhaba birim oluşturulduktan sonra bir birim yeniden adlandırılamıyor.

   4. Hello Hello aşağı açılan listesinde seçin **türü** biriminiz için. Yerel garantilerin, düşük gecikme sürelerinin ve yüksek performansın gerektiği iş yükleri için **Yerel olarak sabitlenmiş** bir birim seçin. Diğer tüm veriler için **Katmanlı** bir birim seçin. Bu birimi arşiv verileri için kullanıyorsanız **Bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın**’ı işaretleyin.
      
       Katmanlı birim ölçülü sayıda kaynak kullanarak sağlanır ve hızlı oluşturulabilir. Seçme **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** arşiv verileri değişiklikleri hello yinelenenleri kaldırma öbek boyutunu biriminiz için hedeflenen katmanlı birim için too512 KB. Bu alan işaretli değilse hello ilgili katmanlı birim 64 KB öbek boyutu kullanır. Daha büyük bir yinelenenleri kaldırma öbek boyutu hello aygıt tooexpedite hello büyük arşiv verilerinin toohello bulut aktarımını sağlar.
       
       Yerel olarak sabitlenmiş bir birim sıkı hazırlanmıştır ve hello birincil veri hello birimde yerel toohello aygıt kalır ve toohello buluta dağıtılmamasını sağlar.  Yerel olarak sabitlenmiş bir birim oluşturursanız, hello aygıt hello yerel katmanlarda kullanılabilir alanı denetler tooprovision hello hello hacmi istenen boyutu. yerel olarak sabitlenmiş bir birim oluşturma işleminin hello hello cihaz toohello bulut varolan veriler dağılmasını neden ve toocreate hello birim geçen hello süre uzun olabilir. Merhaba toplam süre sağlanan hello birim, kullanılabilir ağ bant genişliği ve hello veri aygıtınızda hello boyutuna bağlıdır.

   5. Merhaba belirtin **sağlanan kapasite** biriminiz için. Seçili hello birim türünü temel alan kullanılabilir hello kapasiteyi not edin. Merhaba, birim boyutu hello kullanılabilir alanı aşmamalıdır belirtilmiş.
      
       Yerel olarak sabitlenmiş birimleri too8.5 TB yedeklemek veya hello 8100 cihazda too200 TB katmanlı birimleri sağlayabilirsiniz. Merhaba büyük 8600 cihazında yerel olarak sabitlenmiş birimleri too22.5 TB yedeklemek veya too500 TB katmanlı birimleri sağlayabilirsiniz. Katmanlı birimlerin çalışma gerekli toohost hello hello cihazda yerel alan olduğu gibi yerel olarak sabitlenmiş birimlerin oluşturması katmanlı birimlerin sağlanması için kullanılabilir hello alanı etkiler. Bu nedenle, yerel olarak sabitlenmiş birim oluşturursanız, katmanlı birimlerin oluşturulması için gereken boş alan azalır. Benzer şekilde, katmanlı birim oluşturulduysa, yerel olarak sabitlenmiş birimlerin oluşturması için hello kullanılabilir alan azalır.
      
       8100 Cihazınızda 8,5 TB (izin verilen boyut sınırı) yerel olarak sabitlenmiş bir birim hazırlıyorsanız, hello aygıtta kullanılabilir tüm yerel hello alanı tükendi. Merhaba aygıt toohost hello çalışma kümesine hello yerel alan olmadığından bu noktadan herhangi bir katmanlı birim oluşturamazsınız katmanlı birim. Var olan katmanlı birimler kullanılabilir hello alanı de etkiler. Örneğin, zaten 106 TB boyutunda katmanlı birimlerin bulunduğu bir 8100 cihazınız varsa, yerel olarak sabitlenmiş birimlerin kullanabileceği yalnızca 4 TB’lık alan kalır.

    6. Merhaba, **bağlı Konaklar** alan, hello oka tıklayın. 

        ![Bağlı konaklar](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. Merhaba, **bağlı Konaklar** dikey penceresinde, varolan bir ACR seçin veya yeni bir ACR hello aşağıdaki adımları gerçekleştirerek ekleyin:

       1. ACR’nize bir **Ad** verin.
       2. Altında **iSCSI başlatıcısı adı**, sağlayın hello iSCSI tam adını (IQN), Windows konağınızın. Merhaba IQN yoksa, çok Git[Get hello bir Windows Server konağının IQN'ini](#get-the-iqn-of-a-windows-server-host).

    9. **Oluştur**'a tıklayın. Bir birim belirtilen hello ile oluşturulan ayarlar.

        ![Oluştur’a tıklayın](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Burada oluşturduğunuz hello birim korunmuyor unutmayın. Bu birimi tootake zamanlanmış yedeklemeler sayesinde toocreate ve ilişkilendirme yedekleme ilkeleri gerekir. 

