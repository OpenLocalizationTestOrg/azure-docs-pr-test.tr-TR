---
title: "Adlı kimlik doğrulama kimlik bilgilerini ayarlama | Microsoft Docs"
description: "İçin kimlik bilgilerini sağlamak için Visual Studio Azure uygulamaya Visual Studio'dan yayımlamak için veya var olan bir bulut hizmetini izlemek için istekleri Azure kimlik doğrulaması için nasıl kullanabileceğinizi öğrenin... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Adlandırılmış kimlik doğrulama kimlik bilgilerini ayarlama
Azure uygulama Visual Studio'dan yayımlamak ya da var olan bir bulut hizmetini izlemek için Visual Studio Azure isteklerine kimliğini doğrulamak için kullanabileceğiniz kimlik bilgilerini sağlamanız gerekir. Visual Studio'da burada bu kimlik bilgilerini sağlamak üzere oturum içinde çeşitli yerlerde vardır. Örneğin, Sunucu Gezgini'nden için kısayol menüsünü açarak **Azure** düğümü seçin **Microsoft Azure aboneliğine Bağlan...** . Oturum açtığınızda Visual Studio'da Azure hesabınızla ilişkili abonelik bilgilerini kullanılabilir ve yapmanız gereken başka bir şey yok.

Azure araçlarını da destekler kimlik bilgileri, sağlama daha eski bir yol abonelik dosyasını (.publishsettings) kullanarak. Bu konu Azure SDK 2.2 hala desteklenmektedir bu yöntem açıklar.

Aşağıdaki öğeler, Azure için kimlik doğrulaması için gereklidir:

* Abonelik kimliği
* Geçerli bir X.509 v3 sertifikası

> [!NOTE]
> X.509 v3 sertifikası'nın anahtar uzunluğu en az 2048 bit olmalıdır. Azure, bu gereksinimi karşılamıyor veya geçerli olmayan herhangi bir sertifikayı reddeder.
>
>

Visual Studio abonelik Kimliğinizi sertifika verileri ile birlikte kimlik bilgileri olarak kullanır. Uygun kimlik bilgilerini içeren bir ortak anahtar sertifikası için abonelik dosyasında (.publishsettings dosyasını) başvurulur. Abonelik dosyası birden fazla aboneliğiniz için kimlik bilgileri içerebilir.

Abonelik bilgileri düzenleyebilirsiniz **yeni/Düzenle abonelik** iletişim kutusunda, bu konunun ilerleyen bölümlerinde açıklandığı gibi.

Bir sertifika kendiniz oluşturmak istiyorsanız,'ndaki yönergeleri başvurabilirsiniz [oluşturun ve Azure için yönetim sertifikası karşıya](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) ve sertifikayı el ile karşıya [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Bulut hizmetleri yönetmek için Visual Studio gerektirir bu kimlik bilgileri isteği Azure storage hizmetlerine karşı kimlik doğrulaması için gerekli kimlik bilgilerini değil.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>İçeri aktarma, ayarlama veya Visual Studio'da kimlik doğrulama bilgilerini Düzenle
İçeri aktarma, ayarlama veya kimlik doğrulama kimlik bilgilerinizi değiştirmek **yeni abonelik** iletişim kutusunda, şu işlemi gerçekleştirirseniz, görünür:

* İçinde **Sunucu Gezgini**, kısayol menüsünü açın **Azure** düğümü seçin **yönetin ve filtre abonelikleri...** , seçin **sertifikaları** sekmesini tıklatın ve aşağıdakilerden birini yapın:

    * Seçin **alma** burada indirebilirsiniz abonelikleri dosyanın şu anda yüklenen abonelik için Microsoft Azure abonelikleri alma iletişim kutusunu açmak için indirme konumuna göz atın ve kullanmak için alma kimlik doğrulaması.
    * Seçin **yeni** burada ayarlayabilirsiniz kimlik doğrulaması kullanmak için yeni bir abonelik Yeni Abonelik iletişim kutusunu açın.
    * Seçin **Düzenle** (sonra etkin aboneliğinizi seçme) burada düzenleyebilirsiniz kimlik doğrulaması kullanmak için mevcut bir aboneliğe abonelik Düzenle iletişim kutusunu açın. 

Aşağıdaki yordam varsayar **yeni abonelik** iletişim kutusunu açın.

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a>Visual Studio'da kimlik doğrulama kimlik bilgilerini ayarlamak için
1. İçinde **varolan bir sertifikayı seçin** kimlik doğrulama listesi için bir sertifika seçin.
2. Seçin **tam yolunu kopyalamak** bağlantı. Sertifika (.cer dosyası) yolunu Panoya kopyalandı.

   > [!IMPORTANT]
   > Azure uygulamanızı Visual Studio'dan yayımlamak için bu sertifikayı karşıya [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. Azure portalına sertifikayı karşıya yüklemek için:

   1. [Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=525040) açın.
   2. İstenirse, portalında oturum açın ve ardından gidin **ayarları**, **yönetim sertifikaları**.
   3. Yönetim sertifikaları bölmesinde seçin **karşıya**.
   4. Azure aboneliğinizi seçin, oluşturulan yeni .cer dosyasının tam yolunu yapıştırın ve **karşıya**.
