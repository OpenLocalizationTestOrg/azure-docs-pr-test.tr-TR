---
title: "aaaProtecting Azure SQL Hizmeti ve verileri Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge adresleri yardımcı olacak öneriler Azure Güvenlik Merkezi'nde veri ve Azure SQL Hizmeti korumak ve güvenlik ilkeleriyle uyumlu olmak."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Azure SQL Hizmeti ve Azure Güvenlik Merkezi'nde veri koruma
Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.  Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve veri ve uygulamaları makineleri (VM'ler).

Bu makalede tooAzure SQL Hizmeti ve verileri uygulamak önerileri giderir. Azure SQL sunucuları ve SQL veritabanları için şifreleme ve Azure depolama hesabınızın etkinleştirme şifreleme etkinleştirme veritabanları için denetimi etkinleştirme geçici önerileri Merkezi.  Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir SQL Hizmeti ve verileri önerileri ve onu uygularsanız her birini ne yaptığını anlayın.

## <a name="available-sql-service-and-data-recommendations"></a>Kullanılabilir SQL Hizmeti ve verileri önerileri
| Öneri | Açıklama |
| --- | --- |
| [SQL sunucularında denetim ve tehdit algılamayı etkinleştirme](security-center-enable-auditing-on-sql-servers.md) |Denetim ve tehdit algılama için (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL sunucuları Aç önerir. |
| [SQL veritabanlarında denetim ve tehdit algılamayı etkinleştirme](security-center-enable-auditing-on-sql-databases.md) |Denetim ve tehdit algılama (sanal makinelerde çalışan SQL Azure SQL Hizmeti yalnızca; içermeyen) Azure SQL veritabanları için Aç önerir. |
| [SQL veritabanlarını saydam veri şifreleme etkinleştir](security-center-enable-transparent-data-encryption.md) |SQL veritabanları (yalnızca Azure SQL Hizmeti) için şifrelemeyi etkinleştirmek önerir. |

## <a name="see-also"></a>Ayrıca bkz.
toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:

* [Azure Güvenlik Merkezi'nde, sanal makineleri koruma](security-center-virtual-machine-recommendations.md)
* [Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma](security-center-application-recommendations.md)
* [Azure Güvenlik Merkezi, ağınızda koruma](security-center-network-recommendations.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
