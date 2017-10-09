---
title: "aaaCommon bulut hizmeti yönetim görevleri (Klasik) | Microsoft Docs"
description: "Toomanage bulut hello Klasik Azure portalı hizmetleri nasıl öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>TooManage Cloud Services nasıl
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-manage-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-manage.md)
>
>

Merhaba, **bulut Hizmetleri** alanı hello Klasik Azure portalı, bir hizmet rolü veya bir dağıtım güncelleştirmek, aşamalı dağıtım tooproduction yükseltmek, yapabilirsiniz hello kaynak görebilmeniz için kaynakları tooyour bulut hizmeti bağlantı Bağımlılıklar ve ölçek kaynakları birlikte hello ve bir bulut hizmeti veya bir dağıtımı silin.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Nasıl yapılır: bir bulut hizmet rolü veya dağıtım güncelleştirme
Bulut hizmetiniz için tooupdate hello uygulama kodu gerekiyorsa kullanın **güncelleştirme** hello Panoda **bulut Hizmetleri** sayfasında veya **örnekleri** sayfa. Tek bir rol veya tüm rolleri güncelleştirebilirsiniz. Tooupload yeni bir hizmet paketi ve hizmet yapılandırma dosyası gerekir.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), hello Panoda **bulut Hizmetleri** sayfasında veya **örnekleri** sayfasında, **güncelleştirme**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. İçinde **dağıtım etiketi**, bir ad tooidentify hello dağıtımı (örneğin, mycloudservice4) girin. Merhaba dağıtım etiketin altında bulabilirsiniz **Hızlı Başlangıç** hello Panoda.
3. İçinde **paket**, kullanın **Gözat** tooupload hello hizmet paketi dosyasının (.cspkg).
4. İçinde **yapılandırma**, kullanın **Gözat** tooupload hello hizmet yapılandırma dosyasının (.cscfg).
5. İçinde **rol**seçin **tüm** tooupgrade istiyorsanız hello tüm rollerde bulut hizmeti. select hello rol tooupdate istediğiniz tooperform tek bir rol güncelleştirin. Belirli bir rol tooupdate seçseniz bile hello güncelleştirmeleri hello hizmet yapılandırma dosyasında uygulanan tooall rolleridir.
6. Rol sayısı veya herhangi bir rolü hello boyutunu Hello güncelleştirme değişiklikleri Merhaba, hello seçin **rol boyutları veya rollerin sayısı değişirse güncelleştirmeye izin ver** onay kutusunu tooenable hello güncelleştirme tooproceed.

    Bir rol (diğer bir deyişle, bir rol örneği barındıran bir sanal makinenin hello boyutu) hello boyutunu değiştirme veya rol sayısı Merhaba, her rol örneği (sanal makine) görüntüsü yüklenmiş olması gerekir ve tüm yerel veriler kaybolacak unutmayın.

7. Herhangi bir hizmet rolü yalnızca bir rol örneği varsa, hello seçin **bir veya daha fazla rol içeriyor olsa bile bir tek örnek onay kutusu güncelleştirme** tooenable hello yükseltme tooproceed.

    Her role en az iki rol örnekleri (sanal makineler) varsa azure yalnızca 99,95 yüzde hizmet kullanılabilirliği bir bulut hizmet güncelleştirmesi sırasında garanti edebilir. Merhaba diğer güncelleştirilirken, bir sanal makine tooprocess istemci isteklerini etkinleştirir.

8. Tıklatın **Tamam** (onay işareti) toobegin hello hizmeti güncelleştirme.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Nasıl yapılır: bir aşamalı dağıtım tooproduction dağıtımları toopromote değiştirme
Kullanım **takas** toopromote bir bulut hizmeti tooproduction hazırlama dağıtımı. Toodeploy bir bulut hizmetinin yeni bir sürüm karar verdiğinizde, aşama ve müşterileriniz üretim hello geçerli sürüm kullanırken yeni sürüm, bulut hizmeti hazırlama ortamınızda sınayın. Hazır olduğunuzda toopromote Merhaba yeni sürüm tooproduction, kullanabileceğiniz **takas** tooswitch hello URL'leri tarafından hangi hello iki dağıtımları açıklanmıştır.

