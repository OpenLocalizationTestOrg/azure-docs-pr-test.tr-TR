---
title: "Visual Studio MVC projelerinde Azure AD ile başlatıldı aaaGet | Microsoft Docs"
description: "Visual Studio kullanarak Azure AD oluşturma tooor bağlandıktan sonra MVC projelerinde Azure Active Directory'yi kullanarak tooget nasıl başlatılacağını bağlı Hizmetleri"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Bağlı hizmetler (MVC projeleri) Azure Active Directory ve Visual Studio ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Başlarken](vs-active-directory-dotnet-getting-started.md)
> * [Ne oldu](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Gerektiren kimlik doğrulaması tooaccess denetleyicileri
Projenizdeki tüm denetleyicileri ile Merhaba donatılan **Authorize** özniteliği. Bu öznitelik hello kullanıcı toobe bu denetleyicileri erişmeden önce kimlik doğrulaması gerektirir. anonim olarak, erişilen tooallow hello denetleyicisi toobe bu öznitelik hello denetleyicisinden kaldırın. Daha ayrıntılı bir düzeyde tooset hello izinleri istiyorsanız toohello denetleyici sınıfı uygulamak yerine yetkilendirme gerektiren hello özniteliği tooeach yöntemi uygulayın.

## <a name="adding-signin--signout-controls"></a>Oturum açma ekleme / SignOut denetler
tooadd hello Signın/SignOut denetimleri tooyour görünümü, hello kullanabilirsiniz **_LoginPartial.cshtml** , görünümleri, kısmi görünüm tooadd hello işlevselliği tooone. Merhaba işlevselliği eklenen toohello standart bir örneği burada verilmiştir **_Layout.cshtml** görünümü. (Not hello son öğesinde hello div sınıfı navbar-Daralt ile):

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a>Sonraki adımlar
- [Azure Active Directory hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/active-directory/) 

