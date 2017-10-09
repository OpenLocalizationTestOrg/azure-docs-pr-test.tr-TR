---
title: "aaaCreating hello Azure Marketi için bir sanal makine görüntüsü | Microsoft Docs"
description: "Nasıl toocreate bir sanal makine görüntü hello Azure Marketi başkaları için toopurchase ayrıntılı yönergeler için."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Kılavuzu toocreate hello Azure Marketi için bir sanal makine görüntüsü
Bu makalede **2. adım**, hello sanal sabit diskleri (VHD) toohello Azure Marketi dağıtacağınız hazırlama aracılığıyla anlatılmaktadır. Vhd'lerinizi, sku'sunun hello temelidir. Hello işlemi, bir Windows tabanlı veya Linux tabanlı SKU olup sağlanmaktadır bağlı olarak farklılık gösterir. Bu makalede her iki senaryoyu ele alınmaktadır. Bu işlem ile paralel olarak gerçekleştirilebilir [hesap oluşturma ve kayıt][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Teklifler ve SKU'ları tanımlayın
Bu bölümde, toodefine hello sunar ve ilişkili SKU'ları öğrenin.

Bir teklif, SKU "üst" tooall geçerlidir. Birden çok teklife sahip olabilirsiniz. Toostructure karar nasıl Teklifleriniz tooyou olur. Bir teklif toostaging gönderildiğinde tüm kendi SKU'ları ile birlikte gönderilir. Dikkatli bir şekilde hello URL'de görünür olacağından, SKU tanımlayıcıları göz önünde bulundurun:

* Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}
* Azure Önizleme portalı: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}  

Bir SKU hello ticari bir VM görüntüsü adıdır. Bir VM görüntüsü içeren bir işletim sistemi diski ve sıfır veya daha fazla veri diski. Temelde hello tam depolama profili için bir sanal makine içindir. Bir VHD her disk için gereklidir. Bile boş veri diskleri oluşturulan bir VHD toobe gerektirir.

Hangi işletim sistemine bağımsız olarak, yalnızca az sayıda veri diski hello SKU tarafından gerekli hello ekleyin. Müşteriler görüntünün bir parçasını hello dağıtım zamanında disklerinin kaldırılamıyor ancak bunları ihtiyacınız varsa her zaman diskleri sırasında veya dağıtımdan sonra ekleyebilirsiniz.

> [!IMPORTANT]
> **Yeni bir görüntü sürümü disk sayısı değiştirmeyin.** Merhaba görüntüsü'ndeki veri disklerinin yeniden yapılandırmanız gerekir, yeni bir SKU tanımlayın. Yeni bir görüntü sürümü farklı bir disk sayıları ile yayımlama hello yeni resim sürümünü otomatik ölçeklendirme, otomatik dağıtımları ARM şablonları ve diğer senaryolar aracılığıyla çözümlerinin durumlarda göre yeni dağıtım sonu, hello olası sahip olur.
>
>

### <a name="11-add-an-offer"></a>1.1 bir teklif ekleyin
1. İçinde toohello oturum [yayımlama portalında] [ link-pubportal] seller hesabınızı kullanarak.
2. Select hello **sanal makineleri** hello yayımlama portalında sekmesinde. Merhaba istendiğinde giriş alanına teklif adınızı girin. Merhaba teklif adı genellikle hello hello ürün veya hizmet hello Azure Marketi toosell planlama adıdır.
3. **Oluştur**’u seçin.

### <a name="12-define-a-sku"></a>1.2 bir SKU tanımlayın
Bir teklif ekledikten sonra toodefine gerekir ve, SKU'ları tanımlayın. Birden çok teklifleri olabilir ve her teklif birden çok SKU'ları altındaki olabilir. Bir teklif toostaging gönderildiğinde tüm kendi SKU'ları ile birlikte gönderilir.

1. **Bir SKU ekleyin.** Merhaba SKU hello URL'SİNDE kullanılan bir tanımlayıcı gerektirir. Hello tanımlayıcı yayımlama profili içinde benzersiz olmalıdır, ancak diğer yayımcı ile tanımlayıcı çakışma riski vardır.

   > [!NOTE]
   > Merhaba teklif ve SKU tanımlayıcıları hello teklif hello Market URL'de görüntülenir.
   >
   >
