---
title: "aaaAzure Disk şifreleme SSS | Microsoft Docs"
description: "Bu makalede yanıtlar sağlayan sorular ilgili daha fazla bilgi için Microsoft Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler toofrequently."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Azure Disk şifrelemesi sık sorulan sorular (SSS)

Bu SSS okuyun, bu hizmet hakkında daha fazla bilgi için Windows ve Linux Iaas VM'ler için Azure disk şifrelemesi hakkında sorular yanıtlanmaktadır [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Genel sorular
**S.** Hangi bölgeyi GA Azure disk şifrelemesi mi?

**Y:** Azure disk şifrelemesi Windows ve Linux Iaas VM'ler için tüm Azure ortak bölgelerde GA de vardır.

**S:** hangi kullanıcı deneyimleri Azure Disk şifrelemesi ile kullanılabilir?

**Y:** Azure Disk şifrelemesi GA Azure Resource Manager şablonlarını, Azure PowerShell, Azure CLI destekler. Disk şifrelemesi, Iaas VM'ler için etkinleştirmek için üç farklı seçeneğiniz vardır, bu size büyük bir esneklik sağlar. Merhaba kullanıcı deneyimi ve adım adım yönergeleri hakkında daha fazla ayrıntı hello Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri mevcut değil.

**S:** nasıl Azure Disk şifrelemesi maliyeti?

**Y:** VM diskleri Azure Disk şifrelemesi ile şifrelemek için herhangi bir ücret alınmaz.

**S:** hangi sanal makine katmanları Azure Disk şifrelemesi ile kullanabilir miyim?

**Y:** Azure Disk şifrelemesi yalnızca standart katmanı Vm'leri de dahil olmak üzere üzerinde kullanılabilir [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) vb. serisi Iaas VM'ler ile premium depolama Vm'leri de dahil olmak üzere. Temel katman VM'ler üzerinde kullanılabilir değil.

**S:** ne Linux dağıtımları Azure Disk Şifrelemesi tarafından desteklenir?

**Y:** Azure Disk şifrelemesi Linux sunucu dağıtımları ve sürümleri aşağıdaki hello üzerinde desteklenir:

| Linux dağıtım | Sürüm | Şifreleme için desteklenen birim türü|
| --- | --- |--- |
| Ubuntu | 16.04 GÜNLÜK LTS | İşletim sistemi ve veri diski |
| Ubuntu | 14.04.5-DAILY-LTS | İşletim sistemi ve veri diski |
| RHEL | 7.3 | İşletim sistemi ve veri diski |
| RHEL | 7.2 | İşletim sistemi ve veri diski |
| RHEL | 6.8 | İşletim sistemi ve veri diski |
| RHEL | 6.7 | Veri diski |
| CentOS | 7.3 | İşletim sistemi ve veri diski |
| CentOS | 7.2n | İşletim sistemi ve veri diski |
| CentOS | 6.8 | İşletim sistemi ve veri diski |
| CentOS | 7.1 | Veri diski |
| CentOS | 7.0 | Veri diski |
| CentOS | 6.7 | Veri diski |
| CentOS | 6.6 | Veri diski |
| CentOS | 6.5 | Veri diski |
| openSUSE | 13.2 | Veri diski |
| SLES | 12 SP1 | Veri diski |
| SLES | Öncelik: 12-SP1 | Veri diski |
| SLES | HPC 12 | Veri diski |
| SLES | Öncelik: 11-SP4 | Veri diski |
| SLES | 11 SP4 | Veri diski |

**S:** çalışmaya nasıl Azure Disk Şifrelemesi'ni kullanarak?

