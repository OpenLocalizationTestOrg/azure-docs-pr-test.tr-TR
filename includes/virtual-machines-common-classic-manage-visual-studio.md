Visual Studio'da Sunucu Gezgini kullanarak Azure'da sanal makineler oluşturabilirsiniz.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Sunucu Gezgini'nde bir Azure sanal makine oluşturma
Bir sanal makine hello oluşturabilirsiniz, ancak [Azure Yönetim Portalı](http://go.microsoft.com/fwlink/?LinkID=253103), sunucu Gezgini'nde komutları kullanarak Azure'da bir sanal makine oluşturabilirsiniz. Sanal makineler kullanılabilir, örneğin, tooprovide bir front end ortak yük dengeli genel bir uç nokta.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate yeni bir sanal makine
1. Server Explorer'da hello açın **Azure** düğümü ve tıklatın **sanal makineleri**.
2. Merhaba bağlam menüsünde **sanal makine oluşturma**.
   
    Merhaba **yeni bir sanal makine oluşturma** Sihirbazı görünür.
   
    ![Merhaba sanal makine Oluştur komutu](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Merhaba üzerinde **bir abonelik seçin** sayfasında, abonelik toouse hello sanal makine oluştururken seçin ve ardından **sonraki**.
   
    İçinde tooAzure oturumunuz açık değil,'ı tıklatın **oturum** toosign içinde. Ardından, henüz seçili değilse, Azure aboneliğinizin hello açılır liste kutusunda seçin.
4. Merhaba üzerinde **bir sanal makine görüntüsü seçin** sayfasında, bir resim türünü hello **görüntü türü** açılır liste kutusu ve bir sanal makine görüntülerini hello ardından **görüntü adı** Liste kutusu. İşiniz bittiğinde tıklatın **sonraki**.
   
    ![Bir sanal makine görüntüsü seçin sayfası](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Resim türleri aşağıdaki hello seçebilirsiniz.
   
   * **Ortak görüntüleri** sanal makine görüntüleri işletim sistemleri ve Windows Server ve SQL Server gibi sunucu yazılımları listeler.
   * **MSDN görüntülerine** yazılım kullanılabilir tooMSDN aboneleri, Visual Studio ve Microsoft Dynamics gibi sanal makine görüntülerini listeler.
   * **Özel resimler** listeleri özelleştirilmiş ve oluşturduğunuz sanal makine görüntülerini genelleştirilmiş.
     
     özelleştirilmiş ve sanal makineleri genelleştirilmiş hakkında toolearn için bkz: [VM görüntüsü](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Bkz: [nasıl tooCapture bir şablon olarak Windows sanal makine tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) nasıl yeni bir sanal makineye tooquickly kullanabileceğiniz bir şablon oluştur tooturn sanal makineleri önceden yapılandırılmış hakkında bilgi.
     
     Bir sanal makine görüntü adı toosee hakkında bilgi hello görüntü hello sağ tarafında hello sayfasının tıklatabilirsiniz.
     
     > [!NOTE]
     > Sanal makine görüntüleri toohello ekleyemezsiniz **ortak görüntüleri** veya **MSDN görüntülerine** salt okunur olduğundan listeler. Oluşturduğunuz tüm sanal makineler toohello eklendikçe **özel görüntüleri** listesi.
     > 
     > 
     
     Bir Visual Studio düzeyi abonelikle bir MSDN abone değilseniz, Visual Studio gibi çeşitli diğer görüntüleri içeren bir önceden oluşturulmuş Azure sanal makine oluşturabilirsiniz. Daha fazla bilgi için bkz: [bir sanal makine Visual Studio kullanarak görüntüleri Visual Studio 2013 galeri görüntüsü tarafından MSDN aboneleri için oluşturmak](http://visualstudio2013msdngalleryimage.azurewebsites.net) ve [MSDN Abonelikleri](https://www.visualstudio.com/products/msdn-subscriptions-vs). |
5. Merhaba üzerinde **sanal makine temel ayarları** sayfasında, bir makine adı girin ve ardından hello belirtimleri hello boyutu ve bir kullanıcı adı ve parola gibi hello sanal makine için ekleyin. İşiniz bittiğinde tıklatın **sonraki**.
   
    Merhaba yeni adını kullanacağınız ve bunları aşağı içinde bu durumda bir fikir toowrite olması için Uzak Masaüstü'nü kullanarak hello makine içine parola toolog unutmayın. Visual Studio'da bir Azure sanal makine oluşturduktan sonra boyutuna ve diğer hello ayarlarını değiştirebilirsiniz [Azure Yönetim Portalı](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Merhaba sanal makine için daha büyük boyutları seçerseniz, ek ücretleri uygulanabilir. Bkz: [sanal makineler fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/virtual-machines/) daha fazla bilgi için.
   > 
   > 
6. Visual Studio'da oluşturulan sanal makineler bir bulut hizmeti gerektirir. Merhaba üzerinde **bulut hizmeti ayarlarını** sayfasında, hello sanal makine için bir bulut hizmeti seçin veya tıklatın **< Yeni Oluştur... >** bir bulut hizmeti veya yeni bir toouse istediğiniz zaten yoksa hello aşağı açılan listesinde biri. Bir depolama hesabı de gereklidir, böylece bir depolama hesabı seçin (veya yeni bir depolama hesabı oluşturun) hello içinde **depolama hesabı** açılır liste kutusu. Bkz: [giriş tooMicrosoft Azure Storage](../articles/storage/common/storage-introduction.md) daha fazla bilgi için.
7. Toospecify (isteğe bağlı olan) bir sanal ağ istiyorsanız hello sanal ağ ve alt açılır liste kutularını seçin.
   
    Bir kullanılabilirlik kümesi üyesi olan bir sanal makine dağıtılan toodifferent hata etki alanı yok. Bkz: [Azure Virtual Network](https://azure.microsoft.com/services/virtual-network/) daha fazla bilgi için.
8. Merhaba, sanal makine toobelong tooan kullanılabilirlik kümesi (Ayrıca isteğe bağlı) istiyorsanız seçin **belirtin bir kullanılabilirlik kümesi** onay kutusunu işaretleyin ve ardından kullanılabilirlik hello açılır liste kutusunda kümesi seçin. İşiniz bittiğinde, hello seçin **sonraki** düğmesi.
   
    Kullanılabilirlik kümesi, sanal makine tooan ekleme ağ hataları, yerel disk donanım hataları ve planlanan kapalı kalma süresi sırasında kullanılabilir kalmasını uygulamanızı yardımcı olur. Toouse hello gereksinim [Azure Yönetim Portalı](http://go.microsoft.com/fwlink/?LinkID=253103) toocreate sanal ağlar, alt ağlar ve kullanılabilirlik ayarlar. Bkz: [Yönet hello sanal makinelerin kullanılabilirliğini](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) daha fazla bilgi için.
9. Merhaba üzerinde **uç noktaları** sayfasında, sanal makinenizin kullanılabilir toousers istediğiniz hello ortak uç noktaları belirtin. Örneğin, tooenable HTTP (bağlantı noktası 80) varsayılan olarak etkinleştirilen toohello Uzak Masaüstü'nü ve PowerShell uç noktaları, ayrıca seçebilirsiniz. uç noktası, bir tooadd hello birinde seçin **bağlantı noktası adı** açılan liste kutusunu ve ardından hello **Ekle** düğmesi. uç noktası, bir tooremove seçin hello kırmızı **X** hello uç noktalar listesinde sonraki toohello adı.
   
    ![Merhaba sanal makineler sihirbazındaki uç noktaları sayfası Hello.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    kullanılabilir hello uç noktaları, sanal makine için seçtiğiniz hello bulut hizmeti bağlıdır. Bkz: [Azure hizmet uç noktaları](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) daha fazla bilgi için.
   
   > [!NOTE]
   > Ortak uç noktaları etkinleştirmek, hizmetleri, sanal makine kullanılabilir toohello yapar Internet. Emin tooinstall olması ve hello uç noktaları için ayarı erişim denetim listeleri (ACL'ler) gibi hello uç noktaları ve hizmetler, sanal makinede düzgün şekilde yapılandırın. Bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) daha fazla bilgi için.
   > 
   > 
10. Merhaba sanal makine ayarlarını yapılandırmaya bitirdikten sonra hello seçin **oluşturma** düğmesini toocreate hello sanal makine.
    
     Azure hello sanal makine oluştururken hello **Azure etkinlik günlüğü** hello hello sanal makine oluşturma işlemi ilerlemesini gösterir.
    
     ![Sanal makine etkinlik günlüğü - sürüyor.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     tooview yalnızca sanal makine bilgilerini hello seçin **sanal makineleri** hello sekmesinde **Azure etkinlik günlüğü**.
    
     ![Sanal makine etkinlik günlüğü - tamamlandı.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Merhaba işlem başarıyla tamamlanırsa hello yeni bir sanal makine hello altında görünür **sanal makineleri** Sunucu Gezgininde. İçine hello tıklayarak oturum **Uzak Masaüstü kullanarak bağlanmak** kısayol.
    
     ![Server Explorer'da görünen sanal makine.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Sanal makinelerinizi yönetme
Merhaba sanal makinenin yapılandırma sayfasında ayrıca tooshutting aşağı, bağlanma, yenileme ve ekleme kontrol noktaları toohello sanal makine seçili, ayrıca görüntülemek veya hello sanal makine için ayarları değiştirebilirsiniz. Şunları yapabilirsiniz:

* Merhaba sanal makine boyutunu değiştirin.
* Select hello kullanılabilirlik hello sanal makineyle toouse ayarlayın.
* Ekle, Kaldır veya ortak uç noktaları için ayarları değiştirin.
* Ekleyin, kaldırın veya sanal makine uzantıları yapılandırın.
* Merhaba sanal makineyle ilişkili hello disklerle ilgili bilgileri görüntüleyin.

### <a name="view-or-change-virtual-machine-settings"></a>Sanal makine ayarlarını görüntülemek veya değiştirmek
1. Sunucu Gezgini'nde, sanal makinenizde hello seçin **Azure sanal makineleri** düğümü.
2. Merhaba kısayol menüsünden seçin **yapılandırma** tooview hello sanal makine yapılandırma sayfası.
   
    ![Hello Azure sanal makine yapılandırma sayfası](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Merhaba sanal makine bilgilerini görüntüleyin veya değiştirin.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Kaydedin veya sanal makinenize hello durumunu geri yükle
Sanal makinenizi yapılandırmanız ve yazılım üzerinde yükleme gibi sanal makine kontrol noktaları oluşturarak ilerleme durumunuzu kaydetmek iyi bir fikir tooregularly gereklidir. Bir denetim noktası bir anlık görüntüsü veya görüntüsü, sanal makinenin geçerli durumu hello ' dir. Bir şey hello sanal makineyle yanlış giden veya tooreconfigure hello sanal makine isterseniz üzerinden sıfırdan yerine tooa önceki kontrol noktası durumuna geri yükleyerek zaman kazanabilirsiniz.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>bir sanal makine kontrol toocreate
1. Sunucu Gezgini'nde, sanal makinenizde hello seçin **Azure sanal makineleri** düğümü.
2. Merhaba kısayol menüsünden seçin **yapılandırma** tooview hello sanal makine yapılandırma sayfası.
3. Merhaba Hello yapılandırma sayfasında, seçin **görüntü yakalama** düğmesi.
   
    ![Azure yapılandırma sayfası yakalama düğmesi](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Merhaba **sanal makine yakalama** iletişim kutusu görüntülenir.
   
    ![Azure yakalama sanal makine iletişim kutusu](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Bir görüntü etiketi ve açıklama girin. Bir varsayılan etiket ve açıklama sağlanır, ancak bunların kendi isterseniz üzerine yazabilirsiniz.
5. Bu sanal makinede Sysprep zaten çalıştırdıysanız, hello seçin **hello sanal makinede Sysprep'i çalıştırdım** kutusu.
   
    Sysprep, başka şeylerin hello sanal makinenin diğer kullanabileceğiniz şablonu kolaylaştırarak Windows sürümünden sistemleri özgü verileri kaldırır bir araçtır. Bkz: [nasıl tooCapture bir şablon olarak Windows sanal makine tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) daha fazla bilgi için. VM Hello, Sysprep çalıştırılmadan önce yedekleyin.
6. Merhaba yakalama ayarlarının yapılandırılmasını bitirdikten sonra hello seçin **yakalama** düğmesini toocreate hello denetim noktası.
   
    Azure hello denetim noktası oluştururken hello **Azure etkinlik günlüğü** hello hello işlemin ilerlemesini gösterir.
   
    ![Bir sanal makine denetim noktası yakalama](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Merhaba denetim noktası işlemi tamamlandığında hello görürsünüz **Azure etkinlik günlüğü**.
   
    ![Denetim noktası işlemi tamamlandı](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>toomanage sanal makine kontrol noktaları
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>bir sanal makine tooa toorestore önceden durumu kaydedildi
* Özetlenen hello adımları [adım adım: gerçekleştirmek bulut geri yükler, Microsoft Azure PowerShell - 2. parça kullanarak sanal makineleri](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete bir denetim noktası
1. Toohello Git [Azure Yönetim Portalı](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Merhaba Hello sanal makinenin yapılandırma sayfasında, seçin **görüntüleri** hello sayfanın üst kısmındaki hello sekmesi.
3. Toodelete istediğiniz ve hello seçin hello kontrol noktası seçin **silmek** hello altındaki hello sayfasının düğmesini.

## <a name="shut-down-your-virtual-machine"></a>Sanal makineyi Kapat
1. Sunucu Gezgini'nde hello içinde aşağı tooshut istediğiniz hello sanal makine seçin **Azure sanal makineleri** düğümü.
2. Merhaba kısayol menüsünde hello seçin **kapatma** komutu ya da seçin **yapılandırma** tooview hello sanal makine yapılandırma sayfası ve ardından hello **kapatma**düğmesi.

## <a name="next-steps"></a>Sonraki adımlar
sanal makineler oluşturma hakkında daha fazla toolearn bkz [çalıştıran bir sanal makine Linux oluşturma](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [hello Azure Önizleme Portalı'nda Windows çalıştıran bir sanal makine oluşturma](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

