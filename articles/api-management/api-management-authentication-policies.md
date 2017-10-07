---
title: "aaaAzure API Management kimlik doğrulama ilkeleri | Microsoft Docs"
description: "Azure API Management'te kullanıma hello kimlik doğrulama ilkeleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>API Management kimlik doğrulama ilkeleri
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a>Kimlik doğrulama ilkeleri  
  
-   [Basic ile kimlik doğrulaması](api-management-authentication-policies.md#Basic) -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.  
  
-   [İstemci sertifikası ile kimlik doğrulaması](api-management-authentication-policies.md#ClientCertificate) -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.  
  
##  <a name="Basic"></a>Basic ile kimlik doğrulaması  
 Kullanım hello `authentication-basic` temel kimlik doğrulaması kullanarak arka uç hizmeti ile ilke tooauthenticate. Bu ilke etkili bir şekilde hello HTTP yetkilendirme üstbilgisi toohello hello belirtilen değeri karşılık gelen toohello kimlik bilgilerini ayarlar.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|kimlik doğrulama-temel|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|kullanıcı adı|Merhaba kullanıcı hello temel kimlik bilgisi adını belirtir.|Evet|Yok|  
|password|Merhaba temel kimlik bilgisi Hello parolasını belirtir.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** API  
  
##  <a name="ClientCertificate"></a>İstemci sertifikası ile kimlik doğrulaması  
 Kullanım hello `authentication-certificate` istemci sertifikasını kullanarak bir arka uç hizmeti ile ilke tooauthenticate. Merhaba sertifikanın gerekir toobe [API yönetime yüklü](http://go.microsoft.com/fwlink/?LinkID=511599) ilk ve kendi parmak izi tarafından tanımlanır.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|kimlik doğrulama sertifikası|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|parmak izi|Merhaba istemci sertifikası parmak izi hello.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** API  
  

## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  