Merhaba dağıtımlarından takas **bulut Hizmetleri** sayfa veya hello Pano.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**.
2. Bulut Hizmetleri Hello listesinde hello bulut hizmeti tooselect tıklayın.
3. Tıklatın **takas**.

    Merhaba aşağıdaki onay istemi açılır.

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Merhaba dağıtım bilgileri doğruladıktan sonra tıklatın **Evet** tooswap hello dağıtımları.

    değişiklikleri hello tek şey hello sanal IP adresleri (VIP) olduğundan hello dağıtımı takas hello dağıtımları için hızlı bir şekilde gerçekleşir.

    toosave işlem maliyetleri hello yeni üretim dağıtımı beklenen şekilde çalıştığını emin olduğunuzda ortam hazırlama hello hello dağıtımda silebilirsiniz.

### <a name="common-questions-about-swapping-deployments"></a>Dağıtımları değiştirme hakkında sık sorulan sorular

**Dağıtımları takas hello Önkoşullar nelerdir?**

Başarılı dağıtım Takas için iki anahtar Önkoşullar şunlardır:

- İçin üretim yuvası toouse statik bir IP adresi kullanmak isterseniz, bir hazırlama yuvası da ayırmanız gerekir. Aksi takdirde hello takas başarısız olur.

- Merhaba takas gerçekleştirmeden önce tüm örneklerini rollerinizi çalıştırması gerekir. Örneklerinizin hello Klasik Azure portalı veya kullanarak hello durumunu kontrol edebilirsiniz [Windows PowerShell komutu Get-AzureRole hello](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Konuk işletim sistemi güncelleştirmelerini ve hizmet işlemleri düzeltme dağıtım takasları toofail ayrıca neden olabileceğini unutmayın. Bkz: [bulut hizmeti dağıtım sorunlarını giderme](cloud-services-troubleshoot-deployment-problems.md) daha fazla ayrıntı için.

**Bir takas Uygulamam için kapalı kalma süresi maliyetine neden olabilir mi? Bunu nasıl işlemesi gerekir?**

Yalnızca bir yapılandırma değişikliği hello Azure yük dengeleyici içinde olduğundan hello son bölümünde açıklandığı gibi bir dağıtımı takas genellikle çok hızlıdır. Bazı durumlarda, Bununla birlikte, en az on dakika sürer ve geçici bağlantı hatalarına neden. toolimit etkisi tooyour müşteriler, göz önünde bulundurun uygulama [istemci yeniden deneme mantığı](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Nasıl yapılır: bir kaynak tooa bulut hizmetine bağlama
tooshow bulut hizmetinizin bağımlılıkları kaynaklar üzerinde Azure SQL veritabanı örneği veya bir depolama hesabı toohello bulut hizmeti bağlayabilirsiniz. Bağlantı ve hello kaynaklardaki bağlantısını **bağlı kaynaklar** sayfasında ve ardından kullanımları hello bulut hizmetinin panosunda izleyebilirsiniz. Bağlantılı Depolama hesabına açık izleme varsa, toplam istek sayısı hello bulut hizmetinin panosunda izleyebilirsiniz.

Kullanım **bağlantı** toolink yeni veya var olan SQL veritabanı örneği veya depolama hesabı tooyour bulut hizmeti. Ardından hello veritabanı üzerinde hello kullanarak hello bulut hizmet rolü ile birlikte ölçeklendirebilirsiniz **ölçek** sayfası. (Bir depolama hesabı kullanımı arttıkça otomatik olarak ölçeklendirir.) Daha fazla bilgi için bkz: [nasıl tooScale bir bulut hizmeti ve bağlı kaynaklar](cloud-services-how-to-scale.md).

Ayrıca izleyebilir, yönetme ve hello hello veritabanı ölçeklendirme **veritabanları** hello Klasik Azure portalı düğümünün.

"Bu bağlamda bir kaynak bağlama" uygulama toohello kaynağınız bağlanmıyor. Kullanarak yeni bir veritabanı oluşturursanız **bağlantı**, tooadd hello bağlantı dizeleri tooyour uygulama kodu ve ardından yükseltme hello bulut hizmeti olması gerekir. Uygulamanız bir bağlantılı depolama hesabında kaynakları kullanıyorsa tooadd bağlantı dizeleri de gerekir.

Aşağıdaki yordamı hello nasıl toolink yeni bir SQL veritabanı örneğinde dağıtılan bir yeni SQL veritabanı sunucusunda tooa bulut hizmeti açıklar.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink bir SQL veritabanı örneği tooa bulut hizmeti
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**. Ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
2. Tıklatın **bağlı kaynakları**.

    Merhaba **bağlı kaynaklar** sayfası açılır.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Ya da tıklatın **bir kaynağı bağladıktan** veya **bağlantı**.

    Merhaba **bağlantı kaynak** Sihirbazı'nı başlatır.

    ![Bağlantı Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Tıklatın **yeni bir kaynak oluşturmak** veya **mevcut bir kaynağı bağlayın**.
5. Kaynak toolink Hello türünü seçin. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **SQL veritabanı**. (Yalnızca hello Klasik Azure portalı, bir depolama hesabı tooa bulut hizmeti bağlama destekler.)
6. toocomplete hello veritabanı yapılandırması, hello Yardımı'ndaki yönergeleri izleyin **SQL veritabanları** hello Klasik Azure portalı alanı.

    Merhaba ileti alanı işlemde bağlama hello hello ilerlemesini izleyebilirsiniz.

    Bağlama tamamlandığında, bağlantılı hello kaynak hello bulut hizmetinin panosundaki hello durumunu izleyebilirsiniz. Bağlantılı bir SQL veritabanı ölçeklendirme hakkında daha fazla bilgi için bkz: [nasıl tooScale bir bulut hizmeti ve bağlı kaynaklar](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>bağlantılı kaynak toounlink
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**. Ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
2. Tıklatın **bağlı kaynaklar**ve ardından hello kaynak seçin.
3. Tıklatın **bağlantısını**. Ardından **Evet** hello onay isteminde.

    Bir SQL veritabanı bağlantısını hello veritabanı veya hello uygulamanın bağlantıları toohello veritabanı üzerinde etkisi yoktur. Merhaba hello veritabanında yönetmeye devam edebilirsiniz **SQL veritabanları** hello Klasik Azure portalı alanı.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Nasıl yapılır: dağıtımları ve bulut hizmeti Sil
Bir bulut hizmeti silebilmek için önce varolan her dağıtım silmeniz gerekir.

Üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra toosave işlem maliyetleri hazırlama dağıtımınızı silebilirsiniz. Bir bulut hizmeti çalışmıyor olsa bile, rol örnekleri için faturalanan işlem maliyetleri demektir.

Aşağıdaki yordam toodelete hello dağıtımı veya Bulut hizmetiniz kullanın.

1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**.
2. Merhaba bulut hizmeti seçin ve ardından **silmek**. (tooselect hello Pano açmadan bir bulut hizmeti tıklatın herhangi bir yere hello bulut hizmeti girişinde hello adı dışında.)

    Hazırlık veya üretim dağıtımında varsa, bir hello pencerenin hello altındaki aşağıdaki seçimleri benzer toohello menüsüne görürsünüz. Merhaba bulut hizmeti silebilmek için önce var olan tüm dağıtımları silmeniz gerekir.

    ![Menü silme](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete bir dağıtım tıklatın **silmek Üretim dağıtımı** veya **hazırlama dağıtımı silin**. Merhaba onay isteminde ardından **Evet**.
4. Toodelete hello bulut hizmeti planlıyorsanız, adım 3, gerekirse, toodelete diğer dağıtımınızı yineleyin.
5. toodelete hello bulut hizmeti tıklatın **Delete bulut hizmeti**. Merhaba onay isteminde ardından **Evet**.

> [!NOTE]
> Ayrıntılı izleme bulut hizmetiniz için yapılandırılmışsa, Azure depolama hesabınızdaki verileri hello bulut hizmeti sildiğinizde izleme hello silmez. Toodelete hello verileri el ile gerekir. Burada toofind hello ölçümleri tabloları hakkında daha fazla bilgi için bkz: "nasıl yapılır: erişim hello Klasik Azure portalı dışında ayrıntılı izleme verileri" içinde [tooMonitor Cloud Services nasıl](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).
