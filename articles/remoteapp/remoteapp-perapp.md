---
title: "aaaPublish uygulamaları tooindividual kullanıcıların bir Azure RemoteApp koleksiyonunda (Önizleme) | Microsoft Docs"
description: "Nasıl uygulamaları tooindividual kullanıcılar yerine gruplar, Azure RemoteApp bağlı olarak yayımlayabilirsiniz öğrenin."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Bir Azure RemoteApp koleksiyonunda (Önizleme) uygulamaları tooindividual kullanıcılar yayımlama
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bu makalede açıklanır nasıl toopublish uygulamaları tooindividual kullanıcıların bir Azure RemoteApp koleksiyonu. Azure RemoteApp, şu anda özel Önizleme ve kullanılabilir yalnızca tooselect erken Benimseyenler Değerlendirme amacıyla yeni işlevsellik budur.

Başlangıçta Azure RemoteApp uygulama yayımlama için yalnızca tek yönlü etkin: Merhaba yönetici hello görüntüden uygulamaları yayımlamak ve hello koleksiyonunda görünür tooall kullanıcılar olacaktır.

Birçok uygulama tek bir görüntü ve sipariş tooreduce yönetim maliyetlerini bir koleksiyona dağıtmak tooinclude buna ortak bir senaryodur. İlgili tooall kullanıcı görmemeleri tüm uygulamalardır – yöneticiler kendi uygulama Gereksiz uygulamaları görmek istemediğiniz toopublish uygulamaları tooindividual kullanıcılar tercih.

Bu artık Azure RemoteApp’te şu anda sınırlı bir önizleme özelliği olarak mümkündür. Merhaba yeni işlevsellik kısa bir özeti aşağıda verilmiştir:

1. Bir koleksiyon iki moddan birini ayarlanabilir:
   
   * bir koleksiyondaki tüm kullanıcıların görebileceğiniz hello özgün koleksiyon modu, yayımlanan tüm uygulamaları. Merhaba varsayılan mod budur.
   * Burada kullanıcılar açıkça toothem atanan uygulamalar yalnızca bkz hello yeni uygulama modu
2. Merhaba şu anda Azure RemoteApp PowerShell cmdlet'lerini kullanarak hello uygulama modu yalnızca etkinleştirilebilir.
   
   * Ne zaman tooapplication modunu ayarlama, kullanıcı ataması hello koleksiyonundaki hello Azure portal yönetilemez. Kullanıcı Ataması PowerShell cmdlet'leri aracılığıyla yönetilen toobe sahiptir.
3. Kullanıcılar yalnızca görürsünüz hello yayımlanan uygulamaları doğrudan toothem. Kullanıcı toolaunch hello için hello görüntüde bulunan diğer uygulamaları doğrudan hello işletim sisteminde erişerek ancak bunu hala mümkün olabilir.
   
   * Bu özellik uygulamalara güvenli bir kilitleme sağlamaz; yalnızca, akış Merhaba uygulaması görünürlüğü sınırlar.
   * Uygulamaları kullanıcılardan tooisolate gerekiyorsa, toouse ayrı koleksiyonlar için gerekir.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Nasıl tooget Azure RemoteApp PowerShell cmdlet'leri
tootry hello yeni önizleme işlevini, toouse Azure PowerShell cmdlet'lerini gerekir. Şu anda olası toouse hello Azure Management portal tooenable hello yeni uygulama yayımlama modunu olmadığı.

Öncelikle, hello sahip olduğunuzdan emin olun [Azure PowerShell Modülü](/powershell/azure/overview) yüklü.

Ardından Yönetici modunda ve aşağıdaki cmdlet'i çalıştırın hello hello PowerShell konsolunu başlatın:

        Add-AzureAccount

Sizden Azure kullanıcı adı ve parola bilgilerini ister. Oturum açtıktan sonra Azure aboneliklerinize karşı mümkün toorun Azure RemoteApp cmdlet'lerini olacaktır.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Nasıl bir koleksiyon hangi modun konusu toocheck
Hello aşağıdaki cmdlet'i çalıştırın:

        Get-AzureRemoteAppCollection <collectionName>

![Merhaba koleksiyonu modunu kontrol etme](./media/remoteapp-perapp/araacllelvel.png)

Merhaba AclLevel özelliği aşağıdaki değerleri hello sahip olabilir:

* Koleksiyonu: hello özgün yayımlama modu. Tüm kullanıcılar yayımlanan bütün uygulamaları görür.
* Uygulama: hello yeni yayımlama modu. Kullanıcılar yalnızca hello uygulamaları doğrudan toothem yayımlanan bakın.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Nasıl tooswitch tooapplication yayımlama modu
Hello aşağıdaki cmdlet'i çalıştırın:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Uygulama yayımlama durumu muhafaza edilir: Başlangıçta tüm kullanıcılar tüm hello özgün yayımlanan bütün uygulamaları görür.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Nasıl belirli bir uygulamayı görebilen toolist kullanıcıları
Hello aşağıdaki cmdlet'i çalıştırın:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Bu hello uygulamayı görebilen tüm kullanıcıları listeler.

Not: Get-AzureRemoteAppProgram - CollectionName çalıştırarak hello uygulama diğer adlarını (yukarıdaki hello söz diziminde "app alias" olarak adlandırılır) görebilirsiniz <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Nasıl tooassign uygulama tooa kullanıcısı
Hello aşağıdaki cmdlet'i çalıştırın:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

Merhaba kullanıcı artık Merhaba uygulaması hello Azure RemoteApp istemcisinde görür ve mümkün tooconnect tooit olacaktır.

## <a name="how-tooremove-an-application-from-a-user"></a>Nasıl tooremove bir kullanıcı bir uygulamadan
Hello aşağıdaki cmdlet'i çalıştırın:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Geribildirim sağlama
Bu önizleme özelliğiyle ilgili teşekkür ver önerileriniz için teşekkür ederiz. Lütfen hello doldurun [anket](http://www.instant.ly/s/FDdrb) Bize düşüncelerinizi toolet.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Bir fırsat tootry hello önizleme özelliği henüz oldu?
Hello henüz önizlemeye değil, lütfen bu kullanırsanız [anket](http://www.instant.ly/s/AY83p) toorequest erişim.

