


Bu makalede hello Klasik dağıtım modeli kullanılarak oluşturulmuş Azure sanal makineler hakkında kullanıcılara sor bazı sık sorulan soruları giderir.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>VM'im hello Klasik dağıtım modeli toohello yeni Resource Manager modelinde oluşturulmuş geçirebilir miyim?
Evet. Yönergeler için toomigrate, bkz:

* [Resource Manager Azure PowerShell kullanarak Klasik tooAzure geçirmek](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Resource Manager Azure CLI kullanarak Klasik tooAzure geçirmek](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>Azure sanal makinesinde ne çalıştırabilirim?
Tüm aboneler bir Azure sanal makinesinde sunucu yazılımı çalıştırabilir. Windows Server’ın yeni sürümlerinin yanı sıra çeşitli Linux dağıtımlarını çalıştırabilirsiniz. Destek ayrıntıları için bkz.

• Windows VM’leri için -- [Azure Sanal Makineleri için Microsoft sunucu yazılımı desteği](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Linux VM’leri için -- [Azure Destekli Dağıtımlarda Linux](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Windows istemci görüntüleri için belirli Windows 7 ve Windows 8.1 kullanılabilir tooMSDN Azure avantajı aboneleri ve geliştirme ve test görevler için MSDN Geliştirme ve Test Kullandıkça Öde aboneleri sürümleridir. Yönerge ve kısıtlamalar dahil olmak üzere ayrıntılı bilgi edinmek için bkz. [MSDN aboneleri için Windows İstemci görüntüleri](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>Benzeşim grupları neden kullanımdan kaldırılıyor?
Benzeşim grupları, bir müşterinin Azure içindeki bulut hizmeti dağıtımlarının ve depolama hesaplarının coğrafi olarak gruplandırılmasıyla ilgili eski bir kavramdır. Bunlar ilk olarak tooimprove VM VM ağ performansını hello erken Azure ağ tasarımları sağlandı. Bunlar da sınırlı tooa küçük bir bölgede donanım kümesi olan sanal ağlar (Vnet'ler) ilk sürümünü hello desteklenir.

bir bölge içinde geçerli Azure ağ hello benzeşim grupları artık gerekli olmayan şekilde tasarlanmıştır. Sanal ağlar da bölgesel bir kapsamda olduğundan, artık sanal ağ kullanılırken benzeşim grubu gerekmez. Toothese geliştirmeleri, artık bazı senaryolarda sınırlama çünkü müşterilerin benzeşim grupları kullanmanızı öneririz. Benzeşim grupları kullanarak kullanılabilir tooyou VM boyutları hello seçimine sınırlar VM'ler toospecific donanımınız gereksiz yere ilişkilendirin. Yeni VM'ler hello belirli donanım hello benzeşim grubu ile ilişkili ise kapasite tooadd denediğinizde de toocapacity ile ilgili hataları neden olabilir.

Benzeşim grubu özellikleri zaten hello Azure Resource Manager dağıtım modeli ve hello Azure portalı kullanım dışı bırakılmıştır. İçin Klasik Azure portalı Merhaba, biz benzeşim grupları oluşturma ve depolama kaynaklarını sabitlenmiş tooan benzeşim grubu oluşturma desteği onaysız kılınmadan. Bir benzeşim grubu kullanmakta olduğunuz toomodify mevcut bulut Hizmetleri gerek yoktur. Bununla birlikte, bir Azure destek uzmanı tarafından önerilmediği sürece yeni bulut hizmetleri için benzeşim gruplarını kullanmamalısınız.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Bir sanal makineyle birlikte ne kadar depolama alanı kullanabilirim?
Her veri diski too1 TB olabilir. Merhaba kullanabileceğiniz veri diski sayısı hello hello sanal makine boyutuna bağlıdır. Ayrıntılar için bkz. [Virtual Machines boyutları](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bir Azure depolama hesabı hello işletim sistemi diski ve veri diskleri için depolama sağlar. Her disk bir sayfa blobu olarak depolanan bir .vhd dosyasıdır. Fiyatlandırma ayrıntıları için bkz. [Depolama Fiyatlandırma Ayrıntıları](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Hangi sanal sabit disk türlerini kullanabilirim?
Azure yalnızca değişmeyen, VHD biçimli sanal sabit diskleri destekler. Azure'da toouse istediğiniz bir VHDX varsa toofirst gerekli Hyper-V Yöneticisi'ni veya hello kullanarak Dönüştür [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet'i. Bunu sonra kullanın [Ekle AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet'te (hizmet yönetimi modu) tooupload hello VHD tooa sanal makinelerle kullanabilmeniz için Azure depolama hesabı.

* Linux yönergeler için bkz: [oluşturma ve bir Sanal Sabit Disk, CONTAINS karşıya hello Linux işletim sistemi](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Windows yönergeler için bkz: [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Bu sanal makineleri hello Hyper-V sanal makineleri aynı misiniz?
Çok benzer birçok yolla "1. nesil" Hyper-V sanal makineleri, ancak bunlar olduğunuz tam hello aynı. Her iki tür sanallaştırılmış donanım sağlayın ve hello VHD biçiminde sanal sabit diskleri uyumludur. Bu, Hyper-V ile Azure arasında geçiş yapabileceğiniz anlamına gelir. Bazen Hyper-V kullanıcılarını şaşırtan üç temel fark şunlardır:

* Azure konsolunda erişim tooa sanal makine sağlamaz. Tamamlanıncaya kadar hiçbir şekilde tooaccess bir VM olan önyükleme.
* Çoğu [boyuttaki](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure VM’ler yalnızca 1 sanal ağ bağdaştırıcısına sahiptir ve bu, yalnızca 1 dış IP adresine sahip olabilecekleri anlamına gelir. (Merhaba A8 ve A9 boyutlarını ikinci bir ağ bağdaştırıcısı sınırlı senaryolarda örnekleri arasında uygulama iletişimi için kullanın.)
* Azure VM’leri 2. Nesil Hyper-V VM özelliklerini desteklemez. Bu özellikler hakkında ayrıntılı bilgi edinmek için bkz. [Hyper-V için Sanal Makine Belirtimleri](http://technet.microsoft.com/library/dn592184.aspx) ve [2. Nesil Sanal Makineye Genel Bakış](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Bu sanal makineler mevcut, şirket içi ağ altyapımı kullanabilir mi?
Merhaba Klasik dağıtım modelinde oluşturulan sanal makineler için mevcut altyapınızı Azure Virtual Network tooextend kullanabilirsiniz. Merhaba bir şube ofis ayarlama gibi bir yaklaşımdır. Sağlamak ve sanal özel ağları (VPN'ler) Azure'da yönetin yanı sıra bunları güvenli bir şekilde tooon içi bağlayın BT altyapısı. Ayrıntılar için bkz. [Sanal Ağa Genel Bakış](../articles/virtual-network/virtual-networks-overview.md).

Sanal makine toobelong toowhen hello sanal makine oluşturma hello istediğiniz toospecify hello ağı gerekir. Varolan bir sanal makine tooa sanal ağı katılamaz. Ancak, hello sanal sabit diskten (VHD) hello varolan sanal makine ayırma tarafından bu sorunu çözmek ve ardından istediğiniz hello ağ yapılandırmasıyla toocreate yeni bir sanal makine kullanın.

## <a name="how-can-i-access--my-virtual-machine"></a>Sanal makinelerime nasıl erişebilirim?
Bir Windows VM veya bir güvenli Kabuk (SSH) için bir Linux VM için Uzak Masaüstü bağlantısı kullanarak tooestablish toohello sanal makineye uzak bağlantı toolog gerekir. Yönergeler için bkz.

* [Nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). En fazla 2 eşzamanlı bağlantı desteklenir, Uzak Masaüstü Hizmetleri oturumu ana bilgisayarı hello sunucu yapılandırılmadığı sürece.  
* [Nasıl tooLog tooa Linux çalıştıran sanal makine üzerinde](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Varsayılan olarak, SSH en fazla 10 eş zamanlı bağlantıya izin verir. Merhaba yapılandırma dosyasını düzenleyerek bu sayıyı artırabilirsiniz.

Uzak Masaüstü veya SSH sorun yaşıyorsanız, yükleme ve hello kullanma [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzantısı toohelp düzeltme hello sorun.

Windows VM’ler için ek seçenekler şunlardır:

* Buna Klasik Azure portalı Merhaba, hello VM bulur ve ardından **sıfırlama uzaktan erişim** hello komut çubuğundan.
* Gözden geçirme [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Windows PowerShell uzaktan iletişimi tooconnect toohello VM kullanın veya diğer kaynakları tooconnect toohello VM için ek uç noktaları oluşturun. Ayrıntılar için bkz [nasıl tooSet yukarı uç noktaları tooa sanal makine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hyper-V ile sahibiyseniz, aracı benzer tooVMConnect için arayan. Konsol erişimi tooa sanal makine desteklenmediğinden azure benzer bir araç sağlamaz.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Merhaba geçici disk (Merhaba D: sürücü Windows veya Linux için /dev/sdb1) toostore verileri kullanabilir miyim?
Merhaba geçici disk (Merhaba D: sürücü varsayılan olarak Windows veya Linux için /dev/sdb1) toostore veri kullanmamalısınız. Bunlar yalnızca geçici depolama alanı olduğundan, verileri kurtarılamaz biçimde kaybetme riskiyle karşılaşırsınız. Bu Hello sanal makine tooa farklı ana bilgisayar taşındığında ortaya çıkabilir. Bir sanal makine yeniden boyutlandırma, hello konak ya da bir donanım hatası hello ana bilgisayarda güncelleştirme bir sanal makineyi taşımak hello nedenlerden bazılarıdır.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Merhaba geçici disk hello sürücü harfi nasıl değiştirebilir miyim?
Bir Windows sanal makinesinde hello sürücü harfiyle hello sayfa dosya taşıma ve sürücü harflerini yeniden atama değiştirebilirsiniz, ancak toomake belirli bir sırada adımları hello emin olmanız gerekir. Yönergeler için bkz: [değişiklik hello sürücü harfi hello Windows geçici disk](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Merhaba konuk işletim sistemini nasıl yükseltebilir miyim?
Merhaba terim yükseltme genellikle taşıma tooa daha anlamına gelir üzerinde hello kalırken, işletim sisteminizi güncel sürümünde aynı donanım. Azure VM'ler için tooa taşıma işlemi hello daha yeni sürüm farklı Linux ve Windows için:

* Linux VM'ler için hello paket Yönetim Araçları ve hello dağıtım için uygun yordamları kullanın.
* Windows sanal makine için aşağıdakine benzer hello Windows Server Geçiş araçları kullanarak toomigrate hello sunucusu gerekir. Azure üzerinde bulunurken tooupgrade hello konuk işletim sistemi denemesi yok. Erişim toohello sanal makine kaybı hello riski nedeniyle desteklenmiyor. Sorunları hello yükseltme sırasında oluşursa, Uzak Masaüstü hello özelliği toostart kaybedebilirsiniz oturum ve mümkün tootroubleshoot hello sorunları olmayacaktır.

Merhaba araçları ve Windows Server geçiş işlemleri hakkında genel bilgi için bkz [rolleri ve özellikleri geçirme tooWindows sunucu](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Merhaba varsayılan kullanıcı adı ve parola hello sanal makineye nedir?
Azure tarafından sağlanan hello görüntüleri bir önceden yapılandırılmış kullanıcı adı ve parolası yok. Bu görüntülerden birini kullanarak sanal makine oluşturduğunuzda, bir kullanıcı adı ve kullanacağınız parola tooprovide gerekir toolog toohello sanal makine üzerinde.

Merhaba kullanıcı adı veya parola unuttuysanız ve hello VM Aracısı yüklediniz, yükleme ve hello kullanma [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzantısı toofix hello sorun.

Ek ayrıntılar:

* Hello Linux görüntüleri için hello Azure Klasik portalı kullanıyorsanız, 'azureuser' varsayılan kullanıcı adı olarak verilir, ancak 'Galeri'den' yerine 'Hızlı Oluştur' hello yolu toocreate hello sanal makine olarak kullanarak bunu değiştirebilirsiniz. 'Galeri'den' kullanarak da olanak tanır karar olup olmadığını toouse bir parola, bir SSH anahtarı ya da her iki toolog size. Merhaba kullanıcı 'sudo' erişimi olan bir ayrıcalıklı olmayan kullanıcı hesabıdır toorun ayrıcalıklı komutları. Merhaba 'root' hesabında devre dışı bırakılır.
* Merhaba VM oluşturduğunuzda, Windows görüntülerini için tooprovide bir kullanıcı adı ve parola gerekir. Merhaba hesabı toohello Administrators grubuna eklenir.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Azure sanal makinelerimde virüsten koruma yazılımı çalıştırabilir mi?
Azure virüsten koruma çözümleri için çeşitli seçenekler sunar, ancak bu tooyou toomanage durumda. Örneğin, kötü amaçlı yazılımdan koruma yazılımı için ayrı bir abonelik gerekebilir ve toorun tarar ve güncelleştirmeleri yüklediğinizde toodecide gerekir. Windows sanal makinesi oluştururken veya daha sonra Microsoft Kötü Amaçlı Yazılımdan Koruma, Symantec Endpoint Protection veya TrendMicro Deep Security Agent için bir VM uzantısıyla virüsten koruma desteği ekleyebilirsiniz. Merhaba Symantec ve TrendMicro uzantıları ücretsiz sınırlı süreli deneme aboneliği veya varolan bir kurumsal aboneliği kullanmanıza olanak tanır. Microsoft Kötü Amaçlı Yazılımdan Koruma ücretsizdir. Ayrıntılar için bkz.

* [Nasıl tooinstall ve Symantec Endpoint Protection Azure VM temelinde yapılandırın](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Nasıl tooinstall ve bir Azure VM bir hizmet olarak eğilimi mikro derin güvenliği yapılandırma](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Azure Sanal Makinelerinde Kötü Amaçlı Yazılıma Karşı Koruma Çözümleri Dağıtma](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Yedekleme ve kurtarma seçeneklerim nelerdir?
Azure Backup belirli bölgelerde önizleme olarak sunulmaktadır. Ayrıntılar için bkz. [Azure sanal makinelerini yedekleme](../articles/backup/backup-azure-vms.md). Sertifikalı iş ortaklarının sunduğu başka çözümler vardır. şu anda kullanılabilir nedir çıkışı toofind hello Azure Marketi arayın.

Ek bir seçenek toouse hello anlık görüntü yetenekleri blob storage'nın ' dir. toodo bunu hello VM üzerinde blob anlık görüntü güvenen herhangi bir işlem önce aşağı tooshut gerekir. Bu bekleyen veri yazma kaydeder ve hello dosya sistemi tutarlı bir duruma koyar.

## <a name="how-does-azure-charge-for-my-vm"></a>Azure, sanal makinem için nasıl bir ücretlendirme uygular?
Azure hello VM'nin boyutu ve işletim sistemi temelinde saatlik fiyat giderler. Kısmi saatler için yalnızca kullanım hello dakika için Azure ücretlidir. Önceden yüklenmiş belirli yazılımlar içeren bir VM görüntüsü ile Merhaba VM oluşturursanız, ek saatlik yazılım ücretleri uygulanabilir. Azure ücretleri hello VM'ın işletim sistemi ve veri diskleri için depolama için ayrı ayrı. Geçici disk depolama ücretsizdir.

Merhaba VM durumu çalışıyor veya durdurulmuş, ancak hello VM durumu durdurulduğunda, sizden ücret istenmese ücretlendirilen (XML'deki ayrılan). tooput hello bir VM'yi (XML'deki ayrılmış) durumu durduruldu, hello aşağıdakilerden birini yapın:

* Kapatıldı veya hello VM hello Klasik Azure Portalı ' silin.
* Merhaba Stop-AzureVM cmdlet'i hello Azure PowerShell modülü kullanılabilir kullanın.
* Merhaba Hizmet Yönetimi REST API'si Hello kapatma rol işlemi kullanın ve StoppedDeallocated hello PostShutdownAction öğesi için belirtin.

Daha ayrıntılı bilgi edinmek için bkz. [Sanal Makine Fiyatlandırması](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Azure, bakım için sanal makinemi yeniden başlatır mı?
Azure bazen VM hello Azure veri merkezleri içinde normal, planlı bakım güncelleştirmelerin parçası olarak yeniden başlatır.

Azure tarafından sanal makinenizi etkileyen ciddi bir donanım sorunu algılandığında planlanmamış bakım olayları gerçekleşebilir. Planlanmamış olayları, Azure otomatik olarak hello VM tooa sağlıklı konak geçirir ve hello VM yeniden başlatır.

Tüm tek başına VM için hello VM'ler hello güncelleştirme sırasında yeniden başlatılamıyor çünkü (Merhaba VM bir kullanılabilirlik kümesinin parçası olmayan anlamına gelir), Azure hello aboneliğin Hizmet Yöneticisi e-posta ile en az bir hafta önce planlı bakım bildirir. Merhaba Vm'lerinde çalışan uygulamalar kapalı kalma süresi yaşar.

Merhaba yeniden başlatma tooplanned bakım meydana geldiğinde hello Azure Klasik portalında veya Azure PowerShell tooview hello yeniden başlatma günlükleri de kullanabilirsiniz. Ayrıntılar için bkz. [VM Yeniden Başlatma Günlüklerini Görüntüleme](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

tooprovide artıklık iki put veya hello yapılandırılmış VM'ler daha benzer şekilde aynı kullanılabilirlik kümesi. Bu, planlı veya planlanmamış bakım sırasında en az bir sanal makinenin kullanılabilir kalmasına yardımcı olur. Azure, bu yapılandırma için belirli düzeylerde VM kullanılabilirliği garantisi verir. Ayrıntılar için bkz [hello sanal makinelerin kullanılabilirliğini yönetme](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Ek kaynaklar
[Azure Sanal Makineleri hakkında](../articles/virtual-machines/virtual-machines-linux-about.md)

[Oluşturma ve yönetme Linux VM'ler ile Azure CLI hello](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure PowerShell ile Windows VM’leri Oluşturma ve Yönetme](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

