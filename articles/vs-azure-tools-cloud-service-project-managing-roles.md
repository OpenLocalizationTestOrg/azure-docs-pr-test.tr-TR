---
title: aaaManaging rolleri Azure bulut Hizmetleri'ni Visual Studio ile | Microsoft Docs
description: "Nasıl tooadd ekleme ve kaldırma rolleri Azure bulut hizmetlerine Visual Studio ile bilgi edinin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Azure bulut Hizmetleri'ni Visual Studio ile rollerini yönetme
Azure bulut hizmetinizi oluşturduktan sonra yeni rol tooit ekleyebilir veya var olan rollerini kaldırın. Ayrıca, mevcut bir projeyi alın ve tooa rol dönüştürün. Örneğin, bir ASP.NET web uygulamasını almak ve bir web rolü olarak belirleyin.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Bir rol tooan Azure bulut hizmeti ekleme
Aşağıdaki adımları hello Visual Studio'da bir web veya çalışan rolü tooan Azure bulut hizmeti projesini eklerken size kılavuzluk.

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin

1. Sağ hello **rolleri** düğümü toodisplay hello bağlam menüsü. Merhaba bağlam menüsünden seçin **Ekle**, bir var olan web rolü veya çalışan rolü hello geçerli çözümden seçin veya bir web veya çalışan rolü projesi oluşturun. Ayrıca, bir ASP.NET web uygulaması projesini gibi uygun bir projeyi seçin ve rol projesi ile ilişkilendirebilirsiniz.

    ![Menü seçeneklerini tooadd bir rol tooan Azure bulut hizmeti projesi](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Bir Azure bulut hizmetinden bir rolünü kaldırma
Hello aşağıdaki adımlarda size bir Azure bulut hizmeti projesini Visual Studio'da web veya çalışan rolü kaldırma aracılığıyla yol.

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin

1. Merhaba genişletin **rolleri** düğümü.

1. Tooremove isterseniz ve, hello bağlam menüsünden seçin sağ hello düğümü **kaldırmak**. 

    ![Menü seçeneklerini tooadd rol tooan Azure bulut hizmeti](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Bir rol tooan Azure bulut hizmeti projesini yeniden ekleniyor
Bulut hizmeti projenizden rolü kaldırmak, ancak daha sonra geri tooadd hello rol karar toohello proje, yalnızca hello rol bildirim ve uç noktaları ve tanılama bilgileri gibi temel öznitelikler eklenir. Ek kaynaklar veya başvuruları toohello eklenen `ServiceDefinition.csdef` dosya ya da toohello `ServiceConfiguration.cscfg` dosya. Bu bilgiler tooadd istiyorsanız, toomanually gerekir bu dosyaları geri ekleyin.

Örneğin, bir web hizmeti rolü kaldırabilir ve daha sonra bu rolü geri tooadd çözümünüze karar. Bunu yaparsanız, bir hata oluşur. tooprevent bu hatayı tooadd hello sahip `<LocalResources>` XML geri hello aşağıdaki hello gösterilen öğesinin `ServiceDefinition.csdef` dosya. Kullanım hello hello hello name özniteliği bir parçası olarak geri hello projeye eklenen hello web hizmeti rolü adını  **<LocalStorage>**  öğesi. Bu örnekte, hello hello web hizmeti rolü adıdır **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Sonraki adımlar
- [Visual Studio ile Merhaba rolleri bir Azure bulut hizmeti için yapılandırma](vs-azure-tools-configure-roles-for-cloud-service.md)
