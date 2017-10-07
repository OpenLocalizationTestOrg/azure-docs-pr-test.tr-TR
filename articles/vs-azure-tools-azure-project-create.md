---
title: bir Azure bulut hizmeti projesini Visual Studio ile aaaCreating | Microsoft Docs
description: "Şimdi toocreate bir Azure bulut hizmeti projesini Visual Studio ile bilgi edinin"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Visual Studio ile bir Azure bulut hizmeti projesi oluşturma
Hello Azure Araçları Visual Studio için Azure bulut hizmeti oluşturmanıza olanak sağlayan bir proje şablonu sağlar. Visual Studio Hello Proje oluşturulduktan sonra tooconfigure sağlar, hata ayıklama ve hello bulut hizmeti tooAzure dağıtın.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Adımları toocreate Visual Studio'da bir Azure bulut hizmeti projesi
Bu bölümde bir veya daha fazla web rolleri ile Visual Studio'da bir Azure bulut hizmeti projesi oluşturmada size yol gösterir.  

1. Visual Studio'yu yönetici olarak başlatın.

1. Merhaba ana menüde seçin **dosya** > **yeni** > **proje**.

1. Seçin **bulut** hello Visual C# veya Visual Basic proje şablonu düğümleri ve seçin **Azure bulut hizmeti** şablonları hello listesinden.

    ![Yeni Azure bulut hizmeti](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Merhaba projenizin toouse toodevelop istediğiniz .NET Framework sürümünü belirtin.

1. Bir ad ve projenizin konumunu ve hello çözüm için bir ad girin. 

1. **Tamam**’ı seçin.

1. Merhaba, **yeni Microsoft Azure bulut hizmeti** iletişim, tooadd istediğiniz ve hello sağ ok düğmesine tooadd seçin select hello rolleri bunları tooyour çözümü.

    ![Yeni Azure bulut hizmeti rollerinizi seçin](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename eklediğiniz, bir rol hello hello rolünde gidildiğinde **yeni Microsoft Azure bulut hizmeti** iletişim kutusunda ve hello bağlam menüsünden seçin **yeniden adlandırma**. Bir rol, çözümünüz içinde adlandırabilirsiniz (Merhaba içinde **Çözüm Gezgini**) eklendikten sonra.

    ![Azure bulut hizmeti rolü yeniden adlandır](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Merhaba Visual Studio Azure project hello çözümde ilişkilendirmeleri toohello rol proje yok. Merhaba proje de hello içeriyor *hizmet tanımı dosyası* ve *hizmet yapılandırma dosyası*:

- **Hizmet tanımı dosyası** -uygulama, hangi rollerin gerekli dahil olmak üzere, uç noktaları ve sanal makine boyutu hello çalışma zamanı ayarlarını tanımlar. 
- **Hizmet yapılandırma dosyası** -kaç bir rolün örnekleri çalıştırılır ve hello bir rol için tanımlanan hello ayarlarının değerleri yapılandırır. 

Bu dosyalar hakkında daha fazla bilgi için bkz: [hello rolleri bir Azure bulut hizmeti için Visual Studio ile yapılandırma](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Sonraki adımlar
- [Visual Studio ile Azure bulut hizmeti projelerinde rollerini yönetme](./vs-azure-tools-cloud-service-project-managing-roles.md)
