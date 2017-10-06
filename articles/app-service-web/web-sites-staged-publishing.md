---
title: "Hazırlık ortamları için Azure App Service'te web uygulamalarını yukarı aaaSet | Microsoft Docs"
description: "Toouse yayımlama Azure App Service'deki web uygulamaları için nasıl hazırlanır öğrenin."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Hazırlık Azure App Service ortamları ayarlama
<a name="Overview"></a>

Dağıttığınızda, web uygulaması, Linux, mobil arka uç ve API uygulaması web uygulaması çok[uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), tooa ayrı bir dağıtım yuvası hello varsayılan üretim yuvasına yerine hello çalıştırırken dağıtabilirsiniz **standart**veya **Premium** uygulama hizmeti planı modu. Dağıtım yuvaları, kendi ana bilgisayar adları ile gerçekten Canlı uygulamalardır. Uygulama içeriği ve yapılandırmaları öğeleri hello üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir. Uygulama tooa dağıtım yuvası dağıtma hello aşağıdaki faydaları vardır:

* Hello üretim yuvasıyla değiştirmeden önce hazırlık dağıtım yuvasındaki uygulama değişikliklerini doğrulayabilirsiniz.
* Bir uygulama tooa yuvaya ilk dağıtma ve üretim ile değiştirmeden hello yuvası tüm örneklerini üretime takas önce warmed olduğunu sağlar. Uygulamanızı dağıttığınızda bu kapalı kalma süresini ortadan kaldırır. Merhaba trafik yeniden yönlendirmesi sorunsuzdur ve değiştirme işlemleri sonucunda hiçbir istek bırakılır. Yapılandırarak bu iş akışının tamamı otomatikleştirilebilir [otomatik takas](#Auto-Swap) zaman öncesi takas doğrulama gerekli değildir.
* Değiştirme işleminden sonra önceden hazırlanmış uygulama hello yuvasıyla hello önceki üretim uygulama artık sahiptir. Beklendiği gibi hello üretim yuvasına hello değişiklikleri varsa, tooget "son bilinen iyi sitenizi" geri hemen aynı takas hello gerçekleştirebilirsiniz.

Her bir uygulama hizmeti planı modu dağıtım yuvaları farklı sayıda destekler. yuva sayısı hello çıkışı toofind uygulamanızın modunu destekliyorsa, bkz: [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).

* Uygulamanız birden çok yuvası olduğunda, hello modunu değiştiremezsiniz.
* Ölçeklendirme için üretim dışı yuvası kullanılabilir değil.
* Bağlantılı kaynak yönetimi için üretim dışı yuvası desteklenmiyor. Merhaba, [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) geçici olarak hello üretim dışı yuvası tooa farklı uygulama hizmeti planı modu taşıyarak bu olası etkisini üretim yuvasına yalnızca önleyebilirsiniz. Bu hello üretim dışı yuvası hello yine paylaşması Not hello iki yuvaları takas önce hello üretim yuvası ile aynı mod.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Bir dağıtım yuvası Ekle
hello Hello uygulamayı çalıştıran **standart** veya **Premium** modunda sipariş, tooenable için birden çok dağıtım yuvası.

1. Merhaba, [Azure Portal](https://portal.azure.com/), uygulamanızın açmak [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Merhaba seçin **dağıtım yuvası** seçeneğini ve ardından **yuva Ekle**.
   
    ![Yeni bir dağıtım yuvası Ekle][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Merhaba uygulama hello değilse **standart** veya **Premium** modu hazırlanmış yayımlamayı etkinleştirmek için desteklenen hello modları belirten bir ileti alırsınız. Bu noktada, hello seçeneği tooselect sahip **yükseltme** toohello giderek **ölçek** devam etmeden önce uygulamanızın sekmesi.
   > 
   > 
3. Merhaba, **bir yuva eklemek** dikey penceresinde hello yuvası bir ad verin ve seçin olup olmadığını başka bir var olan dağıtım yuvadan tooclone uygulama yapılandırması. Merhaba onay işareti toocontinue'ı tıklatın.
   
    ![Yapılandırma kaynağı][ConfigurationSource1]
   
    Merhaba bir yuva eklediğiniz ilk kez, yalnızca iki seçenek gerekir: kopya yuvadan yapılandırma hello varsayılan üretim ya da hiç.
    Birkaç yuvaları oluşturduktan sonra üretim hello dışında bir yuvadan mümkün tooclone yapılandırma olacaktır:
   
    ![Yapılandırma kaynakları][MultipleConfigurationSources]
4. Uygulamanızın kaynak dikey penceresinde tıklayın **dağıtım yuvası**, ölçümleri ve diğer herhangi bir uygulama gibi yapılandırma kümesi ile Bu yuvanın kaynak dikey bir dağıtım yuvası tooopen'ye tıklayın. Merhaba hello yuva adını gösterilen hello dikey tooremind hello üstünde görüntülemekte olduğunuz, dağıtım yuvası hello.
   
    ![Dağıtım yuvası başlığı][StagingTitle]
5. Merhaba yuvanın dikey penceresinde Hello uygulama URL'Sİ'ı tıklatın. Merhaba dağıtım yuvası kendi ana bilgisayar adı olan hem de dinamik uygulama dikkat edin. toolimit genel erişim toohello dağıtım yuvası bkz [App Service Web uygulaması – blok web erişim toonon üretim dağıtım yuvaları](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Dağıtım yuvası oluşturulduktan sonra içerik yok. Farklı depo dalından veya tamamen farklı bir depo toohello yuvadan dağıtabilirsiniz. Merhaba yuvanın yapılandırmasını da değiştirebilirsiniz. Kullanım hello içerik güncelleştirmeleri hello dağıtım yuvası ile ilişkili profil veya dağıtım kimlik bilgilerini yayımlayın.  Örneğin, [toothis yuvası git ile yayımlama](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Dağıtım yuvası için yapılandırma
Başka bir dağıtım yuvası yapılandırmasından kopyaladığınızda hello kopyalanan düzenlenebilir yapılandırmadır. Ayrıca, diğer yapılandırma öğeleri aynı değiştirme işleminden sonra (Yuva belirli) yuva hello kalır ancak bazı yapılandırma öğeleri takas (değil yuva belirli) hello içeriği izler. Merhaba aşağıdaki listeleri yuvaları takas yükleyen değiştirecek hello yapılandırmasını gösterir.

**Değiştirilen ayarları**:

* -Framework sürümü, 32/64-bit, Web yuvaları gibi genel ayarları
* Uygulama ayarları (yapılandırılmış toostick tooa yuvası olabilir)
* Bağlantı dizeleri (yapılandırılmış toostick tooa yuvası olabilir)
* İşleyici eşlemeleri
* İzleme ve tanılama ayarları
* Web işleri içeriği

**Değil takas ayarları**:

* Yayımlama uç noktaları
* Özel etki alanı adları
* SSL sertifikaları ve bağlamaları
* Ölçek ayarları
* Web işleri zamanlayıcılar

tooconfigure (takas değil), bir uygulama ayarı veya bağlantı dizesi toostick tooa yuvaya erişim hello **uygulama ayarları** belirli yuvası sonra select hello için dikey **yuva ayarı** hello kutusu Merhaba yuvası takılıyor yapılandırma öğeleri. Yuva belirli o öğeye hello uygulamayla ilişkili tüm hello dağıtım yuvaları arasında swappable oluşturma hello etkisi gibi bir yapılandırma öğesi işaretleme unutmayın.

![Yuva ayarları][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Dağıtım yuvalarını değiştirme 
Merhaba dağıtım yuvaları takas **genel bakış** veya **dağıtım yuvası** uygulamanızın kaynak dikey penceresinin görünümü.

> [!IMPORTANT]
> Üretime bir uygulamadan bir dağıtım yuvası takas önce tüm yuva olmayan belirli ayarları tıpkı toohave istediğiniz şekilde yapılandırılmış olduğundan emin olun hello değiştirme hedefi içinde.
> 
> 

1. tooswap dağıtım yuvaları, tıklatın hello **takas** düğmesi hello uygulamasının hello komut çubuğunda veya dağıtım yuvasının komut çubuğunda hello.
   
    ![Değiştirme düğmesi][SwapButtonBar]

2. Merhaba takas kaynak ve takas hedefleyen düzgün şekilde ayarlandığını doğrulayın. Genellikle, hello takas hello üretim yuvasına hedefidir. Tıklatın **Tamam** toocomplete hello işlemi. Merhaba işlemi bittikten sonra hello dağıtım yuvaları takas.

    ![Değiştirmeyi Tamamla](./media/web-sites-staged-publishing/SwapImmediately.png)

    Hello için **Önizleme ile değiştirme** değiştirme türü için bkz: [(çok aşaması takas) önizleme ile değiştirme](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>(Çok aşaması takas) önizleme ile değiştirme

Önizleme ile değiştirme ya da çok aşaması takas yuvası özel yapılandırma öğeleri, bağlantı dizeleri gibi doğrulama basitleştirin.
Kritik iş yükleri için uygulama hello toovalidate hello üretim yuvanın yapılandırmasını uygulandığında beklendiği gibi davranır istediğiniz ve böyle doğrulama gerçekleştirmelisiniz *önce* hello uygulama üretime takas. Önizleme ile değiştirme ihtiyacınız olur.

> [!NOTE]
> Linux üzerinde web uygulamalarında Önizleme ile değiştirme desteklenmez.

Merhaba kullandığınızda **Önizleme ile değiştirme** seçeneği (bkz [dağıtım yuvaları takas](#Swap)), uygulama hizmeti hello aşağıdaki:

- Tutar hello hedef yuvası değişmemiş şekilde mevcut iş yüküne o yuva (örneğin, üretim) etkilenmez.
- Merhaba yuvası özgü bağlantı dizeleri ve uygulama ayarları dahil hello hedef yuva toohello kaynak yuvaya, Hello yapılandırma öğeleri için geçerlidir.
- Bu daha önce bahsedilen yapılandırma öğeleri kullanarak hello kaynak yuvaya Hello çalışan işlemleri yeniden başlatır.
- Merhaba takas tamamlandığında: hello hedef yuvaya taşır hello öncesi warmed yukarı kaynak yuvaya. Merhaba hedef yuvaya el ile değiştirme gibi hello kaynak yuvasına taşınır.
- İptal zaman hello takas: hello kaynak yuva toohello kaynak yuvaya hello yapılandırma öğeleri yeniden uygular.

Merhaba uygulama hello hedef yuvanın yapılandırma ile tam olarak nasıl davranacak önizleyebilirsiniz. Doğrulama tamamlandığında, ayrı bir adım hello değiştirmeyi tamamlayın. Bu adım hello kaynak yuvaya zaten hello istenen yapılandırma ile warmed ve istemcilerin kapalı kalma süresi karşılaşmazsınız fayda hello sahiptir.  

Hello Azure PowerShell cmdlet'leri çok aşaması takas için kullanılabilir için örnek hello dağıtım yuvası bölümü için Azure PowerShell cmdlet'leri dahil edilmiştir.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Otomatik Takas yapılandırın
Otomatik Takas ölçeklendirerek toocontinuously istediğiniz DevOps senaryoları hello uygulama son müşteriler için sıfır cold start ve sıfır kapalı kalma süresi ile uygulamanızı dağıtın. Kod güncelleştirme toothat yuvası itme her zaman bir dağıtım yuvası üretim ortamına otomatik takas için yapılandırıldığında, onu zaten hello yuvasına warmed sonra uygulama hizmeti otomatik olarak hello uygulama üretime değiştireceksiniz.

> [!IMPORTANT]
> Otomatik Takas yuvası için etkinleştirdiğinizde, tam olarak hello hedef yuva (genellikle hello üretim yuvasına) için hedeflenen hello yapılandırma hello yuvası yapılandırması olduğundan emin olun.
> 
> 

> [!NOTE]
> Otomatik Takas web uygulamaları Linux üzerinde desteklenmiyor.

Otomatik Takas yuvası için yapılandırma kolaydır. Merhaba adımları izleyin:

1. İçinde **dağıtım yuvası**, bir üretim dışı yuva seçin ve **uygulama ayarları** Bu yuvanın kaynak dikey penceresinde.  
   
    ![][Autoswap1]
2. Seçin **üzerinde** için **otomatik takas**seçin hello istenen hedef yuvada **otomatik takas yuvası**, tıklatıp **kaydetmek** hello komut çubuğunda. Tam olarak hello hedef yuva için hedeflenen hello yapılandırma hello yuvası için yapılandırma olduğundan emin olun.
   
    Merhaba **bildirimleri** flash yeşil sekmesi **başarı** hello işlemi tamamlandıktan sonra.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest otomatik takas uygulamanız için bir üretim dışı hedef yuvada ilk seçebilirsiniz **otomatik takas yuvası** toobecome hello özelliğiyle tanıdık.  
   > 
   > 
3. Bir kod itme toothat dağıtım yuvası yürütün. Otomatik Takas kısa bir süre sonra gerçekleşir ve hello güncelleştirme hedef yuvanın URL'de yansıtılır.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback takas sonra bir üretim uygulaması
Bir yuva değişikliğinden sonra üretimde herhangi bir hata belirlenirse, hello yuvaları hello aynı iki hemen yuvayı değiştirerek geri tootheir öncesi takas durumları alma.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Takas önce özel Isınma
Bazı uygulamalar özel Isınma Eylemler gerekebilir. Merhaba `applicationInitialization` web.config dosyasındaki yapılandırma öğesi sağlar, toospecify özel başlatma eylemleri toobe gerçekleştirilen bir isteği almadan önce. Merhaba değiştirme işlemi için bu özel Isınma toocomplete bekler. Bir örnek web.config parçası değil.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete bir dağıtım yuvası
Açık hello dağıtım yuvanın dikey penceresinde, bir dağıtım yuvası için hello dikey penceresine tıklayın **genel bakış** (Merhaba varsayılan sayfa) tıklatıp **silmek** hello komut çubuğunda.  

![Bir dağıtım yuvası Sil][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Dağıtım yuvaları için Azure PowerShell cmdlet'leri
Azure PowerShell cmdlet'leri toomanage Azure uygulama hizmeti dağıtım yuvalarında yönetmek için destek dahil olmak üzere Windows PowerShell üzerinden Azure sağlayan bir modüldür.

* Yükleme ve yapılandırma Azure PowerShell ve Azure PowerShell'i Azure aboneliğiniz ile kimlik doğrulaması hakkında bilgi için bkz: [nasıl tooinstall ve Microsoft Azure PowerShell yapılandırma](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Web uygulaması oluşturma
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Bir dağıtım yuvası oluşturma
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Gözden geçirme (çok aşaması takas) ile değiştirme başlatmak ve hedef yuvası yapılandırması toosource yuvaya Uygula
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Bekleyen bir değiştirme (gözden geçirme ile değiştirme) iptal kaynak yuvası yapılandırması ve geri yükleme
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Dağıtım yuvalarını değiştirme
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Dağıtım yuvası Sil
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Dağıtım yuvaları için Azure komut satırı arabirimi (Azure CLI) komutları
Hello Azure CLI, uygulama hizmeti dağıtım yuvaları yönetmek için destek dahil olmak üzere, Azure ile çalışmak için platformlar arası komutları sağlar.

* Azure CLI yükleme ve yapılandırma hakkında yönergeler hello için hakkında bilgi de dahil olmak üzere tooconnect Azure CLI tooyour Azure aboneliği bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md).
* hello Azure CLI, Azure App Service için kullanılabilir toolist hello komutlarını çağıran `azure site -h`.

> [!NOTE] 
> İçin [Azure CLI 2.0](https://github.com/Azure/azure-cli) bkz: dağıtım yuvaları için komutları [az appservice web dağıtım yuvası](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>Azure site listesi
Merhaba geçerli abonelikte hello uygulamalar hakkında daha fazla bilgi için arama **azure site listesi**, aşağıdaki örneğine hello gibi.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>Azure sitesi oluştur
bir dağıtım yuvası toocreate çağrısı **azure sitesi oluşturmak** ve var olan bir uygulamanın hello adı ve örnek aşağıdaki hello olduğu gibi hello yuvası toocreate hello adını belirtin.

`azure site create webappslotstest --slot staging`

Merhaba yeni yuva, kullanım hello tooenable kaynak denetimi **--git** aşağıdaki örneğine hello olduğu gibi seçeneği.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>Azure site değiştirme
toomake güncelleştirilen dağıtım yuvası hello üretim uygulama Merhaba, hello kullan **azure site takas** komutu tooperform aşağıdaki örneğine hello gibi bir değiştirme işlemi. Merhaba üretim uygulamasına herhangi kesinti karşılaşmazsınız veya cold start yapılacaktır.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>Azure site Sil
toodelete artık bir dağıtım yuvası hello kullanmak gerekli **azure sitesi silme** aşağıdaki örneğine hello olduğu gibi komutu.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Bir web uygulamasını çalışırken görün. [App Service'i deneyin](https://azure.microsoft.com/try/app-service/) hemen bir kısa süreli başlangıç uygulaması oluşturun — gerekli herhangi bir kredi kartı veya bir taahhüt.
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
[Azure App Service Web uygulaması – web erişim toonon üretim dağıtım yuvalarını engelleme](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[giriş tooApp Linux hizmette](./app-service-linux-intro.md)
[Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

