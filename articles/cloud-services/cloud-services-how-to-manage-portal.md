---
title: "aaaCommon bulut hizmeti yönetim görevleri | Microsoft Docs"
description: "Toomanage bulut hello Azure portal hizmetleri nasıl öğrenin. Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

Merhaba, **bulut Hizmetleri (Klasik)** alanı hello Azure portal, hizmet rolü veya bir dağıtım güncelleştirmek, aşamalı dağıtım tooproduction yükseltmek, yapabilirsiniz hello kaynak görebilmeniz için kaynakları tooyour bulut hizmeti bağlantı Bağımlılıklar ve ölçek kaynakları birlikte hello ve bir bulut hizmeti veya bir dağıtımı silin.

Nasıl tooscale bulut hizmetiniz kullanılabilir olduğu hakkında daha fazla bilgi [burada](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Nasıl yapılır: bir bulut hizmet rolü veya dağıtım güncelleştirme
Bulut hizmetiniz için tooupdate hello uygulama kodu gerekiyorsa kullanın **güncelleştirme** hello bulut hizmeti dikey. Tek bir rol veya tüm rolleri güncelleştirebilirsiniz. tooupdate, yeni hizmet paketi ya da hizmet yapılandırma dosyasını karşıya yükleyebilirsiniz.

1. Merhaba, [Azure portal][Azure portal], tooupdate istediğiniz hello bulut hizmeti seçin. Bu adım hello bulut hizmeti örneği dikey pencere açılır.
2. Merhaba dikey penceresinde hello tıklayın **güncelleştirme** düğmesi.

    ![Güncelleştir düğmesi](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Merhaba dağıtım yeni hizmet paketi dosyasının (.cspkg) ve hizmet yapılandırma dosyasının (.cscfg) ile güncelleştirin.

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **İsteğe bağlı olarak** hello dağıtım etiketi ve hello depolama hesabı güncelleştirin.
5. Herhangi bir rolü yalnızca bir rol örneği varsa, hello seçin **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** tooenable hello yükseltme tooproceed.

    Her role en az iki rol örnekleri (sanal makineler) varsa azure yalnızca 99,95 yüzde hizmet kullanılabilirliği bir bulut hizmet güncelleştirmesi sırasında garanti edebilir. Merhaba diğer güncelleştirilirken iki rol örneği ile bir sanal makine istemci isteklerini işler.

6. Denetleme **Başlat dağıtım** toohave hello güncelleştirme hello paketinin hello karşıya yükleme tamamlandıktan sonra uygulanır.
7. Tıklatın **Tamam** hello hizmeti güncelleştirme toobegin.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Nasıl yapılır: bir aşamalı dağıtım tooproduction dağıtımları toopromote değiştirme
Ne zaman toodeploy yeni sürümde bir bulut hizmeti, aşama karar verin ve yeni sürüm, bulut hizmeti hazırlama ortamınızda sınayın. Kullanım **takas** hangi hello iki dağıtım giderilmesini ve yeni bir sürüm tooproduction Yükselt tooswitch hello URL'leri.

Merhaba dağıtımlarından takas **bulut Hizmetleri** sayfa veya hello Pano.

1. Merhaba, [Azure portal][Azure portal], tooupdate istediğiniz hello bulut hizmeti seçin. Bu adım hello bulut hizmeti örneği dikey pencere açılır.
2. Merhaba dikey penceresinde hello tıklayın **takas** düğmesi.

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Merhaba aşağıdaki onay istemi açılır.

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Merhaba dağıtım bilgileri doğruladıktan sonra tıklatın **Tamam** tooswap hello dağıtımları.

    değişiklikleri hello tek şey hello sanal IP adresleri (VIP) olduğundan hello dağıtımı takas hello dağıtımları için hızlı bir şekilde gerçekleşir.

    toosave işlem maliyetleri, üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra dağıtım hazırlama hello silebilirsiniz.

### <a name="common-questions-about-swapping-deployments"></a>Dağıtımları değiştirme hakkında sık sorulan sorular

**Dağıtımları takas hello Önkoşullar nelerdir?**

Başarılı dağıtım Takas için iki anahtar Önkoşullar şunlardır:

- İçin üretim yuvası toouse statik bir IP adresi kullanmak isterseniz, bir hazırlama yuvası da ayırmanız gerekir. Aksi takdirde hello takas başarısız olur.

- Merhaba takas gerçekleştirmeden önce tüm örneklerini rollerinizi çalıştırması gerekir. Merhaba, örneklerini hello genel bakış dikey penceresinde hello Azure portal durumunu kontrol edebilirsiniz. Alternatif olarak, hello kullanabilirsiniz [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell komutu.

Konuk işletim sistemi güncelleştirmeleri ve hizmet işlemleri düzeltme dağıtım neden olabilir Not toofail değiştirir. Daha fazla bilgi için bkz: [bulut hizmeti dağıtım sorunlarını giderme](cloud-services-troubleshoot-deployment-problems.md).

**Bir takas Uygulamam için kapalı kalma süresi maliyetine neden olabilir mi? Bunu nasıl işlemesi gerekir?**

Yalnızca bir yapılandırma değişikliği hello Azure yük dengeleyici içinde olduğundan hello son bölümünde açıklandığı gibi bir dağıtımı takas genellikle hızlıdır. Bazı durumlarda, Bununla birlikte, en az on dakika sürer ve geçici bağlantı hatalarına neden. toolimit etkisi tooyour müşteriler, göz önünde bulundurun uygulama [istemci yeniden deneme mantığı](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Nasıl yapılır: bir kaynak tooa bulut hizmetine bağlama
Hello Azure portal birlikte hello geçerli Klasik Azure portalı yaptığı gibi kaynakları bağlantı vermiyor. Bunun yerine, ek kaynaklar toohello dağıtmak hello bulut hizmeti tarafından kullanılan aynı kaynak grubu.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Nasıl yapılır: dağıtımları ve bulut hizmeti Sil
Bir bulut hizmeti silebilmek için önce varolan her dağıtım silmeniz gerekir.

toosave işlem maliyetleri, üretim dağıtımınızın beklendiği gibi çalıştığını doğruladıktan sonra dağıtım hazırlama hello silebilirsiniz. İşlem maliyetleri durdurulur dağıtılan rol örnekleri için faturalandırılır.

Aşağıdaki yordam toodelete hello dağıtımı veya Bulut hizmetiniz kullanın.

1. Merhaba, [Azure portal][Azure portal], toodelete istediğiniz hello bulut hizmeti seçin. Bu adım hello bulut hizmeti örneği dikey pencere açılır.
2. Merhaba dikey penceresinde hello tıklayın **silmek** düğmesi.

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. Denetleyerek hello tüm bulut hizmeti silebilirsiniz **bulut hizmeti ve hizmetin dağıtımları** veya seçin ya da hello **Üretim dağıtımı** veya hello **hazırlama dağıtımı**.

    ![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Merhaba tıklatın **silmek** hello altındaki düğmesi.
5. toodelete hello bulut hizmeti tıklatın **Delete bulut hizmeti**. Merhaba onay isteminde ardından **Evet**.

> [!NOTE]
> Bir bulut hizmeti silindi ve ayrıntılı izleme yapılandırılmış hello veri depolama hesabınızdan el ile silmelisiniz. Burada toofind hello ölçümleri tabloları hakkında daha fazla bilgi için bkz: [bu](cloud-services-how-to-monitor.md) makalesi.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Nasıl yapılır: başarısız dağıtımları hakkında daha fazla bilgi
Merhaba **genel bakış** dikey penceresinde hello üstünde durum çubuğu vardır. Merhaba Çubuğu'nu tıklatın, yeni bir dikey pencere açar ve hata bilgilerini görüntüler. Merhaba dağıtım hatalarını içermiyorsa hello bilgi dikey boştur.

![Bulut Hizmetleri değiştirme](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).