2. **SKU için Özet açıklama ekleyin.** Özet açıklamaları görünür toocustomers olduğundan, kolay okunabilir yapmanız. Bu bilgiler hello "Anında iletme tooStaging" aşamasında kadar kilitli toobe gerekmez. Ücretsiz tooedit olduğunuz o zamana kadar bu.
3. Windows tabanlı SKU'ları kullanıyorsanız, hello önerilen bağlantıları izleyin tooacquire hello Windows Server sürümlerinde olduğu onaylandı.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. (Linux tabanlı) bir Azure uyumlu VHD oluşturma
Bu bölümde hello Azure Marketi için bir Linux tabanlı VM görüntüsü oluşturmak için en iyi uygulamalar odaklanır. Bir adım adım kılavuz için belgeleri aşağıdaki toohello bakın: [oluşturma ve bir Sanal Sabit Disk, CONTAINS karşıya hello Linux işletim sistemi](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. (Windows tabanlı) bir Azure uyumlu VHD oluşturma
Bu bölümde Azure Marketi hello için Windows Server tabanlı bir SKU hello adımları toocreate odaklanır.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>Hello kullandığınız 3.1 olun temel VHD düzeltin
Merhaba işletim sistemi VHD VM görüntüsü için Windows Server veya SQL Server içeren Azure onaylı temel görüntüde dayalı olması gerekir.

toobegin, görüntüler, hello bulunan aşağıdaki hello birinden bir VM oluşturma [Microsoft Azure portal][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1] [link-datactr-2008-r2])
* SQL Server 2014 ([Kurumsal][link-sql-2014-ent], [standart][link-sql-2014-std], [Web] [ link-sql-2014-web])
* SQL Server 2012 SP2'yi ([Kurumsal][link-sql-2012-ent], [standart][link-sql-2012-std], [Web] [ link-sql-2012-web])

Bu bağlantılar da hello yayımlama portalında hello SKU sayfanın altında bulunabilir.

> [!TIP]
> Merhaba geçerli Azure portal veya PowerShell kullanıyorsanız, Windows Server görüntülerini 8 Eylül 2014 yayınlanan ve üzeri onaylanır.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2, Windows tabanlı VM oluşturma
Merhaba Microsoft Azure Portal'dan, yalnızca birkaç basit adımda onaylanmış bir temel görüntü göre VM oluşturabilirsiniz. Merhaba, hello işlemine genel bakış verilmiştir:

1. Merhaba temel görüntü sayfasında seçin **sanal makine oluşturma** toobe toohello yeni yönlendirilmiş [Microsoft Azure portal][link-azure-portal].

    ![Çizim][img-acom-1]
2. Merhaba Microsoft hesabı ile toohello portal ve parolayı hello toouse istediğiniz Azure aboneliği için oturum açın.
3. Seçtiğiniz hello temel görüntü kullanılarak Hello istemleri toocreate VM izleyin. Tooprovide bir ana bilgisayar adı (Merhaba bilgisayar adı), (yönetici olarak kayıtlı) kullanıcı adı ve parola Merhaba VM gerekir.

    ![Çizim][img-portal-vm-create]
4. Merhaba VM toodeploy Hello boyutunu seçin:

    a.    Toodevelop hello VHD şirket içi planlıyorsanız, hello boyutu önemli değildir. Merhaba birini kullanmayı daha küçük VM'ler.

    b.    Toodevelop hello Azure görüntüde planlıyorsanız, VM boyutları hello seçilen görüntü için önerilen hello birini kullanarak göz önünde bulundurun.

    c.    Fiyatlandırma bilgileri için toohello başvuran **fiyatlandırma katmanlarına önerilen** hello portalında görüntülenen Seçici. Bunu hello hello yayımcı tarafından sağlanan üç önerilen boyut sağlar. (Bu durumda, Microsoft hello yayımcı olur.)

    ![Çizim][img-portal-vm-size]
5. Özellikleri ayarlayın:

    a.    Hızlı dağıtım için hello altında hello özellikleri için varsayılan değer bırakabilirsiniz **isteğe bağlı yapılandırma** ve **kaynak grubu**.

    b.    Altında **depolama hesabı**, hello depolama hesabı işletim sistemi hangi hello VHD depolanacağı isteğe bağlı olarak seçebilirsiniz.

    c.    Altında **kaynak grubu**, isteğe bağlı olarak hangi tooplace hello VM hello mantıksal grup seçebilirsiniz.
6. Select hello **konumu** dağıtımı için:

    a.    Toodevelop hello VHD şirket içi planlıyorsanız, hello görüntü tooAzure daha sonra karşıya yükleyecek çünkü hello konumu önemli değildir.

    b.    Toodevelop hello Azure görüntüde planlıyorsanız, hello ABD tabanlı Microsoft Azure bölgelerinden hello başından kullanmayı düşünün. Bu sertifika için görüntünüzü gönderdiğinizde, Microsoft sizin adınıza gerçekleştiren hello VHD kopyalama işlemini hızlandırır.

    ![Çizim][img-portal-vm-location]
