---
title: "Federasyon tek oturum açma için Galeri olmayan uygulama yapılandırma aaaProblem | Microsoft Docs"
description: "Bazı listelenmeyen Federasyon tek oturum açma tooyour özel SAML uygulama hello Azure AD uygulama galerisinde yapılandırırken karşılaşabileceğiniz hello yaygın sorunları ele"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Federasyon tek oturum açma için Galeri olmayan uygulama yapılandırma sorunu

Bir uygulama yapılandırırken bir sorunla karşılaşırsanız. Merhaba makaledeki tüm hello adımları takip doğrulayın [hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Merhaba uygulaması başka bir örneği eklenemiyor

bir uygulamanın ikinci bir örneğini tooadd, toobe yapabileceksiniz da gerekir:

-   Merhaba ikinci örneği için benzersiz bir tanımlayıcı yapılandırın. Merhaba ilk örnek için kullanılan aynı tanımlayıcısı mümkün tooconfigure hello olmayacaktır.

-   Merhaba hello ilk örnek için kullanılan daha farklı bir sertifika yapılandırın.

Merhaba, uygulama hello yukarıdaki hiçbirini desteklemiyor. Ardından, mümkün tooconfigure ikinci bir örneğini olmayacaktır.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Merhaba Entityıd (kullanıcı tanımlayıcısı) biçimi belirlendiği

Azure AD hello yanıtta toohello uygulama kullanıcı kimlik doğrulamasından sonra gönderir mümkün tooselect hello Entityıd (kullanıcı tanımlayıcısı) biçimi olmayacaktır.

Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello. Daha fazla bilgi için hello makale ziyaret [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy, hello bölümünde

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Merhaba uygulama meta verileri veya sertifika Azure AD'den nereden bulabilirim

toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri. Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.

Azure AD, URL tooget hello meta verilerinin sağlamaz. Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Toocustomize SAML talep tooan uygulama nasıl gönderileceğini bilmiyorsanız

toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
