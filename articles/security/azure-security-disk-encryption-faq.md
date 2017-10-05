---
title: "Azure Disk şifrelemesi ile ilgili SSS | Microsoft Docs"
description: "Bu makale için Microsoft Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler için sık sorulan soruların yanıtlarını sağlar."
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
ms.openlocfilehash: 0d15bf42c156ea7a72c54d690f4016877913efe4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Azure Disk şifrelemesi sık sorulan sorular (SSS)

Bu SSS okuyun, bu hizmet hakkında daha fazla bilgi için Windows ve Linux Iaas VM'ler için Azure disk şifrelemesi hakkında sorular yanıtlanmaktadır [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Genel sorular
**S.** Hangi bölgeyi GA Azure disk şifrelemesi mi?

**Y:** Azure disk şifrelemesi Windows ve Linux Iaas VM'ler için tüm Azure ortak bölgelerde GA de vardır.

**S:** hangi kullanıcı deneyimleri Azure Disk şifrelemesi ile kullanılabilir?

**Y:** Azure Disk şifrelemesi GA Azure Resource Manager şablonlarını, Azure PowerShell, Azure CLI destekler. Disk şifrelemesi, Iaas VM'ler için etkinleştirmek için üç farklı seçeneğiniz vardır, bu size büyük bir esneklik sağlar. Adım adım yönergeler ve kullanıcı deneyimi hakkında daha fazla ayrıntı Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri mevcut değil.

**S:** nasıl Azure Disk şifrelemesi maliyeti?

**Y:** VM diskleri Azure Disk şifrelemesi ile şifrelemek için herhangi bir ücret alınmaz.

**S:** hangi sanal makine katmanları Azure Disk şifrelemesi ile kullanabilir miyim?

**Y:** Azure Disk şifrelemesi yalnızca standart katmanı Vm'leri de dahil olmak üzere üzerinde kullanılabilir [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) vb. serisi Iaas VM'ler ile premium depolama Vm'leri de dahil olmak üzere. Temel katman VM'ler üzerinde kullanılabilir değil.

**S:** ne Linux dağıtımları Azure Disk Şifrelemesi tarafından desteklenir?

**Y:** Azure Disk şifrelemesi aşağıdaki Linux sunucu dağıtımları ve sürümleri desteklenir:

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

**Y:** müşteriler nasıl bulunan Azure Disk şifrelemesi teknik incelemesi okuyarak başlayacağınızı öğrenin [burada](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**S:** Azure Disk şifrelemesi ile hem önyükleme hem de veri birimleri şifreleyebilir mi?

**Y:** Evet, Windows ve Linux Iaas VM'ler için önyükleme ve veri birimlerini şifreleyebilirsiniz. Windows VM'ler için ilk encrpting işletim sistemi birimi olmadan veri şifrelenemiyor. Linux VM'ler için veri birimi encryptinng işletim sistemi birimi olmadan önce şifreleyebilirsiniz. Bir işletim sistemi biriminde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakmak için Linux işletim sistemi birimi şifrelenmiş sonra desteklenmiyor

**S:** mu Azure Disk şifrelemesi etkinleştirmek bir "kendi anahtarını getir" (BYOK) yeteneği?

**Y:** Evet, kendi anahtar şifreleme anahtarları sağlayabilir. Bu anahtarları Azure anahtar Kasası ' Azure Disk şifrelemesi için anahtar deposu olduğu korunur. Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri anahtar şifreleme anahtar destek senaryoları hakkında daha fazla bilgi için bkz:

**S:** oluşturulan Azure anahtar şifreleme anahtarı kullanabilir miyim?

**Y:** Evet, Azure disk şifrelemesi kullanmak için bir anahtar şifreleme anahtarı oluşturmak için Azure anahtar kasası kullanabilirsiniz. Bu anahtarları Azure anahtar Kasası ' Azure Disk şifrelemesi için anahtar deposu olduğu korunur. Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri anahtar şifreleme anahtar destek senaryoları hakkında daha fazla bilgi için bkz:

**S:** şirket içi anahtar yönetimi hizmeti/HSM şifreleme anahtarları korumak için kullanabilir miyim?

**Y:** Azure disk şifrelemesi ile şifreleme anahtarları korumak için şirket içi anahtar yönetimi hizmeti/HSM kullanamazsınız. Azure anahtar kasası hizmetindeki yalnızca şifreleme anahtarları korumak için de kullanabilirsiniz. Azure Disk şifrelemesi dağıtım senaryoları ve deneyimleri anahtar şifreleme anahtar destek senaryoları hakkında daha fazla bilgi için bkz:

**S:** disk şifrelemesi önkoşulları Azure yapılandırmak için nelerdir?

**Y:** yeni anahtar kasası ya da kurulum var olan anahtar kasası, şifreleme ve koruma gizli anahtarları ve anahtar etkinleştirmek disk şifreleme erişimi için AAD uygulaması oluşturmak için Azure disk şifrelemesi önkoşul PowerShell Betiği oluşturun.  Anahtar şifreleme anahtar destek senaryoları hakkında daha fazla bilgi için bkz: Azure Disk şifrelemesi önkoşulları ve dağıtım senaryoları ve deneyimleri

**S:** Azure Disk şifrelemesi yapılandırmak için PowerShell kullanma hakkında daha fazla bilgi nereden alabilirim?

**Y:** nasıl daha Gelişmiş senaryolar yanı sıra temel Azure Disk şifrelemesi görevleri gerçekleştirebilir üzerinde bazı harika makaleleri sunuyoruz. Temel görevlerde Araştır denetleyin [Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Araştır daha Gelişmiş senaryolar için bkz: [Azure PowerShell – bölüm 2 ile Azure Disk şifrelemesi](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**S:** Azure PowerShell hangi sürümünün Azure Disk Şifrelemesi tarafından desteklenir?

**Y:** Azure Disk şifrelemesi yapılandırmak için Azure PowerShell SDK sürümü'nın en son sürümünü kullanın. En son sürümünü indirme [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Azure Disk şifrelemesi Azure SDK sürüm 1.1.0 tarafından desteklenmiyor.

> [!NOTE]
> Linux Azure disk şifrelemesi Önizleme uzantısını kullanım dışıdır. Ayrıntılar için belgelere bakın [burada](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**S:** Azure disk şifrelemesi my özel Linux görüntüye uygulayabilirsiniz?

**Y:** özel Linux görüntünüzü Azure disk şifrelemesi uygulanamıyor. Yukarıdaki çağrılan desteklenen distro'lar için yalnızca galeri Linux görüntüleri destekliyoruz. Şu anda özel Linux görüntüleri desteklemiyoruz

**S:** bir Red Hat Yum güncelleştirme kullanarak Linux VM için güncelleştirmeler uygulayabilir mi?

**Y:** Evet, güncelleştirme gerçekleştirebilir ve veya Red Hat Linnux belgelenen yönergeler aşağıdaki VM düzeltme eki [burada](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**S:** miyim nereye soru sorun ya da geribildirim sağlamak için

**Y:** isteyin sorularınız veya Geri bildiriminiz Azure disk şifrelemesi Forumunda sağlayabilir [burada](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, bu hizmet ve okuma kendi özelliği hakkında daha fazla bilgi için Azure disk şifrelemesi ile ilgili en sık kullanılan sorular hakkında daha fazla öğrendiniz:

- [Azure Güvenlik Merkezi'nde disk şifrelemesi Uygula](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Azure sanal Makine'yi şifreleme](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure veri şifreleme çalışmıyorken-](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
