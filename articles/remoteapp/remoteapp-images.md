---
title: "aaaWhat hello Azure RemoteApp şablon görüntülerinde mi? | Microsoft Belgeleri"
description: "Azure RemoteApp ile birlikte hello şablon görüntüleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Hello Azure RemoteApp şablon görüntülerinde neler var?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp aboneliğiniz üç şablon görüntüsü içerir:

* Windows Server 2012
* Microsoft Office 365 ProPlus (Office 365 aboneliği gereklidir)
* Microsoft Office 2013 Professional Plus (yalnızca deneme)

> [!IMPORTANT]
> Azure RemoteApp aboneliğiniz, Office 365 ayrı bir abonelik gerektiren ProPlus ve üretimde kullanılamayan Office 2013 hello özel hello görüntülerinde toohello yazılımına erişim verir. Başka bir deyişle, hello program veya hello şablon görüntüleri uygulamaları Kullanıcılarınızla paylaşabilirsiniz. Örneğin, hello Windows Server 2012 R2 görüntüsünü kullanan bir koleksiyon oluşturursanız, kullanıcılar tooaccess RemoteApp aracılığıyla için System Center Endpoint Protection'ı yayımlayabilirsiniz.
> 
> Merhaba denetleyin [RemoteApp lisanslama](remoteapp-licensing.md) daha fazla bilgi için. Ve [Azure RemoteApp ile Office'i kullanma](remoteapp-o365.md) hello Office lisanslama bilgileri için.
> 
> 

Her görüntünün içerdikleri ile ilgili ayrıntılar için okumaya devam edin.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("Merhaba temel alınan görüntü")
Bu görüntü Microsoft Windows Server 2012 R2 Datacenter işletim sistemini temel alır ve hello aşağıdaki rolleri ve özellikleri Azure RemoteApp şablon görüntüleri için toomeet hello gereksinimleri yükledi:

* .NET Framework 4.5, 3.5.1, 3.5
* Masaüstü Deneyimi
* Mürekkep ve El Yazısı Hizmetleri
* Medya Altyapısı
* Uzak Masaüstü Oturumu Konağı
* Windows PowerShell 4.0
* Windows PowerShell ISE
* WoW64 Desteği

Bu görüntü ayrıca yüklenen uygulamalar aşağıdaki hello vardır:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (abonelik gereklidir)
Office 365 olduğu hello en istenen uygulama biz "özel" bir görüntü için toowork ile oluşturduğunuz şekilde.

Bu görüntü hello temel alınan görüntünün bir uzantısıdır ve hello Microsoft Office 365 ProPlus aşağıdaki bileşenlerden ayrıca hello Windows Server 2012 R2 görüntüsünde açıklanan toohello bileşenleri yüklüdür:

* Access
* Excel
* Lync
* OneNote
* OneDrive iş (Azure RemoteApp ile kullanmak için bu hello eşitleme aracı desteklenmez unutmayın)
* Outlook
* PowerPoint
* Word
* Microsoft Office Yazım Denetleme Araçları

Merhaba görüntü ayrıca Visio Pro ve Project Pro'yu da içerir.

Ve hello aşağıdaki uygulamalar da dahildir:

* SQL Native istemcisi
* ODBC Sürücüsü
* SQL Server Data Mining istemcisi
* MasterDataServices istemcisi
* Microsoft Publisher
* PowerQuery
* PowerMap

Office 365 ProPlus uygulamalarının tüm işlevleri yalnızca bir Office 365 ProPlus planı olan kullanıcılar tarafından kullanılabilir. Planları hello Office 365 aboneliği hakkında daha fazla bilgi için bkz: [Office 365 hizmet planları](http://technet.microsoft.com/library/office-365-plan-options.aspx). Hala sorularınız mı var? Merhaba denetleyin [Office 365 + RemoteApp](remoteapp-o365.md) bilgi. Ayrıca hello yeni makalesine göz atın [nasıl toouse Azure RemoteApp ile Office 365 aboneliğinize](remoteapp-officesubscription.md).

Toolicense Office 365 ProPlus, Visio Pro ve Project Pro'yu ayrı olarak gereksinim - her kendi lisanslarına sahip olduğuna dikkat edin.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (yalnızca deneme)
Merhaba ücretsiz deneme süresi boyunca, hello hizmetini hello Office 2013 görüntüsüyle test edebilirsiniz.

Bu görüntü hello temel alınan görüntünün bir uzantısıdır ve hello Microsoft Office 2013 Professional Plus aşağıdaki bileşenlerden ayrıca hello Windows Server 2012 R2 görüntüsünde açıklanan toohello bileşenleri yüklüdür:

* Access
* Excel
* Lync
* OneNote
* OneDrive iş (Azure RemoteApp ile kullanmak için bu hello eşitleme aracı desteklenmez unutmayın)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Microsoft Office Yazım Denetleme Araçları

> [!IMPORTANT]
> **Yasal bilgiler:** Bu görüntü bir Microsoft Office lisansı içermez ve *üretim için kullanılamaz*. Merhaba Office 2013 Professional Plus görüntüsü yalnızca deneme kullanımı için tasarlanmıştır. Üretim için toouse Office uygulamalarını Azure RemoteApp istiyorsanız toouse hello Office 365 ProPlus görüntüsünü gerekir. Office’i lisanslama hakkında daha fazla bilgi için bkz. [Azure RemoteApp ile Office 365’i kullanma](remoteapp-o365.md)
> 
> 

