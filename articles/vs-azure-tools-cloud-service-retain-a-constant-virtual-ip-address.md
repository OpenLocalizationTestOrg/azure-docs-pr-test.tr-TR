---
title: "aaaHow tooretain bir Azure bulut hizmeti için sabit bir sanal IP adresi | Microsoft Docs"
description: "Sanal IP adresi (VIP) Azure bulut hizmetinizin hello tooensure nasıl değiştirmez öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Bir Azure bulut hizmeti için sabit bir sanal IP adresi koru
Azure üzerinde barındırılan bir bulut hizmeti güncelleştirdiğinizde, hello sanal hello hizmetinin IP adresi (VIP) değişmez tooensure gerekebilir. Birçok etki alanı Yönetim Hizmetleri hello etki alanı adı sistemi (DNS) etki alanı adları kaydetmek için kullanın. Merhaba VIP kalır aynı hello DNS çalışır. Merhaba kullanabilirsiniz **Yayımlama Sihirbazı** bulut hizmetinizin VIP ne zaman değiştirmez hello Azure Araçları tooensure içinde güncelleştirmeniz. Hakkında daha fazla bilgi için bkz: toouse DNS etki alanı yönetimi, bulut Hizmetleri için [bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Bir bulut hizmeti, VIP değiştirmeden yayımlama
ilk tooAzure hello üretim ortamı gibi belirli bir ortamda dağıtmak hello VIP bir bulut hizmeti ayrılır. yalnızca hello dağıtımı açıkça silin veya hello dağıtım örtük olarak hello dağıtım tarafından silinmesi durumunda hello VIP değişiklikleri işlem güncelleştirin. tooretain hello VIP dağıtımınızı silmemelisiniz ve Visual Studio, dağıtımınızı otomatik olarak silmez emin olmanız gerekir. 

Dağıtım ayarları hello belirtebilirsiniz **Yayımlama Sihirbazı**, çeşitli dağıtım seçenekleri destekler. Yeni bir dağıtımını veya artımlı veya eşzamanlı olabilir bir güncelleştirme dağıtımı belirtebilirsiniz. Her iki tür güncelleştirme dağıtımı hello VIP korur. Bu farklı dağıtım türleri tanımları için bkz: [Azure uygulaması Yayımlama Sihirbazı](vs-azure-tools-publish-azure-application-wizard.md). Ayrıca, bir hata oluşursa hello önceki bir bulut hizmeti dağıtımının silinip silinmediğini kontrol edebilirsiniz. Bu seçenek doğru şekilde ayarlamazsanız hello VIP beklenmedik bir şekilde değiştirebilirsiniz.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Güncelleştirme, VIP değiştirmeden bir bulut hizmeti
1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın. 

2. İçinde **Çözüm Gezgini**, sağ hello projesi. Merhaba kısayol menüsünden seçin **Yayımla**.

    ![Yayımla menüsü](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. Merhaba, **Azure uygulamasını Yayımla** iletişim kutusu, select hello Azure aboneliği toowhich toodeploy istiyor. Gerekli ve select oturum **sonraki**.

    ![Azure uygulama oturum aç sayfasında yayımlama](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Merhaba üzerinde **ortak ayarları** sekmesinde, bu hello bulut hizmeti toowhich dağıtım, hello hello adını doğrulayın **ortam**, hello **yapı yapılandırması**ve hello **Hizmet yapılandırmasını** doğru olduğunu.

    ![Azure uygulama ortak ayarlar sekmesinde yayımlama](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Hello üzerinde **Gelişmiş ayarları** sekmesinde, bu hello doğrulayın **dağıtım etiketi** ve hello **depolama hesabı** doğrudur. Bu hello doğrulayın **hata durumunda dağıtımı Sil** onay kutusu işaretli değildir ve bu hello doğrulayın **dağıtım güncelleştirme** onay kutusu seçilidir. Temizleme hello tarafından **hata durumunda dağıtımı Sil** onay kutusunu olun dağıtımı sırasında bir hata meydana gelirse, VIP kayıp değil. Merhaba seçerek **dağıtım güncelleştirme** onay kutusu, dağıtımınızı silinmez ve uygulamanızı yayımladığınızda, VIP kaybı olmadığından emin olun. 

    ![Azure uygulama Gelişmiş Ayarlar sekmesi yayımlama](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther güncelleştirilmiş hello rolleri toobe nasıl ilişkilendireceğini belirleyin, seçin **ayarları** sonraki çok**dağıtım güncelleştirme**. Şunlardan birini seçin **Artımlı güncelleştirme** veya **eşzamanlı güncelleştirme**seçip **Tamam**. Seçin **Artımlı güncelleştirme** tooupdate, uygulamanızın her örneği birbiri ardından uygulama hello olduğundan her zaman kullanılabilir. Seçin **eşzamanlı güncelleştirme** tooupdate hello uygulamanız tüm örnekleri aynı anda. Eşzamanlı güncelleştirme hızlıdır ancak hizmetinizi hello güncelleştirme işlemi sırasında kullanılamayabilir. İşiniz bittiğinde, seçin **sonraki**.

    ![Azure uygulama dağıtım ayarları sayfasında yayımlama](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. Merhaba, **Azure uygulamasını Yayımla** iletişim kutusunda **sonraki** hello kadar **Özet** sayfası görüntülenir. Lütfen ayarlarınızı doğrulayın ve ardından **Yayımla**.
   
    ![Azure uygulama Özet sayfası yayımlama](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Sonraki adımlar
- [Merhaba Visual Studio Azure uygulaması Yayımlama Sihirbazı kullanma](vs-azure-tools-publish-azure-application-wizard.md)

