<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, başlatın ve bir birimi biçimlendirme
1. Merhaba Microsoft iSCSI başlatıcısını başlatın.
2. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **bulma** sekmesini tıklatın, **Portal Bul**.
3. Merhaba, **Hedef Portal Bul** iletişim kutusu, Merhaba, iSCSI etkin ağ arabiriminin IP adresini girin ve ardından **Tamam**. 
4. Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **hedefleri** sekmesinde, hello bulun **bulunan hedefler**. Merhaba Aygıt durumu olarak görünmelidir **devre dışı**.
5. Merhaba hedef cihazı seçin ve ardından **Bağlan**. Merhaba cihaz bağlandıktan sonra hello durumu çok değişmelidir**bağlı**. (Merhaba Microsoft iSCSI başlatıcısını kullanma hakkında daha fazla bilgi için bkz: [yükleme ve yapılandırma Microsoft iSCSI başlatıcısı][1]).
6. Windows konağında, hello Windows logosu tuşu + X tuşlarına basın ve ardından **çalıştırmak**. 
7. Merhaba, **çalıştırmak** iletişim kutusuna **Diskmgmt.msc**. Tıklatın **Tamam**ve hello **Disk Yönetimi** iletişim kutusu görüntülenir. Merhaba sağ bölmede, konaktaki hello birimleri gösterir.
8. Merhaba, **Disk Yönetimi** penceresinde hello takılan birimler görünür hello aşağıdaki çizimde gösterildiği gibi. Merhaba bulunan birime sağ tıklayın (Merhaba disk adına tıklayın) ve ardından **çevrimiçi**.
   
     ![Birim biçimlendirmeyi başlatma](./media/storsimple-8000-mount-initialize-format-volume/step7initializeformatvolume.png) 
9. Merhaba birime sağ tıklayın (Merhaba disk adına tıklayın) yeniden ve ardından **başlatma**.
10. tooformat basit bir birimi hello aşağıdaki adımları gerçekleştirin:
    
    1. Merhaba birimi seçin, sağ tıklayın (Merhaba sağ alanı tıklayın) tıklatıp **yeni basit birim**.
    2. Hello yeni basit birim sihirbazında hello birim boyutunu ve sürücü harfini belirtin ve hello birim bir NTFS dosya sistemi olarak yapılandırın.
    3. 64 KB ayırma birimi boyutu belirtin. Bu ayırma birimi boyutu iyi hello yinelenenleri kaldırma algoritmalarıyla hello StorSimple çözüm kullanılan çalışır.
    4. Hızlı biçimlendirme gerçekleştirin.

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
