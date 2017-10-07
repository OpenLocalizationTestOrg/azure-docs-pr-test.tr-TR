---
title: "Uygulama hizmeti dağıtım kimlik bilgileri aaaAzure | Microsoft Docs"
description: "Nasıl toouse hello Azure uygulama hizmeti dağıtım kimlik bilgileri öğrenin."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Dağıtım kimlik bilgileri Azure App Service için yapılandırma
[Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) iki tür kimlik bilgilerini destekler [yerel Git dağıtımı](app-service-deploy-local-git.md) ve [FTP/S dağıtım](app-service-deploy-ftp.md). Bunlar olan değil hello Azure Active Directory kimlik bilgileriniz ile aynı.

* **Kullanıcı düzeyinde kimlik**: bir hello tüm Azure hesabı için kimlik bilgileri kümesi. Herhangi bir uygulama izni tooaccess Azure hesabı hello herhangi abonelikte için kullanılan toodeploy tooApp hizmet olabilir. Yapılandırdığınız hello varsayılan kimlik bilgileri kümesi bunlar **uygulama hizmetleri** > **&lt;app_name >** > **dağıtım kimlik bilgileri**. Bu olduğunu da hello hello portal GUI ortaya varsayılan kümesi (Merhaba gibi **genel bakış** ve **özellikleri** , uygulamanızın, [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Rol tabanlı erişim denetimi (RBAC) veya ortak yönetici izinleri aracılığıyla erişim tooAzure kaynaklara temsilci atarken, erişim tooan uygulama alan her bir Azure kullanıcı erişimi iptal kadar güncelleştirmesini kişisel kullanıcı düzeyinde kimlik bilgilerini kullanabilir. Bu dağıtım kimlik bilgileri Azure diğer kullanıcılarla Paylaşılmaması gerekiyor.
    >
    >

* **Uygulama düzeyinde kimlik**: bir her uygulama için kimlik bilgileri kümesi. Yalnızca kullanılan toodeploy toothat uygulama olabilir. her uygulamanın uygulama oluşturma sırasında otomatik olarak oluşturulur ve hello uygulamanın içinde bulunan için yayımlama profili hello kimlik bilgileri. Merhaba kimlik bilgilerini el ile yapılandıramazsınız, ancak bunları bir uygulama için dilediğiniz zaman sıfırlayabilirsiniz.

    > [!NOTE]
    > Sipariş toogive birisi erişim toothese kimlik bilgilerini aracılığıyla rol tabanlı erişim denetimi (RBAC), toomake gerek bunları katkıda bulunan veya hello Web uygulaması üzerinde daha yüksek. Okuyucular toopublish izin verilmiyor ve bu nedenle bu kimlik bilgilerini erişemiyor.
    >
    >

## <a name="userscope"></a>Ayarlama ve kullanıcı düzeyinde kimlik bilgilerini sıfırlama

Bir uygulamanın ait kullanıcı düzeyinde kimlik bilgilerinizi yapılandırabilirsiniz [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources). Ne olursa olsun hangi uygulamanın bu kimlik bilgilerini yapılandırın, Azure içinde tüm abonelikler için hesap ve tooall uygulamaları geçerlidir. 

tooconfigure kullanıcı düzeyinde kimlik bilgilerinizi:

1. Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **dağıtım kimlik bilgileri**.

    > [!NOTE]
    > Merhaba Portalı'nda hello dağıtım kimlik bilgileri dikey penceresini erişebilmeniz için önce en az bir uygulama olmalıdır. Bununla birlikte, hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kullanıcı düzeyinde kimlik bilgileri olan bir uygulama olmadan yapılandırabilirsiniz.

2. Merhaba kullanıcı adını ve parolasını yapılandırın ve ardından **kaydetmek**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Dağıtım kimlik bilgilerinizi ayarladıktan sonra hello bulabilirsiniz *Git* dağıtım kullanıcıadı uygulamanızın **genel bakış**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

ve ve *FTP* dağıtım kullanıcıadı uygulamanızın **özellikleri**.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure kullanıcı düzeyinde dağıtım parolanızı göstermez. Merhaba parolanızı unutursanız, alınamıyor. Ancak, bu bölümdeki hello adımları izleyerek kimlik bilgilerinizi sıfırlayabilirsiniz.
>
>  

## <a name="appscope"></a>Alma ve uygulama düzeyinde kimlik bilgilerini sıfırlama
App Service içinde her uygulama için uygulama düzeyinde kimlik bilgilerini hello depolanan XML yayımlama profili.

tooget hello uygulama düzeyinde kimlik bilgileri:

1. Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.

2. Tıklatın **... Daha fazla** > **Get yayımlama profili**, indirme başlatılması için ve bir. PublishSettings dosyası.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Açık hello. PublishSettings dosyasını açıp hello bulur `<publishProfile>` hello özniteliği etiketiyle `publishMethod="FTP"`. Daha sonra kendi `userName` ve `password` öznitelikleri.
Bunlar hello uygulama düzeyinde kimlik bilgileridir.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Benzer toohello kullanıcı düzeyinde kimlik bilgileri, hello FTP dağıtım kullanıcı adınızdır hello biçiminde `<app_name>\<username>`, ve hello Git dağıtım kullanıcı adı yalnızca `<username>` hello önceki olmadan `<app_name>\`.

tooreset hello uygulama düzeyinde kimlik bilgileri:

1. Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.

2. Tıklatın **... Daha fazla** > **sıfırlama yayımlama profili**. Tıklatın **Evet** tooconfirm hello sıfırlayın.

    Merhaba sıfırlama eylemi herhangi önceden indirilmiş geçersiz kılar. PublishSettings dosyaları.

## <a name="next-steps"></a>Sonraki adımlar

Öğrenin toouse bu kimlik bilgileri toodeploy uygulamanızdan [yerel Git](app-service-deploy-local-git.md) veya kullanarak [FTP/S](app-service-deploy-ftp.md).
