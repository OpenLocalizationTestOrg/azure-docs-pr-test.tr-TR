---
title: "aaaAzure API Management sayfası denetimleri | Microsoft Docs"
description: "Azure API Management'ta Geliştirici Portalı şablonlarındaki kullanıma hello sayfa denetimleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Azure API Management sayfası denetimleri
Azure API Management denetimleri şablonlarda hello Geliştirici Portalı aşağıdaki hello sağlar.  
  
 toouse bir denetim yerleştirin, istenen hello konumda hello Geliştirici Portalı şablonunda. Hello gibi bazı denetimler [uygulama eylemleri](#app-actions) denetlemek, parametreleri, hello aşağıdaki örnekte gösterildiği gibi sahiptir.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Merhaba parametrelerin Hello değerleri içinde hello veri modeli hello şablonu için bir parçası olarak geçirilir. Çoğu durumda, yalnızca yapıştırabilirsiniz hello sağlanan örnek için her denetim için toowork doğru. Merhaba parametre değerleri ile ilgili daha fazla bilgi için denetim kullanılabilir her şablon için hello veri modeli bölümünde görebilirsiniz.  
  
 Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Geliştirici Portalı şablonuna sayfa denetimleri  
  
-   [Uygulama eylemleri](#app-actions)  
  
-   [temel oturum açma](#basic-signin)  
  
-   [disk belleği denetimi](#paging-control)  
  
-   [sağlayıcıları](#providers)  
  
-   [arama denetimi](#search-control)  
  
-   [Kaydolma](#sign-up)  
  
-   [Abone düğmesi](#subscribe-button)  
  
-   [aboneliği iptal etme](#subscription-cancel)  
  
##  <a name="app-actions"></a>Uygulama eylemleri  
 Merhaba `app-actions` denetim hello kullanıcı profili sayfasında hello Geliştirici Portalı'nda uygulamalarla etkileşim için bir kullanıcı arabirimi sağlar.  
  
 ![uygulamanın &#45; Eylemler denetim](./media/api-management-page-controls/APIM-app-actions-control.png "APIM uygulama eylemleri denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Parametreler  
  
|Parametre|Açıklama|  
|---------------|-----------------|  
|AppID|Merhaba uygulaması Hello kimliği.|  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `app-actions` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Uygulamalar](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>temel oturum açma  
 Merhaba `basic-signin` Denetim toplama kullanıcı oturum açma bilgilerini hello içinde hello Geliştirici Portalı'ndaki sayfasında oturum için bir denetim sağlar.  
  
 ![Basic &#45; oturum açma denetimi](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic oturum açma denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `basic-signin` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Oturum Aç](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a>disk belleği denetimi  
 Merhaba `paging-control` sayfalama işlevselliğinin Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.  
  
 ![Denetim disk belleği](./media/api-management-page-controls/APIM-paging-control.png "APIM disk belleği denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `paging-control` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [API listesi](api-management-api-templates.md#APIList)  
  
-   [Sorun listesi](api-management-issue-templates.md#IssueList)  
  
-   [Ürün Listesi](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a>sağlayıcıları  
 Merhaba `providers` denetim hello oturum açma sayfası hello Geliştirici Portalı'nda kimlik doğrulama sağlayıcıları seçimi için bir denetim sağlar.  
  
 ![sağlayıcıları Denetim](./media/api-management-page-controls/APIM-providers-control.png "APIM sağlayıcıları denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `providers` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Oturum Aç](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a>arama denetimi  
 Merhaba `search-control` arama işlevini Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.  
  
 ![Arama denetim](./media/api-management-page-controls/APIM-search-control.png "APIM arama denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `search-control` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [API listesi](api-management-api-templates.md#APIList)  
  
-   [Ürün Listesi](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a>Kaydolma  
 Merhaba `sign-up` denetim hello kayıt sayfasını hello Geliştirici Portalı'nda kullanıcı profili bilgilerini toplamak için bir denetim sağlar.  
  
 ![oturum &#45; yukarı denetim](./media/api-management-page-controls/APIM-sign-up-control.png "APIM kayıt denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `sign-up` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Kaydol](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a>Abone düğmesi  
 Merhaba `subscribe-button` bir kullanıcı tooa ürüne abone olmak için bir denetim sağlar.  
  
 ![Abone &#45; düğme denetimi](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abone düğmesi denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Parametreler  
 yok.  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `subscribe-button` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Ürün](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a>aboneliği iptal etme  
 Merhaba `subscription-cancel` denetim hello kullanıcı profili sayfasını hello Geliştirici Portalı'nda bir abonelik tooa üründe iptal etmek için bir denetim sağlar.  
  
 ![Abonelik &#45; denetim iptal](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM aboneliği iptal denetimi")  
  
### <a name="usage"></a>Kullanım  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Parametreler  
  
|Parametre|Açıklama|  
|---------------|-----------------|  
|subscriptionId|Merhaba abonelik toocancel Hello kimliği.|  
|CancelUrl|Merhaba aboneliği iptal etmeniz URL.|  
  
### <a name="developer-portal-templates"></a>Geliştirici Portalı şablonları  
 Merhaba `subscription-cancel` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.  
  
-   [Ürün](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Sonraki adımlar
Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).