7. **Oluştur**'a tıklayın. Merhaba VM toodeploy başlatır. Dakika içinde başarılı bir dağıtım sahip olur ve toocreate hello görüntü SKU için başlayabilir.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3, VHD hello bulutta geliştirin
Uzak Masaüstü Protokolü (RDP) kullanarak, VHD hello bulutta geliştirmek öneririz. Merhaba kullanıcı adı ve parolayla sağlama işlemi sırasında belirtilen tooRDP bağlayın.

> [!IMPORTANT]
> VHD geliştiriyorsanız (hangi önerilmez) şirket içi, bkz: [şirket içi bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md). VHD indirme hello bulutta geliştiriyorsanız gerekli değildir.
>
>

**Hello kullanarak RDP aracılığıyla bağlanma [Microsoft Azure portalı][link-azure-portal]**

1. Seçin **Gözat** > **VM'ler**.
2. Merhaba sanal makineleri dikey pencere açılır. Bu hello tooconnect ile istediğiniz VM çalışıyorsa ve dağıtılan VM'ler hello listeden seçip emin olun.
3. Seçili VM hello açıklayan bir dikey penceresini açar. Merhaba üstünde tıklatın **Bağlan**.
4. İstendiğinde tooenter hello kullanıcı adı ve sağlama işlemi sırasında belirtilen parola var.

**PowerShell kullanarak RDP aracılığıyla bağlanma**

