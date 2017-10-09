---
title: "Azure Güvenlik Merkezi'nde aaaApply disk şifrelemesi | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** disk şifreleme ** uygulayın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde disk şifrelemesi Uygula
Azure Güvenlik Merkezi, Azure Disk şifrelemesi kullanılarak şifrelenmiş değil Windows veya Linux VM diskiniz varsa, disk şifrelemesi uygulamanızı önerir. Disk şifrelemesi, Windows ve Linux Iaas VM diskleri şifrelemek olanak tanır.  Şifreleme hello işletim sistemi ve veri birimlerine, VM için önerilir.

Disk şifrelemesi kullanır hello endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) özelliği Windows hello ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux özelliğidir. Bu özellikler OS sağlar ve veri şifreleme toohelp korumak ve verilerinizi korumak ve Kuruluş güvenliği ve uyumluluk taahhüt karşılamak. Disk şifrelemesi ile tümleştirildiğinde [Azure anahtar kasası](https://azure.microsoft.com/documentation/services/key-vault/) toohelp, denetlemek ve, bekleyenhelloVMdisklerdekitümverilerşifrelenirsağlarkenanahtarkasasıaboneliğinizdehellodiskşifrelemeanahtarlarıvegizlianahtarlarıYönet[ Azure depolama](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Azure Disk şifrelemesi, Windows sunucu işletim sistemi - Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 aşağıdaki hello üzerinde desteklenir. Disk şifrelemesi, Linux ve sunucu işletim sistemleri - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) aşağıdaki hello üzerinde desteklenir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **disk şifrelemesi uygulamak**.
2. Merhaba, **disk şifrelemesi uygulamak** dikey penceresinde, Disk şifrelemesi önerilir VM'ler listesini görürsünüz.
3. Merhaba yönergeleri tooapply şifreleme toothese VM'ler izleyin.

![][1]

Güvenlik Merkezi tarafından şifreleme gerektiği belirlenen Azure Virtual Machines tooencrypt hello aşağıdaki adımları öneririz:

* Azure PowerShell'i yükleyip yapılandırın. Bu, toorun hello PowerShell komutları gerekli tooset hello önkoşullar gerekli tooencrypt Azure sanal makineleri yedeklemek sağlar.
* Edinin ve hello Azure Disk şifrelemesi önkoşulları Azure PowerShell betiğini çalıştırın.
* Sanal makinelerinizi şifreleyin.

[Bir Azure sanal Makine'yi şifreleme](security-center-disk-encryption.md) Bu adımlarda size yol gösterir.  Bu konu, disk şifrelemesi'ni yapılandırma hello istemci makine gibi Windows 10 kullandığınızı varsayar.

Azure sanal makineler için kullanılabilir birçok yaklaşım vardır. Zaten Azure PowerShell veya Azure CLI bilgiliyseniz, toouse alternatif yaklaşımlar tercih edebilirsiniz. Bu diğer yaklaşımlar hakkında toolearn bkz [Azure disk şifrelemesi](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Ayrıca bkz.
Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "Uygula disk şifrelemesi." gösterdi. disk şifrelemesi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure anahtar kasası ile şifreleme ve anahtar yönetimi](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sn)--nasıl toouse disk şifreleme yönetim Iaas Vm'leri ve Azure anahtar kasası toohelp korumak ve verilerinizi korumak için öğrenin.
* [Bir Azure sanal Makine'yi şifreleme](security-center-disk-encryption.md) (belge)--öğrenin nasıl tooencrypt Azure sanal makineler.
* [Azure disk şifrelemesi](../security/azure-security-disk-encryption.md) (belge)--nasıl tooenable disk şifrelemesi Windows ve Linux VM'ler için öğrenin.

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
