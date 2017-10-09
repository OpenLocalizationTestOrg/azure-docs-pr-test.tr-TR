1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba üst sol başlayarak, tıklatın **yeni > işlem > Windows Server 2016 Datacenter**.

    ![Merhaba portalında toohello Azure VM görüntülerini gidin](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Windows Server 2016 Datacenter Hello üzerinde hello Klasik dağıtım modeli seçin. Oluştur’a tıklayın.

    ![Merhaba Portalı'nda kullanılabilir hello Azure VM görüntülerini gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Temel Bilgiler dikey penceresi

Merhaba temel bilgileri dikey penceresinde hello sanal makine için yönetim bilgi ister.

1. Girin bir **adı** hello sanal makine için. Merhaba örnekte _HeroVM_ hello sanal makinenin hello adıdır. Merhaba adı 1-15 karakter uzunluğunda olmalıdır ve özel karakterler içeremez.

2. Girin bir **kullanıcı adı** ve güçlü **parola** kullanılan toocreate hello VM üzerindeki yerel bir hesap olan. Merhaba yerel hesap kullanılan tooand toosign hello VM yönetin. Merhaba örnekte _azureuser_ hello kullanıcı adıdır.

 Merhaba parola 8-123 karakter uzunluğunda olmalıdır ve üç dışında hello dört aşağıdaki karmaşıklık gereksinimlerini karşılayacak: bir küçük harf karakter, bir büyük harf karakter, bir sayı ve bir özel karakter. [Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/windows/faq.md) hakkında daha fazla bilgi edinin.

3. Merhaba **abonelik** isteğe bağlıdır. Yaygın olarak kullanılan bir ayar "Kullandıkça Öde"dir.

4. Var olan seçin **kaynak grubu** veya yeni bir hello adını yazın. Merhaba örnekte _HeroVMRG_ hello hello kaynak grubunun adıdır.

5. Azure veri merkezi seçin **konumu** hello VM toorun istediğiniz. Merhaba örnekte **Doğu ABD** hello konumdur.

6. İşiniz bittiğinde tıklatın **sonraki** toocontinue toohello sonraki dikey.

    ![Bir Azure VM'yi yapılandırmak için hello temel bilgileri dikey penceresinde hello ayarları gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Boyut dikey penceresi

Hello boyutu dikey penceresinde hello VM hello yapılandırma ayrıntılarını tanımlar ve işletim sistemi, işlemciler, disk depolama türü ve tahmini aylık kullanım maliyetleri sayısı dahil çeşitli seçenekler listeler.  

Bir VM boyutu seçin ve ardından **seçin** toocontinue. Bu örnekte, _DS1_\__V2 standart_ hello VM boyutu.

  ![Merhaba seçebileceğiniz Azure VM boyutlarını gösteren hello boyutu dikey penceresinin ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Ayarlar dikey penceresi

Hello ayarları dikey penceresinde, depolama ve ağ seçenekleri ister. Merhaba varsayılan ayarları kabul edebilirsiniz. Azure, gerekli durumlarda uygun girişleri oluşturur.

Bunu destekleyen bir sanal makine boyutu seçtiyseniz, Disk türü altında Premium (SSD) seçeneğini belirleyerek Azure Premium Depolama’yı deneyebilirsiniz.

Değişiklikleriniz bittiğinde **Tamam**’a tıklayın.

## <a name="4-summary-blade"></a>4. Özet dikey penceresi

Merhaba Özet dikey penceresinde hello önceki tüm dikey pencereleri içinde belirtilen hello ayarları listeler. Tıklatın **Tamam** hazır toomake hello görüntü olduğunuzda.

 ![Merhaba sanal makinenin belirtilen ayarlarını vermiş Özet dikey raporu](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Merhaba sanal makine oluşturulduktan sonra hello portal hello yeni sanal makinenin altında listeler **tüm kaynakları**ve hello Panoda bir kutucuğu hello sanal makinenin görüntüler. Hello karşılık gelen bulut hizmeti ve depolama hesabı aynı zamanda oluşturulur ve listelenir. Merhaba sanal makine ve bulut hizmeti başlatıldığında otomatik olarak ve durumlarını olarak listelenen **çalıştıran**.

 ![Merhaba sanal makinesinin VM aracısı ve hello uç noktalarını yapılandırma](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