bir Uzak Masaüstü dosyası tooa yerel makine toodownload kullanmak hello [Get-AzureRemoteDesktopFile cmdlet'i][link-technet-2]. Bu cmdlet toouse sipariş, tooknow hello hello hizmetin adını ve hello VM adını gerekir. Hello hello VM oluşturduysanız [Microsoft Azure portal][link-azure-portal], bu bilgileri VM Özellikleri'nin altında bulabilirsiniz:

1. Merhaba Microsoft Azure Portalı'nda seçin **Gözat** > **VM'ler**.
2. Merhaba sanal makineleri dikey pencere açılır. Merhaba, dağıtılan VM seçin.
3. Seçili VM hello açıklayan bir dikey penceresini açar.
4. **Özellikler**'e tıklayın.
5. Merhaba ilk hello etki alanı adı hello hizmet adı bölümüdür. Merhaba ana bilgisayar adı hello VM adıdır.

    ![Çizim][img-portal-vm-rdp]
6. oluşturulan hello VM toohello yöneticinin yerel Masaüstü için Hello cmdlet toodownload hello RDP dosyası aşağıdaki gibidir.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

RDP hakkında daha fazla bilgi MSDN'de hello makalesinde bulunabilir [tooan Azure VM RDP veya SSH ile bağlantı](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Bir VM yapılandırın ve, SKU oluşturun**

Merhaba işletim sistemi VHD indirilir sonra SKU oluşturma VM toobegin yapılandırmak ve Hyper-v kullanın. Ayrıntılı adımlar TechNet bağlantı aşağıdaki hello bulunabilir: [HyperV yükleme ve yapılandırma VM](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 hello doğru VHD boyutu seçin
VM görüntünüzdeki Hello Windows işletim sistemi VHD 128 GB sabit biçimli VHD oluşturulmalıdır.  

Merhaba fiziksel boyutu 128 GB daha az ise, hello VHD seyrek olmalıdır. sağlanan hello temel Windows ve SQL Server görüntüler zaten bu gereksinimleri karşılayan, böylece hello biçimi veya hello boyutunu VHD elde hello değiştirmeyin.  

Veri diskleri 1 TB'ye kadar büyük olabilir. Merhaba disk boyutuna karar verirken, müşterilerin dağıtımının hello zaman içinde bir görüntü VHD'ler boyutlandırılamıyor unutmayın. Veri diski VHD'leri sabit biçimli VHD oluşturulmalıdır. Bunlar ayrıca seyrek olmalıdır. Veri diskleri boş olabilir veya veri içerebilir.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 Merhaba en son Windows düzeltme eklerinin yükleyin
Merhaba taban görüntüleri içeren hello en son düzeltme eklerinin tootheir yayımlanan tarih. Merhaba işletim sistemi VHD yayımlamadan önce oluşturmuş olduğunuz, Windows Update'i çalıştırın ve tüm son kritik hello ve önemli güncelleştirmelerin yüklendiğinden emin olun.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 gerektiği gibi ek yapılandırma ve zamanlama görevleri gerçekleştirme
Ek yapılandırma gerekli olursa, onu dağıtıldıktan sonra tüm son değişiklikleri toohello VM başlangıç toomake sırasında çalışan zamanlanmış bir görev kullanmayı dikkate alın:

* Bu en iyi yöntem toohave hello görev silme kendisini aktarılmadığı olur.
* Bunlar her zaman tooexist garanti hello yalnızca iki sürücüleri olduğundan herhangi bir yapılandırma C veya D sürücüsü dışındaki sürücülerde yararlanmalıdır. C sürücüsünün hello işletim sistemi diski ve sürücü D hello geçici yerel disk.

### <a name="37-generalize-hello-image"></a>3.7 Merhaba görüntü generalize
Hello Azure Marketi tüm görüntüleri genel bir şekilde yeniden kullanılabilir olması gerekir. Diğer bir deyişle, hello işletim sistemi VHD genelleştirilmiş gerekir:

* Windows için "sysprepped" Merhaba görüntü olmalıdır ve hiçbir yapılandırmaları hello desteklemeyen yapılmalıdır **sysprep** komutu.
* Merhaba dizin % windir%\System32\Sysprep komutu aşağıdaki hello çalıştırabilirsiniz.

        sysprep.exe /generalize /oobe /shutdown

  MSDN makalesine aşağıdaki hello adımda toosysprep hello işletim sistemini nasıl sağlandığını konusunda yönergeler: [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Vhd'lerinizi VM'den dağıtma
Vhd'lerinizi (Merhaba genelleştirilmiş bir işletim sistemi ve VHD disk sıfır veya daha fazla veri) karşıya sonra tooan Azure depolama hesabı, size kaydolabilir bunları bir kullanıcı VM görüntüsü olarak. Ardından, görüntü test edebilirsiniz. İşletim sisteminizi VHD genelleştirilmiş olmadığından, doğrudan hello VM hello VHD URL'si sağlayarak dağıtamayacağınızı unutmayın.

toolearn VM görüntüleri hakkında daha fazla blog gönderileri aşağıdaki gözden geçirme hello:

* [VM görüntüsü](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM görüntüsü PowerShell nasıl yapılır](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Azure'da VM görüntüleri hakkında](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Merhaba gerekli araçlarını Kur, PowerShell ve Azure CLI
* [Nasıl toosetup PowerShell](/powershell/azure/overview)
* [Nasıl toosetup Azure CLI](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 kullanıcı VM görüntüsü oluşturma
#### <a name="capture-vm"></a>VM yakalama
Lütfen hello PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen hello bağlantılar okuyun.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Görüntü generalize
Lütfen hello PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen hello bağlantılar okuyun.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 bir kullanıcı VM görüntüsü VM'den dağıtma
bir kullanıcı VM görüntüsü VM'den toodeploy, kullanabileceğiniz hello geçerli [Azure portal](https://manage.windowsazure.com) veya PowerShell.

**Merhaba geçerli Azure portalından bir VM'yi dağıtmak**

1. Çok Git**yeni** > **işlem** > **sanal makine** > **galerisinden**.

    ![Çizim][img-manage-vm-new]
2. Çok Git**görüntülerim**, ve ardından seçin hangi toodeploy VM görüntüsünü VM hello:

   1. Ödeme Kapat dikkat toowhich görüntüsü seçin, çünkü hello **görüntülerim** işletim sistemi görüntüleri ve VM görüntüleri listeler.
   2. Diskleri Hello numaradan arayan VM görüntüleri hello çoğunluğu olduğu için birden fazla disk görüntüsü hangi türü, dağıttığınız, belirlenmesine yardımcı olabilir. Ancak, yine olası toohave sonra olması gereken bir tek işletim sistemi diskle bir VM görüntüsü olan **disk sayısı** too1 ayarlayın.

      ![Çizim][img-manage-vm-select]
3. Merhaba VM Oluşturma Sihirbazı'nı izleyin ve hello VM adı, VM boyutu, konum, kullanıcı adı ve parola belirtin.

**PowerShell VM'den dağıtma**

Yeni oluşturduğunuz VM görüntüsü hello büyük bir VM'den genelleştirilmiş toodeploy cmdlet'leri aşağıdaki hello kullanabilirsiniz.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Ek Yardım için lütfen [VHD oluşturma sırasında karşılaşılan sorun giderme ortak sorunları] bakın.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. VM görüntüsü için sertifika elde
VM görüntüsü hello Azure Marketi hazırlama hello sonraki sertifikalı toohave adımıdır.

Merhaba doğrulama sonuçları toohello karşıya Vhd'lerinizi bulunduğu Azure kapsayıcı, bir teklif ekleme, SKU tanımlama ve VM gönderme görüntü için sertifika, bu işlem özel sertifika aracını çalıştıran içerir.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 indirin ve Azure sertifikalı hello sertifika Test aracı çalıştırın
Merhaba sertifika Aracı kullanıcı VM görüntüden sağlanan çalışan bir VM için VM görüntüsü hello tooensure Microsoft Azure ile uyumludur. Merhaba yönerge ve, VHD hazırlama hakkında gereksinimleri karşılandıktan doğrular. Merhaba hello aracın çıktısının hello yayımlama portalında sırasında istekte bulunan sertifika karşıya yüklenmelidir uyumluluk rapordur.

Merhaba sertifika aracı, Windows ve Linux VM'ler ile kullanılabilir. TooWindows tabanlı VM'ler PowerShell aracılığıyla bağlanır ve tooLinux VM'ler SSH.Net üzerinden bağlanır:

1. İlk olarak, hello hello sertifika aracını indirin [Microsoft İndirme sitesi][link-msft-download].
2. Merhaba sertifikası aracını açın ve hello ardından **yeni Testi Başlat** düğmesi.
3. Merhaba gelen **Test bilgi** ekranında, hello test çalışması için bir ad girin.
4. VM'nizin Linux üzerinde veya Windows üzerinde çalıştığına ilişkin seçim yapın. Seçim bağlı olarak, hello sonraki seçenekleri seçin.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Merhaba sertifika aracı tooa Linux VM görüntüsü Bağlan**
1. Select hello SSH kimlik doğrulama modu: parola veya anahtar dosyası.
2. Parola tabanlı kimlik doğrulamasını kullanıyorsanız, hello etki alanı adı sistemi (DNS) adı, kullanıcı adı ve parola girin.
3. Anahtar dosyası kimlik doğrulamasını kullanıyorsanız, hello DNS adı, kullanıcı adı ve özel anahtar konumu girin.

   ![Linux VM görüntüsü parola kimlik doğrulaması][img-cert-vm-pswd-lnx]

   ![Linux VM görüntüsü anahtar dosyası kimlik doğrulaması][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Merhaba sertifika aracı tooa Windows tabanlı VM görüntü Bağlan**
1. Tam hello VM DNS adını (örneğin, MyVMName.Cloudapp.net) girin.
2. Merhaba kullanıcı adı ve parola girin.

   ![Windows VM görüntüsünü parola kimlik doğrulaması][img-cert-vm-pswd-win]

Linux veya Windows tabanlı VM görüntü için hello doğru seçeneklerini seçtikten sonra Seç **Bağlantıyı Sına** tooensure SSH.Net veya PowerShell test etmek için geçerli bir bağlantı vardır. Bağlantı kurulduktan sonra Seç **sonraki** toostart hello test.

Merhaba test tamamlandıktan sonra her bir test öğesi için hello sonuçları (Geçiş/başarısız/uyarı) alırsınız.

![Linux VM görüntüsü için test çalışmaları][img-cert-vm-test-lnx]

![Windows VM görüntüsü için test çalışmaları][img-cert-vm-test-win]

Merhaba testleri hiçbirini başarısız olursa, görüntünüzü uygunluğu onaylanmamıştır. Bu gerçekleşirse, hello gereksinimleri gözden geçirin ve gerekli değişiklikleri yapın.

Test Hello otomatik sonra VM görüntüsüne bir soru formu ekran aracılığıyla tooprovide ek giriş istenir.  Merhaba soruları tamamlayın ve ardından **sonraki**.

![Sertifika aracı anket][img-cert-vm-questionnaire]

![Sertifika aracı anket][img-cert-vm-questionnaire-2]

Merhaba soru tamamladıktan sonra hello Linux VM görüntüsü için SSH erişim bilgileri gibi ek bilgileri ve başarısız tüm değerlendirmeleri için bir açıklama sağlar. Merhaba test sonuçları indirmek ve günlük dosyalarının hello yürütülen test çalışmaları için ek tooyour yanıtlar toohello soru. Hello Hello Sonuçları Kaydet Vhd'lerinizi aynı kapsayıcı.

![Test sonuçları sertifika Kaydet][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 hello paylaşılan erişim imzası URI için VM görüntülerini alın.
İşlem yayımlama hello sırasında hello SKU için oluşturduğunuz VHD'leri tooeach sağlama hello Tekdüzen Kaynak Tanımlayıcıları (URI'ler) belirtin. Microsoft access toothese VHD'ler hello sertifika işlemi sırasında gerekir. Bu nedenle, her VHD için bir paylaşılan erişim imzası URI toocreate gerekir. Merhaba girilmesi URI budur **görüntüleri** hello yayımlama portalında sekmesindedir.

Merhaba paylaşılan erişim imzası oluşturulan URI gereksinimlerine toohello uyması:

* Paylaşılan erişim imzası URI'ler Vhd'lerinizi için oluştururken, liste ve Okuma izinleri yeterlidir. Yazma veya Silme erişimi sağlamayın.
* Merhaba paylaşılan erişim imzası URI oluşturulduğunda hello süresi erişim için üç (3) hafta ila en az olmalıdır.
* toosafeguard hello geçerli tarih seçin hello günün UTC saati için. Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.

SAS URL olabilir içinde birden çok yol tooshare, VHD için Azure Marketi oluşturulur.
Aşağıdaki 3 önerilen araçları hello:

1.  Azure Depolama Gezgini
2.  Microsoft Storage Gezgini
3.  Azure CLI

**Azure Depolama Gezgini (Windows kullanıcıları için önerilir)**

Azure Storage Gezgini kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir

1. Karşıdan [Azure Storage Gezgini 6 Önizleme 3](https://azurestorageexplorer.codeplex.com/) Codeplex. Çok Git[Azure Storage Gezgini 6 Önizleme](https://azurestorageexplorer.codeplex.com/) tıklatıp **"İndirmeleri"**.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Karşıdan [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) ve unzipping sonra yükleyin.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Yüklendikten sonra hello uygulamasını açın.
4. Tıklatın **hesabı eklemek**.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Merhaba depolama hesabı adı, depolama hesabı anahtarı ve depolama uç noktaları etki alanı belirtin. Azure Portalı'nda, VHD'yi nerede tutulur Azure aboneliğinizde hello depolama hesap budur.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Azure Storage Gezgini bağlandıktan sonra tooyour belirli bir depolama hesabı, bu tüm hello içeren hello depolama hesabında gösteren başlayacak. Merhaba işletim sistemi disk VHD dosyasını (senaryonuz için uygun olup olmadığını da veri diskleri) kopyaladığınız hello kapsayıcısı seçin.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Merhaba blob kapsayıcısı seçtikten sonra Azure Storage Gezgini hello kapsayıcıdaki hello dosyaları gösteren başlatır. Gönderilen toobe gereken hello görüntü dosyası (.vhd) seçin.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Merhaba kapsayıcısında Hello .vhd dosyası seçtikten sonra hello tıklatın **güvenlik** sekmesi.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  Merhaba, **Blob kapsayıcı güvenlik** iletişim kutusu, hello bırakın hello varsayılanlarına **erişim düzeyi** sekmesini ve ardından **paylaşılan erişim imzaları** sekmesi.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Toogenerate hello .vhd görüntüsü için paylaşılan erişim imzası URI Hello adımları izleyin:

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Erişime izin:** toosafeguard hello geçerli tarih seçin hello günün UTC saati için. Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.

    b. **Erişime izin:** en az 3 hafta hello sonra bir tarihi seçin **erişime izin** tarih.

    c. **İzin verilen eylemleri:** Select hello **listesi** ve **okuma** izinleri.

    d. .Vhd dosyası doğru seçtiğiniz sonra dosyanızı görünür **Blob adı tooaccess** uzantısı .vhd ile.

    e. Tıklatın **imzayı üretmek**.

    f. İçinde **oluşturulan paylaşılan erişim imzası URI bu kapsayıcının**, yukarıda vurgulandığı aşağıdaki hello denetle:

       - Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** hello URI şunlardır.
       - Merhaba imza Hello sonunda olduğundan emin olun **"rl ="** görüntülenir. Bu, okuma ve liste erişim başarıyla sağlandı gösterir.
       - Merhaba imza ortadaki olduğundan emin olun **"sr c ="** görüntülenir. Bu kapsayıcı düzeyinde erişime sahip olması gösterir

11. oluşturulan hello tooensure paylaşılan erişim imzası URI çalışır, tıklatın **tarayıcısında Test**. Merhaba indirme işlemi başlamanız gerekir.

12. Merhaba paylaşılan erişim imzası URI kopyalayın. Merhaba URI toopaste hello yayımlama portalında içine budur.

13. Merhaba SKU'ndaki her VHD için 6-10 adımları yineleyin.

**Microsoft Azure Depolama Gezgini (MAC/Windows/Linux)**

Microsoft Azure Storage Gezgini kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir

1.  Microsoft Azure Storage Gezgini form karşıdan [http://storageexplorer.com/](http://storageexplorer.com/) Web sitesi. Çok Git[Microsoft Azure Storage Gezgini](http://storageexplorer.com/releasenotes.html) tıklatıp **"Windows için karşıdan yükleme"**.

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Yüklendikten sonra hello uygulamasını açın.

3.  Tıklatın **hesabı eklemek**.

4.  Microsoft Azure Storage Gezgini tooyour abonelik tooyour hesabında oturum yapılandırın

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Toostorage hesabı gidin ve hello kapsayıcısı seçin

6.  Seçin **"Paylaşımı erişim imzası Al …"** Merhaba, sağ tıklatma kullanarak **kapsayıcı**

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Aşağıdaki gibi başına başlangıç zamanı, bitiş saati ve izinleri güncelleştirme

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Başlangıç saati:** toosafeguard hello geçerli tarih seçin hello günün UTC saati için. Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.

    b.  **Sona erme saati:** en az 3 hafta hello sonra bir tarihi seçin **başlangıç saati** tarih.

    c.  **İzinleri:** Select hello **listesi** ve **okuma** izinleri

8.  Kapsayıcı paylaşılan erişim imzası URI kopyalayın

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    Oluşturulan SAS URL için düzeyi kapsayıcıdır ve şimdi biz tooadd VHD adı da gerekir.

    Kapsayıcı düzeyi SAS URL biçimi:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Aşağıdaki şekilde hello kapsayıcı adı SAS URL sonra VHD adı Ekle`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Örnek:

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    VHD SAS URL hello VHD adı TestRGVM201631920152.vhd olduğundan`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** hello URI şunlardır.
    - Merhaba imza ortadaki olduğundan emin olun **"sp rl ="** görüntülenir. Bu, okuma ve liste erişim başarıyla sağlandı gösterir.
    - Merhaba imza ortadaki olduğundan emin olun **"sr c ="** görüntülenir. Bu kapsayıcı düzeyinde erişime sahip olması gösterir

9.  oluşturulan paylaşılan erişim imzası URI works hello tooensure tarayıcıda sınayın. Merhaba indirme işlemi başlamanız gerekir

10. Merhaba paylaşılan erişim imzası URI kopyalayın. Merhaba URI toopaste hello yayımlama portalında içine budur.

11. Merhaba SKU'ndaki her VHD için bu adımları yineleyin.

**Azure CLI (Windows dışı & sürekli tümleştirme için önerilir)**

Azure CLI kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir

1.  Microsoft Azure CLI üzerinden indirme [burada](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Farklı bağlantıları için bulabileceğiniz  **[Windows](http://aka.ms/webpi-azure-cli)**  ve  **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Bir kez yüklenir, lütfen yükleyin

3.  Aşağıdaki kod ile bir PowerShell dosyası oluşturun ve yerel Kaydet

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Merhaba aşağıdaki güncelleştirme yukarıda parametreleri

    a. **`<StorageAccountName>`**: Depolama hesabınızın adını verin

    b. **`<Storage Account Key>`**: Depolama hesabı anahtarınızı verin

    c. **`<Permission Start Date>`**: toosafeguard hello geçerli tarih seçin hello günün UTC saati için. Örneğin, hello geçerli tarihidir 26 Ekim 2016 sonra değeri 25/10/2016

    d. **`<Permission End Date>`**: En az 3 hafta hello sonra bir tarihi seçin **başlangıç tarihi**. Değerin olması **02/11/2016**.

    Uygun parametreleri güncelleştirdikten sonra hello örnek kod aşağıda verilmiştir

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  "Yönetici olarak çalıştır" moduyla PowerShell Düzenleyicisi'ni açın ve #3. adımda dosyasını açın.

5.  Kapsayıcı düzeyinde erişimi için SAS URL hello çalışma hello komut dosyası ve sağlar

    Aşağıdaki hello SAS imza ve kopyalama vurgulanmış hello bölümü bir Not Defteri'nde hello çıktısını olacaktır

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Kapsayıcı düzeyi SAS URL artık alacak ve tooadd VHD adı da gerekir.

    Kapsayıcı düzeyi SAS URL #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Aşağıda gösterildiği gibi hello kapsayıcı adı SAS URL sonra VHD adı Ekle`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Örnek:

    VHD SAS URL hello VHD adı TestRGVM201631920152.vhd olduğundan

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Yansıma Dosya adı ve ".vhd" Merhaba URI olduğundan emin olun.
    -   Merhaba imza ortadaki olduğundan emin olun "sp rl =" görüntülenir. Bu, okuma ve liste erişim başarıyla sağlandı gösterir.
    -   Merhaba imza ortadaki olduğundan emin olun "sr c =" görüntülenir. Bu kapsayıcı düzeyinde erişime sahip olması gösterir

8.  oluşturulan paylaşılan erişim imzası URI works hello tooensure tarayıcıda sınayın. Merhaba indirme işlemi başlamanız gerekir

9.  Merhaba paylaşılan erişim imzası URI kopyalayın. Merhaba URI toopaste hello yayımlama portalında içine budur.

10. Merhaba SKU'ndaki her VHD için bu adımları yineleyin.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 hello VM görüntü ile ilgili bilgileri sağlayın ve hello Yayımlama Portalı sertifika isteği
Teklif ve SKU oluşturduktan sonra SKU ile ilişkili hello görüntü ayrıntıları girmeniz gerekir:

1. Toohello Git [yayımlama portalında][link-pubportal]ve satıcının hesabınızla oturum açın.
2. Select hello **VM görüntüleri** sekmesi.
3. Merhaba hello sayfanın başında listelenen hello gerçekte hello teklif tanımlayıcısı ve hello SKU tanımlayıcısı tanımlayıcısıdır.
4. Merhaba özellikleri hello altında doldurmak **SKU'ları** bölümü.
5. Altında **işletim sistemi ailesi**, VHD hello işletim sistemiyle ilişkili hello işletim sistemi türü'nü tıklatın.
6. Merhaba, **işletim sistemi** kutusunda, hello işletim sistemi tanımlar. İşletim sistemi ailesi, türü, sürüm ve güncelleştirmeler gibi bir biçim göz önünde bulundurun. "Windows Server Datacenter 2014 R2." örneğidir
7. Sanal makine boyutlarını önerilen toosix seçin. Bunlar toopurchase karar verin ve görüntünüzü dağıtmak, görüntülenen toohello müşteri hello fiyatlandırma katmanı dikey penceresinde hello Azure Portal almak önerilerdir. **Bunlar yalnızca önerilerdir. Merhaba müşteri yansımanıza hello diskleri düzenler herhangi bir VM boyutta belirtilen mümkün tooselect olur.**
8. Merhaba sürümü girin. Merhaba sürüm alanı bir anlamsal sürüm tooidentify hello ürün ve kendi güncellemeleri yalıtır:
   * Sürümleri X, Y ve Z tamsayılar nerede X.Y.Z hello biçiminde olmalıdır.
   * Farklı SKU'ları görüntülerinde farklı birincil ve ikincil sürümleri olabilir.
   * İçinde bir SKU sürümlerinde yalnızca hello düzeltme eki sürümü (Z X.Y.Z gelen) artırmak artımlı değişiklikler olmalıdır.
9. Merhaba, **OS VHD URL'si** kutusuna, hello paylaşılan erişim imzası hello işletim sistemi VHD için oluşturulan URI girin.
10. Bu SKU ile ilişkili veri disklerinin varsa, bu veri diski toobe dağıtım takılı istediğiniz hello mantıksal birim numarası (LUN) toowhich seçin.
11. Merhaba, **LUN X VHD URL'si** kutusuna, hello paylaşılan erişim imzası oluşturulan hello ilk veri VHD URI girin.

    ![Çizim](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Ortak SAS URL sorunları ve düzeltmeleri

|Sorun|Hata iletisi|Düzeltme|Belge bağlantı|
|---|---|---|---|
|Kopyalama hatası görüntüleri - "?" SAS URL'si bulunamadı|Hata: Görüntüleri kopyalama. Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.|Güncelleştirme hello SAS URL'yi kullanarak önerilen araçları|[https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Görüntüleri kopyalama hatası - SAS URL'si değil, "st" ve "se" parametreleri|Hata: Görüntüleri kopyalama. Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.|Başlangıç ve bitiş tarihleri üzerindeki ile güncelleştirme hello SAS URL'si|[https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Görüntüleri - "sp rl SAS url değil =" kopyalama hatası|Hata: Görüntüleri kopyalama. SAS URI'sini sağlanan blob erişilemiyor toodownload kullanarak|"Okuma" & "listesi olarak ayarla izinlerle güncelleştirme hello SAS URL'si|[https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Görüntüleri - SAS url kopyalama hatası vhd adlarında boşluk sahip|Hata: Görüntüleri kopyalama. Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.|Boşluk olmadan güncelleştirme hello SAS URL'si|[https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Görüntüleri – SAS Url yetkilendirmesi hata kopyalama hatası|Hata: Görüntüleri kopyalama. Tooauthorization hatası nedeniyle erişilemiyor toodownload blob|Merhaba SAS Url yeniden oluştur|[https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Sonraki adım
Merhaba SKU ayrıntılarla tamamladıktan sonra İleri toohello taşıyabilirsiniz [Azure Marketi pazarlama içerik Kılavuzu][link-pushstaging]. İşlem yayımlama hello Bu adım çok pazarlama içeriği, fiyatlandırma ve diğer bilgileri gerekli önceki hello sağlamak**adım 3: VM sınama teklif hazırlamada**, burada dağıtmadan önce çeşitli kullanım örneği senaryoları test Genel görünürlük için Azure Marketi teklifi toohello hello ve satın alma.  

## <a name="see-also"></a>Ayrıca bkz.
* [Başlarken: nasıl toopublish bir teklif toohello Azure Market](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
