---
title: "Azure anahtar kasası aaaWhat mi? | Microsoft Belgeleri"
description: "Azure Anahtar Kasası, bulut uygulamaları ve hizmetleri tarafından kullanılan şifreleme anahtarlarının ve gizli anahtarların korunmasına yardımcı olur. Azure Anahtar Kasası'nı kullanarak müşteriler, anahtarları ve gizli anahtarları (kimlik doğrulaması anahtarları, depolama hesabı anahtarları, veri şifreleme anahtarları, .PFX dosyaları ve parolalar gibi), donanım güvenlik modülleri tarafından korunan anahtarları kullanarak şifreleyebilir."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Azure Anahtar Kasası nedir?
Azure Anahtar Kasası çoğu bölgede kullanılabilir. Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Giriş
Azure Anahtar Kasası, bulut uygulamaları ve hizmetleri tarafından kullanılan şifreleme anahtarlarının ve gizli anahtarların korunmasına yardımcı olur. Anahtar Kasası'nı kullanarak anahtarları ve gizli anahtarları (kimlik doğrulaması anahtarları, depolama hesabı anahtarları, veri şifreleme anahtarları, .PFX dosyaları ve parolalar gibi), donanım güvenlik modülleri tarafından korunan anahtarları kullanarak şifreleyebilirsiniz. Ek güvenlik için HSM'lerde anahtarları içeri aktarabilir veya oluşturabilirsiniz. Bu, Microsoft işlemleri toodo seçerseniz anahtarlarınızı FIPS 140-2, 2 doğrulanmış HSM'ler (donanım ve bellenim) düzeyi.  

Anahtar kasası hello anahtar yönetimi işlemini kolaylaştırır ve erişmek ve veri şifreleme anahtarları toomaintain denetimini etkinleştirir. Geliştiriciler, geliştirme ve test dakika cinsinden tuşları oluşturabilir ve ardından bunları tooproduction anahtarları sorunsuz geçiş. Güvenlik yöneticileri verin (iptal gerektiğinde izni tookeys ve).

Tablo toobetter aşağıdaki kullanım hello anlamak anahtar kasası geliştiricilere ve güvenlik yöneticilerine toomeet hello gereksinimlerini nasıl yardımcı olabilir.

| Rol | Sorun bildirimi | Azure Anahtar Kasası tarafından çözüldü |
| --- | --- | --- |
| Bir Azure uygulaması geliştiricisi |"İmzalama ve şifreleme için anahtarları kullanan Azure toowrite uygulamanın istiyorum, ancak hello çözüm coğrafi olarak dağıtılmış bir uygulama için uygun olmasını sağlamak Bu anahtarları toobe dış my uygulamadan istiyorum. <br/><br/>Ayrıca korumalı, toowrite hello kod kendim gerek kalmadan bu anahtarları ve gizli anahtarları toobe istiyorum. Ayrıca bu anahtarları ve gizli anahtarları toobe kolay benim için toouse en iyi performansla Uygulamam uygulamalardan istiyorum." |√ Anahtarlar bir kasada depolanır ve gerektiğinde URI tarafından çağrılır.<br/><br/> √ Anahtarlar, endüstri standardında algoritmalar, anahtar uzunlukları ve donanım güvenliği modülleri (HSM'ler) kullanılarak Azure tarafından korunur.<br/><br/> √ Anahtarlar aynı hello bulunan HSM'ler içinde işlenir hello uygulamalar olarak Azure veri merkezleri. Bu, daha iyi güvenilirlik ve hello anahtarları şirket içi gibi ayrı bir konumda bulunan, daha düşük gecikme sağlar. |
| Hizmet olarak Yazılım (SaaS) geliştiricisi |"Hello sorumluluk veya olası yükümlülük my Kiracı anahtarları ve gizli anahtarları için istemiyorum. <br/><br/>I hello müşteriler tooown istediğiniz ve böylece en iyi şekilde, hangi hello çekirdek yazılım özelliklerini sağlamaya ne yapabilirim yapmayı yoğunlaşabilirsiniz kendi anahtarları Yönet." |√ Müşteriler kendi anahtarları Azure'a aktarabilir ve bunları yönetebilir. SaaS uygulamasının müşterilerin anahtarlarını kullanarak tooperform şifreleme işlemleri gerektiğinde, anahtar kasası hello uygulama adına bu işlemleri yapar. Merhaba uygulaması hello müşterilerin anahtarlarını görmez. |
| Güvenlik başkanı (CSO) |"Güvenli anahtar yönetimi için FIPS 140-2 Düzey 2 HSM'ler bizim uygulamaları uyması tooknow istiyorum. <br/><br/>I toomake Kuruluşum hello anahtar yaşam döngüsü denetiminde olmasını istediğiniz ve anahtar kullanımını izleyebilirsiniz. <br/><br/>Ve biz birden çok Azure hizmeti ve kaynağı kullanıyor olsa da, toomanage hello anahtarları azure'da tek bir konumdan istiyor." |√ HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına sahiptir.<br/><br/>√ Anahtar Kasası, Microsoft anahtarlarınızı görmeyecek ve ayıklamayacak şekilde tasarlanmıştır.<br/><br/>√ Gerçek zamanlıya yakın anahtar kullanımı günlüğü.<br/><br/>√ hello kasası, destek ve hangi uygulamaların bunları kullandığına kaç kasanız sahip olduğunuz Azure, hangi bölgelerin bunlar bağımsız olarak tek bir arabirim sağlar. |

Bir Azure aboneliği olan herhangi biri, anahtar kasalarını oluşturabilir ve kullanabilir. Anahtar Kasası geliştiricilere ve güvenlik yöneticilerine avantaj sağlasa da, bir kuruluş için diğer Azure hizmetlerini yöneten bir kuruluş yöneticisi tarafından uygulanabilir ve yönetilebilir. Örneğin, bu yönetici Azure abonelikle oturum açmak, hangi toostore anahtarlarında hello kuruluş için bir kasa oluşturun ve ardından gibi işlemsel görevlerden sorumlu:

* Bir anahtar veya gizli anahtarı oluşturma veya içeri aktarma
* Bir anahtar veya gizli anahtarı iptal etme veya silme
* Kullanıcılar veya uygulamalar tooaccess hello anahtar kasası, bunlar daha sonra yönetmek veya ve gizli anahtarları kullanmak için yetkilendirme
* Anahtar kullanımını (örneğin, imzalama veya şifreleme) yapılandırma
* Anahtar kullanımını izleme

Bu yönetici ardından geliştiricilere URI'ler toocall kendi uygulamalardan sağlamak ve güvenlik yöneticisine anahtar kullanımı günlüğü bilgilerini sunar. 

   ![Azure Anahtar Kasası'na Genel Bakış][1]

Geliştiriciler ayrıca hello anahtarları doğrudan API'lerini kullanarak yönetebilirsiniz. Daha fazla bilgi için bkz: [anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).

## <a name="next-steps"></a>Sonraki Adımlar
Bir yöneticiye yönelik başlama öğreticisi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md).

Anahtar Kasası'na yönelik kullanım günlüğü hakkında daha fazla bilgi için bkz. [Azure Anahtar Kasası Günlüğü](key-vault-logging.md).

Azure Anahtar Kasası ile anahtarları ve gizli anahtarları kullanma hakkında daha fazla bilgi için bkz. [Anahtarlar, Parolalar ve Sertifikalar Hakkında](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
