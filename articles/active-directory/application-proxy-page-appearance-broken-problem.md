---
title: "aaaApplication sayfası için uygulama proxy'si uygulama doğru görüntülemiyor | Microsoft Docs"
description: "Azure AD ile tümleşik Hello sayfa doğru bir uygulama Proxy uygulamada değil görüntülenirken Kılavuzu"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Uygulama sayfası için uygulama proxy'si uygulama düzgün görüntülenmez

Bu makale yardımcı, Azure Active Directory Uygulama proxy'si uygulamalarıyla tootroubleshoot sorunları toohello sayfasına gidin, ancak başlangıç sayfasında bir şey doğru görünmüyor.

## <a name="overview"></a>Genel Bakış
Bir uygulama proxy'si uygulama yayımladığınızda, yalnızca, kök altındaki sayfalar Merhaba uygulaması erişirken erişilebilir. Merhaba sayfa doğru görüntülemiyorsa hello kök İç URL hello uygulama için kullanılan bazı sayfası kaynakları eksik olabilir. tooresolve, yayımlanan emin olun *tüm* hello hello sayfa için kaynaklar, uygulamanızın bir parçası olarak.

Bu durum, hello sorunundan Ağ İzleyicisi'ni açarak doğrulayabilirsiniz (Fiddler veya F12 gibi araçlar Internet Explorer/kenar) hello sayfa yüklenirken ve 404 hatalarını aranıyor. Bu, şu anda bulunamıyor ve yayımlanan toobe hala gerekebilir hello sayfaları gösterir.

Bu durumda bir örnek olarak, bir iç URL'sini kullanarak giderleri uygulama yayımlandı varsayalım <http://myapps/expenses>, ancak hello uygulamanın kullandığı hello stil <http://myapps/style.css>. Bu durumda, Hello giderleri uygulama yüklenirken throw şekilde çalışırken tooload style.css 404 hatası hello stil sayfası, uygulamanızda yayınlanmadı. Bu örnekte, hello sorunun bir iç URL'si ile Merhaba uygulaması yayımlama tarafından çözülmüş <http://myapp/> yerine.

## <a name="problems-with-publishing-as-one-application"></a>Bir uygulama yayımlama sorunları

Olası toopublish değilse içindeki tüm kaynakların aynı uygulama Merhaba, aralarında bağlantıları etkinleştirmek ve birden çok uygulama toopublish gerekir.

toodo bu nedenle, hello kullanmanızı öneririz [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) çözümü. Ancak, bu çözüm hello sertifika etki alanınız için sahip olduğunuz ve uygulamalarınızı tam etki alanı adlarını (FQDN) kullanmak gerektirir. Diğer seçenekler için bkz: Merhaba [bağlantıların belgelerine sorun giderme](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md)
