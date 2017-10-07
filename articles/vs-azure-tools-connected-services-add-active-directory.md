---
title: "Visual Studio'da bağlı hizmetler kullanarak bir Azure Active Directory aaaAdding | Microsoft Docs"
description: "Merhaba Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bir Azure Active Directory'ye ekleme"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Visual Studio'da bağlı hizmetler kullanarak bir Azure Active Directory'ye ekleme
Azure Active Directory (Azure AD) kullanarak, çoklu oturum açma (SSO) ASP.NET MVC web uygulamaları veya Active Directory kimlik doğrulaması için Web API Hizmetleri'ni destekler. Azure Active Directory kimlik doğrulaması ile kullanıcılarınızın Azure Active Directory tooconnect tooyour web uygulamalarından hesaplarını kullanabilirsiniz. bir web uygulamasından bir API gösterme işlemlerinde, Azure Active Directory kimlik doğrulaması Web API ile Merhaba avantajları gelişmiş veri güvenliği kullanır. Azure AD ile toomanage kendi hesabı ve kullanıcı yönetimi ile ayrı kimlik doğrulama sistemi sahip değilsiniz.

## <a name="prerequisites"></a>Ön koşullar
- Azure hesabı - bir Azure hesabınız yoksa şunları yapabilirsiniz [ücretsiz deneme için kaydolun](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>TooAzure hello bağlantılı hizmetler kullanarak Active Directory connect iletişim
1. Visual Studio'da oluşturun veya bir ASP.NET MVC projesini ya da bir ASP.NET Web API projesini açın.

1. Çözüm Gezgini Hello hello sağ tıklatın **bağlantılı Hizmetler** düğümü ve hello bağlam menüsünden seçin **bağlı Hizmetleri Ekle**.

1. Merhaba üzerinde **bağlantılı Hizmetler** sayfasında, **Azure Active Directory ile kimlik doğrulaması**.
   
    ![Bağlı hizmetler sayfası](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. Merhaba üzerinde **giriş** hello sayfasının **yapılandırma Azure AD kimlik doğrulama** seçin **sonraki**.
   
    ![Giriş sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. Merhaba üzerinde **tek oturum açma** hello sayfasının **yapılandırma Azure AD kimlik doğrulama** Sihirbazı, bir etki alanından hello seçin **etki alanı** aşağı açılan liste. Merhaba etki alanlarının listesi hello hesap ayarları iletişim kutusunda listelenen hello hesapları tarafından erişilebilir tüm etki alanları içerir. Alternatif olarak, hello bir aradığınız, gibi bulamazsanız, bir etki alanı adı girebilirsiniz `mydomain.onmicrosoft.com`. Bir Azure Active Directory Uygulama hello seçeneği toocreate seçin veya mevcut bir Azure Active Directory uygulamadan hello ayarları kullanın. Seçin **sonraki** bittiğinde.
   
    ![Çoklu oturum açma sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Hello üzerinde **dizin erişimi** hello sayfasının **yapılandırma Azure AD kimlik doğrulama** Sihirbazı, o hello sağlamak **dizin verilerini okuma** seçeneği işaretli. 
   
    ![Dizin erişim sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Seçin **son** tooadd projenizi Azure AD kimlik doğrulaması için gerekli yapılandırma kodu ve başvuruları tooenable hello. Merhaba Active Directory etki alanı üzerinde hello görebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio görüntüler bir [ne](#how-your-project-is-modified) makale tooshow, projenizin nasıl değiştirildi. Her şeyin çalıştığı toocheck istiyorsanız değiştiren hello yapılandırma dosyalarından birini açın ve hello makalede değinilen hello ayarlarını doğrulayın. 

## <a name="how-your-project-is-modified"></a>Projenizi nasıl değiştirilir
Başlangıç Sihirbazı'nı çalıştırdığınızda, Visual Studio Azure Active Directory ve ilişkili başvurular tooyour proje ekler. Yapılandırma dosyaları ve kod dosyaları projenizdeki ayrıca Azure AD değiştirilmiş tooadd destek sağlar. Visual Studio yapar hello belirli değişiklikler hello proje türüne bağlıdır. ASP.NET MVC projeleri nasıl değiştirilir hakkında ayrıntılı bilgi için bkz: [hangi happened – MVC projeleri](http://go.microsoft.com/fwlink/p/?LinkID=513809). Web API projeleri için bkz: [ne – Web API projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Active Directory için MSDN Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Azure Active Directory belgeleri](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog postası: Giriş tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

