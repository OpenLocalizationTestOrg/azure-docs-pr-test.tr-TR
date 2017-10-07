---
title: "Azure için aaaCommand satır içi derleme | Microsoft Docs"
description: "Azure komut satırı derleme"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Merhaba komut satırından Azure projeler derleme
Merhaba Microsoft Build Engine (MSBuild) kullanarak, Visual Studio değil yüklendiği yapı Laboratuvar ortamlarında ürünleri oluşturabilir. MSBuild genişletilebilir ve Microsoft tarafından tam olarak desteklenen proje dosyaları için bir XML biçimi kullanır. Merhaba MSBuild dosya biçimini kullanarak, hangi öğeler olmalıdır açıklayabilirsiniz bir veya daha fazla platformlar ve yapılandırmaları için oluşturulmuştur.

Bu konu, bu yaklaşımı açıklar ve MSBuild hello komut satırında çalıştırabilirsiniz. Merhaba komut satırında özellikleri ayarlayarak, belirli yapılandırmaları bir proje oluşturabilirsiniz. Benzer şekilde, MSBuild derlemeler hello hedefleri tanımlayabilirsiniz. Komut satırı parametreleri ve MSBuild hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>MSBuild parametreleri
Merhaba en basit yolu toocreate bir paket olup toorun MSBuild hello ile `/t:Publish` seçeneği. Varsayılan olarak, bu komutu bir ilişkisi toohello kök klasöründe hello projesi için gibi dizini `<ProjectDirectory>\bin\Configuration\app.publish\`. Bir Azure projesi derlerken, iki dosya oluşturulur: Merhaba paket dosyasının kendisini ve hello eşlik eden yapılandırma dosyası:

* Paket dosyası (`project.cspkg`)
* Yapılandırma dosyası (`ServiceConfiguration.TargetProfile.cscfg`)

Varsayılan olarak, her Azure projesi yerel (hata ayıklama) yapılar için bir hizmet yapılandırma dosyası ve başka bir bulut (hazırlık veya üretim) derlemeleri içerir. Ancak, ekleyebilir veya gerektiği gibi hizmet yapılandırma dosyalarını kaldırabilirsiniz. Visual Studio içinde bir paket oluşturduğunuzda, hangi hizmet yapılandırma dosyası tooinclude hello paket yanında istenir. MSBuild kullanarak bir paket oluşturduğunuzda, hello yerel hizmet yapılandırma dosyası varsayılan olarak dahil edilir. tooinclude farklı bir hizmet yapılandırma dosyası, kümesi hello `TargetProfile` hello MSBuild komut özelliği (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Toouse istiyorsanız hello için alternatif bir dizin paketini ve yapılandırma dosyaları, hello kullanarak hello yolu ayarla depolanan `/p:PublishDir=Directory\` ters eğik çizgi ayırıcı sondaki hello dahil olmak üzere seçeneği.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba paket oluşturulduktan sonra tooAzure dağıtabilirsiniz. Gösteren bir öğretici için tooautomate işlem bkz [Azure bulut Hizmetleri için devamlı teslim](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

