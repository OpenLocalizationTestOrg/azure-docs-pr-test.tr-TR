---
title: "etki alanları arası ilkeler aaaAzure API Management | Microsoft Docs"
description: "Etki alanları arası ilkeler Azure API Management'te kullanıma hello hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>API Management etki alanları arası ilkeler
Bu konuda API Management ilkelere hello için bir başvuru sağlar. Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a>Etki alanı ilkelerini arası  
  
-   [Etki alanları arası çağrılar izin](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -yapar hello API erişilebilir Microsoft Silverlight Adobe Flash ve tarayıcı tabanlı istemcilerden.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağıran ekler.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - JSON ile destek tooan işlemi (JSONP) doldurma ekler veya bir API tooallow etki alanları arası JavaScript tarayıcı tabanlı istemcilerden çağırır.  
  
##  <a name="AllowCrossDomainCalls"></a>Etki alanları arası çağrılar izin ver  
 Kullanım hello `cross-domain` İlkesi toomake hello API Adobe Flash ve Microsoft Silverlight tarayıcı tabanlı istemcilerden erişilebilir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|etki alanları arası|Kök öğesi. Alt öğeler toohello uygun olmalıdır [Adobe etki alanları arası ilke dosya belirtimi](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Evet|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** genel  
  
##  <a name="CORS"></a>CORS  
 Merhaba `cors` ilkesi ekler çıkış noktaları arası kaynak paylaşımını (CORS) tooan işlemi destekler veya bir API tooallow etki alanları arası tarayıcı tabanlı istemcilerden çağırır.  
  
 CORS tooallow belirli çıkış noktaları arası (bir web sayfası tooother etki alanları JavaScript yapılan yani XMLHttpRequests çağrıları) isteklerini olup olmadığını belirlemek ve bir tarayıcı ve sunucu toointeract sağlar. Bu, yalnızca kaynak aynı isteklerine izin'den daha fazla esneklik sağlar, ancak tüm çıkış noktaları arası istekleri izin vererek değerinden daha güvenlidir.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Örnek  
 Bu örnek nasıl toosupport öncesi uçuş, özel üstbilgi veya dışında GET ve POST yöntemleri olanlar gibi istekleri gösterir. toosupport özel üstbilgi ve ek HTTP fiilleri kullanın hello `allowed-methods` ve `allowed-headers` bölümler hello aşağıdaki örnekte gösterildiği gibi.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|cors|Kök öğesi.|Evet|Yok|  
|izin verilen çıkış|İçeren `origin` çıkış noktası etki alanları arası istekleri için izin verilen hello açıklayan öğeler. `allowed-origins`ya da tek bir içerebilir `origin` belirtir öğesi `*` tooallow her türlü kaynağa veya bir veya daha fazla `origin` bir URI içeren öğeler.|Evet|Yok|  
|Kaynak|Merhaba değer ya da olabilir `*` tooallow tüm kaynaklara ya da tek bir kaynak belirten bir URI. Merhaba URI düzeni, ana bilgisayar ve bağlantı noktası eklemeniz gerekir.|Evet|Başlangıç bağlantı noktası bir URI atlanırsa, HTTP için 80 numaralı bağlantı noktası kullanılır ve HTTPS için 443 numaralı bağlantı noktası kullanılır.|  
|izin verilen yöntemleri|Yöntemleri dışında GET veya POST izin verilir, bu öğe gereklidir. İçeren `method` hello desteklenen HTTP fiilleri belirtin öğeleri.|Hayır|Bu bölümde mevcut değilse, GET ve POST desteklenir.|  
|Yöntemi|Bir HTTP fiili belirtir.|En az bir `method` öğesi olup gerekli hello `allowed-methods` bölüm mevcut.|Yok|  
|izin verilen üstbilgileri|Bu öğeyi içeren `header` öğeleri hello isteğine dahil hello başlıklarının adlarını belirtme.|Hayır|Yok|  
|sunmaya üstbilgileri|Bu öğeyi içeren `header` öğeleri hello istemci tarafından erişilebilecek hello başlıklarının adlarını belirtme.|Hayır|Yok|  
|üst bilgi|Bir üstbilgi adı belirtir.|En az bir `header` öğesi gerekli `allowed-headers` veya `expose-headers` hello bölüm mevcut değilse.|Yok|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|izin ver-kimlik bilgileri|Merhaba `Access-Control-Allow-Credentials` hello ön yanıt üstbilgisi kümesi toohello değeri bu özniteliğin olmalı ve etki alanları arası istek hello istemcinin özelliği toosubmit kimlik bilgileri etkiler.|Hayır|False|  
|Ön-sonuç-max-age|Merhaba `Access-Control-Max-Age` hello ön yanıt üstbilgisi kümesi toohello değeri bu özniteliğin olmalı ve hello kullanıcı aracısının özelliği toocache öncesi uçuş yanıt etkiler.|Hayır|0|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** gelen  
  
-   **İlke kapsamları:** API, işlemi  
  
##  <a name="JSONP"></a>JSONP  
 Merhaba `jsonp` İlkesi (JSONP) destek tooan işlem ya da bir API tooallow etki alanları arası çağrılar JavaScript tarayıcı tabanlı istemcilerden doldurma ile JSON ekler. JSONP JavaScript programları toorequest verileri farklı bir etki alanındaki bir sunucudan kullanılan bir yöntemdir. JSONP atlar burada erişim tooweb sayfaları olmalıdır hello çoğu web tarayıcısı tarafından uygulanan hello sınırlaması aynı etki alanı.  
  
### <a name="policy-statement"></a>İlke bildirimi  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Örnek  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Merhaba geri çağırma parametresi olmadan hello yöntemini çağırırsanız? cb = XXX (olmadan işlev çağrısı sarmalayıcı) düz JSON döndürecektir.  
  
 Merhaba geri çağırma parametresi eklerseniz `?cb=XXX` hello özgün JSON sonuçları gibi hello geri çağırma işlevi geçici kaydırma bir JSONP sonucunu döndürür`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Öğeleri  
  
|Ad|Açıklama|Gerekli|  
|----------|-----------------|--------------|  
|jsonp|Kök öğesi.|Evet|  
  
### <a name="attributes"></a>Öznitelikler  
  
|Ad|Açıklama|Gerekli|Varsayılan|  
|----------|-----------------|--------------|-------------|  
|geri çağırma parametre adı|Merhaba etki alanları arası JavaScript işlev çağrısı hello işlevi bulunduğu hello tam etki alanı adı öneki.|Evet|Yok|  
  
### <a name="usage"></a>Kullanım  
 Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **İlke bölümleri:** giden  
  
-   **İlke kapsamları:** genel, ürün, API işlemi  
  
## <a name="next-steps"></a>Sonraki adımlar
İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).  