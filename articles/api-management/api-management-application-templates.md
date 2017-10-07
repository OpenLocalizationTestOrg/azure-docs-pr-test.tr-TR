---
title: "Azure API Management'te aaaApplication şablonları | Microsoft Docs"
description: "Nasıl toocustomize hello hello uygulama hello Azure API Management'ta Geliştirici portalını sayfalarında içeriğini öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="36d09-103">Azure API Management'te uygulama şablonları</span><span class="sxs-lookup"><span data-stu-id="36d09-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="36d09-104">Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="36d09-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="36d09-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="36d09-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="36d09-106">Bu bölümdeki Hello şablonları hello Geliştirici Portalı'nda hello uygulama sayfaları toocustomize Merhaba içeriğine sağlar.</span><span class="sxs-lookup"><span data-stu-id="36d09-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="36d09-107">Uygulama listesi</span><span class="sxs-lookup"><span data-stu-id="36d09-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="36d09-108">Uygulama</span><span class="sxs-lookup"><span data-stu-id="36d09-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="36d09-109">Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="36d09-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="36d09-110">İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36d09-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="36d09-111">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="36d09-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="36d09-112"><a name="ProductList"></a>Uygulama listesi</span><span class="sxs-lookup"><span data-stu-id="36d09-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="36d09-113">Merhaba **uygulama listesini** şablonu verir hello uygulama listesi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="36d09-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="36d09-114">![Uygulama listesi sayfasında Geliştirici Portalı şablonları](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM uygulama listesi sayfasında Geliştirici Portalı şablonları")</span><span class="sxs-lookup"><span data-stu-id="36d09-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="36d09-115">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="36d09-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="36d09-116">Denetimler</span><span class="sxs-lookup"><span data-stu-id="36d09-116">Controls</span></span>  
 <span data-ttu-id="36d09-117">Merhaba `Product list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="36d09-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="36d09-118">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="36d09-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="36d09-119">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="36d09-119">Data model</span></span>  
  
|<span data-ttu-id="36d09-120">Özellik</span><span class="sxs-lookup"><span data-stu-id="36d09-120">Property</span></span>|<span data-ttu-id="36d09-121">Tür</span><span class="sxs-lookup"><span data-stu-id="36d09-121">Type</span></span>|<span data-ttu-id="36d09-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d09-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="36d09-123">Sayfalama</span><span class="sxs-lookup"><span data-stu-id="36d09-123">Paging</span></span>|<span data-ttu-id="36d09-124">[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.</span><span class="sxs-lookup"><span data-stu-id="36d09-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="36d09-125">Hello disk belleği bilgileri hello uygulamaları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="36d09-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="36d09-126">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="36d09-126">Applications</span></span>|<span data-ttu-id="36d09-127">Koleksiyonu [uygulama](api-management-template-data-model-reference.md#Application) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="36d09-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="36d09-128">Merhaba uygulamaları görünür toohello geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="36d09-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="36d09-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="36d09-129">CategoryName</span></span>|<span data-ttu-id="36d09-130">Dize</span><span class="sxs-lookup"><span data-stu-id="36d09-130">string</span></span>|<span data-ttu-id="36d09-131">Uygulama Hello kategorisi.</span><span class="sxs-lookup"><span data-stu-id="36d09-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="36d09-132">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="36d09-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="36d09-133"><a name="Application"></a>Uygulama</span><span class="sxs-lookup"><span data-stu-id="36d09-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="36d09-134">Merhaba **uygulama** şablonu verir hello uygulama sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="36d09-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="36d09-135">![Uygulama sayfası Geliştirici Portalı şablonları](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM uygulama sayfasında Geliştirici Portalı şablonları")</span><span class="sxs-lookup"><span data-stu-id="36d09-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="36d09-136">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="36d09-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="36d09-137">Denetimler</span><span class="sxs-lookup"><span data-stu-id="36d09-137">Controls</span></span>  
 <span data-ttu-id="36d09-138">Merhaba `Application` şablon herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="36d09-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="36d09-139">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="36d09-139">Data model</span></span>  
 <span data-ttu-id="36d09-140">[Uygulama](api-management-template-data-model-reference.md#Application) varlık.</span><span class="sxs-lookup"><span data-stu-id="36d09-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="36d09-141">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="36d09-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="36d09-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36d09-142">Next steps</span></span>
<span data-ttu-id="36d09-143">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="36d09-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
