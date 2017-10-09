---
title: "Azure Active Directory B2C: Özel öznitelikleri | Microsoft Docs"
description: "Nasıl tüketicileriniz hakkında Azure Active Directory B2C toocollect bilgi toouse özel öznitelikler"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active Directory B2C: tüketicileriniz hakkında özel öznitelikler toocollect bilgileri kullanın
Azure Active Directory (Azure AD) B2C dizininize bilgi (öznitelikler) yerleşik bir dizi birlikte gelir: verilen ad, Soyadı, şehir, posta kodu ve diğer öznitelikleri. Bununla birlikte, her tüketiciye yönelik uygulama hangi özniteliklerin toogather tüketicileri gelen üzerinde benzersiz gereksinimleri vardır. Azure AD B2C ile her tüketici hesapta depolanan öznitelikler hello kümesi genişletebilirsiniz. Özel öznitelikler üzerinde hello oluşturabilirsiniz [Azure portal](https://portal.azure.com/) ve aşağıda gösterildiği gibi kaydolma ilkelerinizi kullanın. Aynı zamanda okuma ve hello kullanarak bu öznitelikler yazma [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Özel öznitelikler kullanın [Azure AD Graph API Directory şema uzantıları](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Özel bir öznitelik oluşturma
1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Tıklatın **kullanıcı öznitelikleri**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Sağlayan bir **adı** hello özel öznitelik (örneğin, "ShoeSize") ve isteğe bağlı olarak bir **açıklama**. **Oluştur**'a tıklayın.
   
   > [!NOTE]
   > Yalnızca "Dize" Merhaba **veri türü** şu anda kullanılabilir değil.
   > 
   > 

Merhaba özel öznitelik hello listesinde yayımlamıştır **kullanıcı öznitelikleri**ve kaydolma ilkelerinizi kullanmak için.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Kaydolma ilkenizde özel bir öznitelik kullanın
1. [Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. **Kaydolma ilkeleri**’ne tıklayın.
3. Kayıt İlkesi (örneğin, "B2C_1_SiUp") tooopen'ı tıklatın. Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.
4. Tıklatın **kaydolma özniteliklerini** ve select hello özel öznitelik (örneğin, "ShoeSize"). **Tamam** düğmesine tıklayın.
5. Tıklatın **uygulama talepleri** ve select hello özel öznitelik. **Tamam** düğmesine tıklayın.
6. Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.

Hello İlkesi tooverify hello tüketici deneyimi hello "Şimdi Çalıştır" özelliğini kullanabilirsiniz. Şimdi "ShoeSize" Merhaba tüketici kaydolma sırasında toplanan özniteliklerinin listesini görmek ve hello belirteci gönderilen geri tooyour uygulamasındaki bakınız gerekir.

## <a name="notes"></a>Notlar
* Kayıt ilkeleri ile birlikte özel öznitelikler de oturum açma veya kaydolma ilkeleri ve profil düzenleme ilkeleri kullanılabilir.
* Özel özniteliklerin bilinen bir sınırlama yoktur. Yalnızca hello kullanıldığı ilk kez herhangi bir ilkede oluşturulan ve toohello listesini değil eklendiğinde olan **kullanıcı öznitelikleri**.

