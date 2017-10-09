<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall hello Azure portal gelen güncelleştirme

1. Merhaba StorSimple hizmeti sayfasında Cihazınızı seçin. Çok gidin**aygıtları** > **Bakım**.
2. Merhaba sayfasının Hello altında tıklatın **Güncelleştirmeleri tara**. Bir iş için kullanılabilir güncelleştirmeleri tooscan oluşturulur. Merhaba işi başarıyla tamamlandığında size bildirilir.
3. Merhaba, **yazılım güncelleştirmelerini** hello üzerinde aynı bölüm sayfasında hello yeni yazılım güncelleştirmeleri mevcuttur. Cihazınızda bir güncelleştirmeyi uygulamadan önce hello sürüm notlarını gözden geçirmenizi öneririz.
4. Merhaba sayfasının Hello altında tıklatın **Güncelleştirmeleri Yükle**ve ardından **Tamam**.
5. Merhaba, **güncelleştirmelerini yükleme** iletişim kutusu, hello önerileri uyguladıysanız emin olun ve ardından seçin **gereksinim yukarıda hello anlamak ve hazır tooupgrade cihazımı 'M** ve hello onay'ı tıklatın düğme.
   
    ![Onay iletisi](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Bir dizi önkoşul denetimi başlatılır. Bu denetimler şunlardır:
   
   * **Denetleyici durumu denetimleri** hem de aygıt denetleyicileri hello tooverify sağlıklı ve çevrimiçi.
   * **Donanım bileşeni durumu denetimleri** tüm donanım bileşenleri, StorSimple Cihazınızda hello tooverify sağlıklı.
   * **Veri 0 denetler** tooverify veri 0 aygıtınızda etkinleştirilir. Bu arabirim etkin değilse etkinleştirmeniz ve sonra yeniden denemeniz gerekir.
   * **Veri 2 ve veri 3 denetimleri** tooverify veri 2 ve veri 3 ağ arabirimlerini etkinleştirilmemiş. Daha sonra bu arabirimleri etkinleştirilirse, bu devre dışı bırakın ve sonra Cihazınızı tooupdate deneyin gerekir. Bu denetim yalnızca GA yazılımı çalıştıran bir cihazdan güncelleştirme yapıyorsanız gerçekleştirilir. 0.1, 0.2 veya 0.3 sürümlerini çalıştıran cihazlarda bu denetim gerekli değildir.
   * **Ağ geçidi onay** sürüm önceki tooUpdate 1 herhangi bir cihazda çalıştırma. Bu onay güncelleştirme 1 yazılımı öncesini çalıştıran tüm hello aygıtta gerçekleştirilir, ancak veri 0 dışında bir ağ arabirimi için yapılandırılmış bir ağ geçidi hello cihazları başarısız olur.
     
     tüm denetimlerden başarıyla tamamlanırsa hello güncelleştirme uygulanır. Merhaba denetimleri devam ederken size bildirilir.
     
     ![Denetim öncesi bildirim](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Merhaba aşağıda hello denetimleri başarısız bir örnek verilmiştir. Her iki hello cihaz denetleyicilerinin sağlıklı ve çevrimiçi olduğunu doğrulamanız gerekir. Merhaba donanım bileşenleri toocheck hello durumunu da gerekir. Bu örnekte, Denetleyici 0 ile Denetleyici 1 bileşenleri dikkat gerektirmektedir. Kendiniz tarafından bu sorunları gidermek olamaz, toocontact Microsoft Support gerekebilir.
     
       ![Denetimler başarısız oldu](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Merhaba denetimleri başarıyla tamamlandıktan sonra bir güncelleştirme işi oluşturulur. Merhaba güncelleştirme işi başarıyla oluşturulduğunda size bildirilir.
   
    ![Güncelleştirme işi oluşturma](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    Merhaba güncelleştirme aygıtınızda sonra uygulanır.
    
8. toomonitor hello hello güncelleştirme işinin ilerlemesini, tıklatın **işi görüntüle**. Merhaba üzerinde **işleri** sayfasında, devam eden güncelleştirme hello görebilirsiniz.
9. Merhaba güncelleştirme birkaç saat toocomplete alır. Merhaba güncelleştirme işi seçin ve tıklatın **ayrıntıları** hello işin herhangi bir zamanda tooview hello ayrıntılarını.
10. Merhaba işi tamamlandıktan sonra toohello gidin **Bakım** sayfasında ve çok ilerleyin**yazılım güncelleştirmelerini**.

