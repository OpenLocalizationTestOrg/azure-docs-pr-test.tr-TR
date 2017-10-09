


## <a name="attach-an-empty-disk"></a>Boş disk ekleme
Boş disk ekleme veri disk, çünkü Azure hello .vhd dosyası sizin için oluşturur ve hello depolama hesabında depolayan basit bir yol tooadd olur.

1. Tıklatın **sanal makineleri (Klasik)**, ve ardından uygun VM seçin hello.

2. Merhaba ayarlar menüsünü tıklatın **diskleri**.

   ![Yeni bir boş diski kullanıma açın](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Merhaba komut çubuğunda **Attach yeni**.  
    Merhaba **Attach yeni disk** iletişim kutusu görüntülenir.

    ![Yeni bir diski kullanıma açın](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Hello aşağıdaki bilgilerle doldurun:
    - İçinde **dosya adı**, hello varsayılan adı kabul edin veya başka bir hello .vhd dosyası için yazın. Merhaba .vhd dosyası için başka bir ad yazın olsa bile hello veri diski otomatik olarak oluşturulan bir ad kullanır.
    - Select hello **türü** hello veri diski. Tüm sanal makineler standart diskler destekler. Çok sayıda sanal makineler ayrıca premium diskleri destekler.
    - Select hello **boyutu (GB)** hello veri diski.
    - İçin **ana bilgisayar önbelleğe alma**, hiçbiri seçin veya salt okunur.
    - Tamam toofinish'ı tıklatın.

4. Merhaba veri diski oluşturduktan ve bağlı sonra hello diskleri bölümünde hello VM listelenir.

   ![Yeni ve boş veri diski başarıyla eklendi](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Bir veri diski ekledikten sonra toohello VM üzerinde toolog gerekir ve böylece bu kullanılabilir hello diski başlatın.

## <a name="how-to-attach-an-existing-disk"></a>Nasıl yapılır: varolan bir diski kullanıma açın
Var olan bir diskin eklenmesi için depolama hesabında bir .vhd olmalıdır. Kullanım hello [Ekle AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd dosyası toohello depolama hesabı. Oluşturulan ve hello .vhd dosyası karşıya sonra tooa VM ekleyebilirsiniz.

1. Tıklatın **sanal makineleri (Klasik)**, ve ardından uygun sanal makine seçin hello.

2. Merhaba ayarlar menüsünü tıklatın **diskleri**.

3. Merhaba komut çubuğunda **Attach varolan**.

    ![Veri diski ekleme](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Tıklatın **konumu**. Merhaba kullanılabilir depolama hesaplarını görüntüler. Ardından, uygun depolama hesabı listeden seçin.

    ![Disk depolama hesabı sağlayın](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. A **depolama hesabı** disk sürücülerini (VHD) içeren bir veya daha fazla kapsayıcıları tutar. Merhaba uygun bir kapsayıcı listeden seçin.

    ![Makineler windows sanal kapsayıcının sağlayın](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Merhaba **VHD'ler** paneli hello disk hello kapsayıcısında tutulan sürücüleri listeler. Merhaba disklerden birini tıklatın ve Seç'i tıklatın.

    ![Sanal makineler-windows için disk görüntüsü belirtin](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Hello **varolan bir diski İlişti** paneli hello depolama hesabı, kapsayıcı ve seçilen sabit disk (vhd) tooadd toohello sanal makine içeren hello konumla yeniden görüntüler.

  Ayarlama **ana bilgisayar önbelleğe alma** toonone veya okuma yalnızca, ardından Tamam'ı tıklatın.

    ![Veri diski başarıyla eklendi](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