**Y:** müşteriler tooget okuma hello tarafından bulunan Azure Disk şifrelemesi teknik incelemesi nasıl başlatılacağını bulabilir [burada](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**S:** Azure Disk şifrelemesi ile hem önyükleme hem de veri birimleri şifreleyebilir mi?

**Y:** Evet, Windows ve Linux Iaas VM'ler için önyükleme ve veri birimlerini şifreleyebilirsiniz. Windows VM'ler için ilk encrpting hello işletim sistemi birimi olmadan hello veriler şifrelenemedi. Linux VM'ler için hello veri birimi encryptinng hello işletim sistemi birimi olmadan önce şifreleyebilirsiniz. Linux için hello işletim sistemi birimi şifrelenmiş sonra bir işletim sistemi biriminde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakmak desteklenmiyor

**S:** mu Azure Disk şifrelemesi etkinleştirmek bir "kendi anahtarını getir" (BYOK) yeteneği?

**Y:** Evet, kendi anahtar şifreleme anahtarları sağlayabilir. Bu anahtarları Azure anahtar Kasası ' Azure Disk şifrelemesi için anahtar deposu hello olduğu korunur. Hello anahtar şifreleme anahtarı hakkında daha fazla ayrıntı için senaryoları desteklemek, hello Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri bakın

**S:** oluşturulan Azure anahtar şifreleme anahtarı kullanabilir miyim?

**Y:** Evet, Azure disk şifrelemesi kullanım için Azure anahtar kasası toogenerate anahtar şifreleme anahtarı kullanabilirsiniz. Bu anahtarları Azure anahtar Kasası ' Azure Disk şifrelemesi için anahtar deposu hello olduğu korunur. Hello anahtar şifreleme anahtarı hakkında daha fazla ayrıntı için senaryoları desteklemek, hello Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri bakın

**S:** şirket içi anahtar yönetimi hizmeti/HSM toosafeguard hello şifreleme anahtarlarını kullanabilir miyim?

**Y:** Azure disk şifrelemesi ile Merhaba şirket içi anahtar yönetimi hizmeti/HSM toosafeguard hello şifreleme anahtarları kullanamazsınız. Yalnızca hello Azure anahtar kasası hizmeti toosafeguard hello şifreleme anahtarları kullanabilirsiniz. Hello anahtar şifreleme anahtarı hakkında daha fazla ayrıntı için senaryoları desteklemek, hello Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri bakın

**S:** hello Önkoşullar tooconfigure Azure disk şifrelemesi nelerdir?

**Y:** Azure disk şifrelemesi önkoşul PowerShell betik toocreate AAD uygulama Merhaba, yeni anahtar kasası oluşturma veya varolan anahtar kasası disk şifreleme erişim tooenable şifreleme ve koruma gizli anahtarları ve anahtar için Kurulum.  Hello anahtar şifreleme anahtarı hakkında daha fazla ayrıntı için senaryoları desteklemek, bkz: hello Azure Disk şifrelemesi önkoşulları ve dağıtım senaryoları ve deneyimleri

**S:** hakkında daha fazla bilgi nereden alabilirim Azure Disk şifrelemesi yapılandırmak için PowerShell toouse?

**Y:** nasıl daha Gelişmiş senaryolar yanı sıra temel Azure Disk şifrelemesi görevleri gerçekleştirebilir üzerinde bazı harika makaleleri sunuyoruz. Araştır Hello temel görevleri denetleyin [Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Araştır daha Gelişmiş senaryolar için bkz: [Azure PowerShell – bölüm 2 ile Azure Disk şifrelemesi](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**S:** Azure PowerShell hangi sürümünün Azure Disk Şifrelemesi tarafından desteklenir?

**Y:** hello en son sürümünü kullanın Azure PowerShell SDK sürüm tooconfigure Azure Disk şifrelemesi. Merhaba en son sürümünü indirme [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Azure Disk şifrelemesi Azure SDK sürüm 1.1.0 tarafından desteklenmiyor.

> [!NOTE]
> Merhaba Linux Azure disk şifrelemesi Önizleme uzantısını kullanım dışıdır. Ayrıntılar için toodocumentation başvurun [burada](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**S:** Azure disk şifrelemesi my özel Linux görüntüye uygulayabilirsiniz?

**Y:** özel Linux görüntünüzü Azure disk şifrelemesi uygulanamıyor. Yukarıdaki çağrılan hello desteklenen distro'lar için yalnızca hello galeri Linux görüntüleri destekliyoruz. Şu anda özel Linux görüntüleri desteklemiyoruz

**S:** güncelleştirmeleri tooa Linux Red Hat VM uygulayabilmeniz için Yum update kullanarak?

**Y:** Evet, güncelleştirme gerçekleştirebilir ve veya Red Hat Linnux belgelenen yönergeler aşağıdaki VM düzeltme eki [burada](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**S:** burada miyim Git tooask soru veya geri bildirim sağlayın

**Y:** isteyin sorularınız veya Geri bildiriminiz hello Azure disk şifrelemesi Forumunda sağlayabilir [burada](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, daha hello en sık kullanılan sorular ilgili tooAzure disk şifrelemesi, bu hizmet ve okuma kendi özelliği hakkında daha fazla bilgi için ilgili öğrenilen:

- [Azure Güvenlik Merkezi'nde disk şifrelemesi Uygula](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Azure sanal Makine'yi şifreleme](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure veri şifreleme çalışmıyorken-](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
