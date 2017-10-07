---
title: "aaaDebugging yayımlanan bir Azure bulut hizmeti Visual Studio ve IntelliTrace ile | Microsoft Docs"
description: "Nasıl toodebug bir bulut hizmeti Visual Studio ve IntelliTrace ile bilgi edinin"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Yayımlanan Azure bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama
IntelliTrace ile Azure içinde çalıştığında bir rol örneği için kapsamlı hata ayıklama bilgileri oturum açabilir. Toofind hello bir sorunun nedenini gerekiyorsa, Azure'da çalışıyormuş gibi hello IntelliTrace günlüklerini toostep Visual Studio kodunuzdan aracılığıyla kullanabilirsiniz. Gerçekte, Azure uygulamanız Azure'daki bir bulut hizmeti olarak çalışan ve olanak tanır, IntelliTrace anahtar kodu yürütme ve ortam verilerini kaydeder hello kaydedilen veri Visual Studio'dan yeniden yürütün. 

Visual Studio Enterprise varsa IntelliTrace ve Azure uygulamanızı hedeflerinizi .NET Framework 4 veya sonraki bir sürümünü kullanabilirsiniz. IntelliTrace Azure rollerinizi için bilgi toplar. Merhaba sanal makineler için her zaman 64-bit işletim sistemlerini çalıştıran bu rolleri.

Alternatif olarak, kullandığınız [uzaktan hata ayıklama](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach doğrudan Azure'da çalışan tooa bulut hizmeti.

> [!IMPORTANT]
> IntelliTrace yalnızca hata ayıklama senaryoları için tasarlanmıştır ve Üretim dağıtımı için kullanılmamalıdır.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>IntelliTrace için bir Azure uygulaması yapılandırma
tooenable IntelliTrace Azure uygulamaya ait oluşturmalı ve Visual Studio Azure project hello uygulamadan yayımlayın. TooAzure yayımlamadan önce Azure uygulamanız için IntelliTrace yapılandırmanız gerekir. IntelliTrace yapılandırmadan uygulamanızı yayımlamak, toorepublish hello proje gerekir. Daha fazla bilgi için bkz: [yayımlama bir Azure bulut hizmeti Visual Studio kullanarak projeleri](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Olduğunuzda toodeploy Azure uygulamanız hazır, projenizin yapı hedeflediği çok ayarlandığını doğrulayın**hata ayıklama**.

1. İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve, hello bağlam menüsünden seçin **Yayımla**.
   
1. Merhaba, **Azure uygulamasını Yayımla** iletişim kutusu, select hello Azure aboneliği ve select **sonraki**.

1. Merhaba, **ayarları** sayfası, select hello **Gelişmiş ayarları** sekmesi.

1. Merhaba üzerinde kapatma **IntelliTrace'i etkinleştirin** hello bulutta yayımlandığında, uygulamanız için toocollect IntelliTrace günlüklerini seçeneği.
   
1. toocustomize hello temel IntelliTrace yapılandırma, select **ayarları** sonraki çok**IntelliTrace'i etkinleştirin**.

    ![IntelliTrace ayarları bağlantısı](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. Merhaba, **IntelliTrace ayarları** iletişim kutusunda, hangi olayların toolog, toocollect arama bilgileri, hangi modüller ve işlemler toocollect günlüklerinde ve ne kadar alan tooallocate toohello kaydı belirtebilirsiniz. IntelliTrace hakkında daha fazla bilgi için bkz: [IntelliTrace ile hata ayıklama](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![IntelliTrace ayarları](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

Merhaba IntelliTrace günlük hello en büyük boyutunu (Merhaba varsayılan boyutu 250 MB'tır) hello IntelliTrace ayarlarında belirtilen döngüsel günlük dosyasıdır. IntelliTrace günlüklerini toplanan tooa dosyasında hello dosya sistemi hello sanal makinenin yer alır. Merhaba günlükleri istediğinde, bir anlık görüntü zamandaki o noktada alınır ve tooyour yerel bilgisayara indirilir.

Hello Azure bulut hizmeti yayımlanan tooAzure sağlandıktan sonra IntelliTrace hello Azure ' etkin olmadığını belirleyebilirsiniz düğümünde **Sunucu Gezgini**hello görüntü aşağıdaki gösterildiği gibi:

![Sunucu Gezgini - IntelliTrace etkin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Rol örneği için IntelliTrace günlüklerini indirin
Visual Studio kullanarak, aşağıdaki adımları izleyerek bir rol örneği için IntelliTrace günlüklerini yükleyebilirsiniz:

1. İçinde **Sunucu Gezgini**, hello genişletin **bulut Hizmetleri** düğümünü ve günlükleri toodownload istediğiniz rol örneği bulun. 

1. Merhaba rol örneği sağ tıklatın ve hello s bağlam menüsünden seçin **IntelliTrace günlüklerini görüntüle**. 

    ![IntelliTrace günlüklerini menü seçeneği görüntüleyin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. Merhaba IntelliTrace günlüklerini, yerel bilgisayarınızda indirilen tooa dosyasında bir dizin yer alır. Merhaba IntelliTrace günlüklerini, istek her zaman yeni bir anlık görüntüsü oluşturulur. Hello günlükleri karşıdan yüklenirken Visual Studio hello hello hello işlemin ilerlemesini görüntüler **Azure etkinlik günlüğü** penceresi. Hello aşağıdaki şekilde gösterildiği gibi daha fazla ayrıntı hello işlemi toosee hello kalem genişletebilirsiniz.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Merhaba IntelliTrace günlüklerini karşıdan yüklenirken Visual Studio'da toowork devam edebilirsiniz. Merhaba günlük yükleme tamamlandığında, Visual Studio açılır.

> [!NOTE]
> Merhaba IntelliTrace günlüklerini özel durumları içerebilir, hello framework oluşturur ve daha sonra işler. İç framework kod bunları güvenle yoksayabilirsiniz bir rolü, başlatma için normal bir parçası olarak bu özel durumları oluşturur.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
- [Azure bulut hizmetlerinde hata ayıklama seçenekleri](vs-azure-tools-debugging-cloud-services-overview.md)
- [Visual Studio kullanarak bir Azure bulut hizmetinde yayımlama](vs-azure-tools-publishing-a-cloud-service.md)