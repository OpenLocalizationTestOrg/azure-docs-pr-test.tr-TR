---
title: "Sorun Azure API Management şablonlarında | Microsoft Docs"
description: "Azure API Management'ta Geliştirici portalını sorunu sayfalarında içeriğini özelleştirmeyi öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="48606-103">Azure API Management şablonları verme</span><span class="sxs-lookup"><span data-stu-id="48606-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="48606-104">Azure API Management Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriği özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="48606-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="48606-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve düzenleyiciyi, gibi [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfa denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde sayfaların yapılandırmak için büyük esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="48606-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="48606-106">Bu bölümdeki şablonları Geliştirici Portalı sorunu sayfalarında içeriğini özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="48606-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="48606-107">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="48606-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="48606-108">Örnek varsayılan şablonları aşağıdaki belgelerde yer alır ancak değişikliği sürekli geliştirmeler nedeniyle tabidir.</span><span class="sxs-lookup"><span data-stu-id="48606-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="48606-109">İstenen tek tek şablonları giderek Geliştirici Portalı'nda Canlı varsayılan şablonları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48606-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="48606-110">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="48606-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="48606-111"><a name="IssueList"></a>Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="48606-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="48606-112">**Sorun listesi** şablonu Geliştirici portalında sorun listesi sayfasının gövdesi özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="48606-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="48606-113">![Sorun listesi Geliştirici Portalı](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM sorun listesi Geliştirici Portalı")</span><span class="sxs-lookup"><span data-stu-id="48606-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="48606-114">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="48606-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="48606-115">Denetimler</span><span class="sxs-lookup"><span data-stu-id="48606-115">Controls</span></span>  
 <span data-ttu-id="48606-116">`Issue list` Şablonu, aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="48606-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="48606-117">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="48606-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="48606-118">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="48606-118">Data model</span></span>  
  
|<span data-ttu-id="48606-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="48606-119">Property</span></span>|<span data-ttu-id="48606-120">Tür</span><span class="sxs-lookup"><span data-stu-id="48606-120">Type</span></span>|<span data-ttu-id="48606-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="48606-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="48606-122">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="48606-122">Issues</span></span>|<span data-ttu-id="48606-123">Koleksiyonu [sorunu](api-management-template-data-model-reference.md#Issue) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="48606-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="48606-124">Geçerli kullanıcıya görülebilir sorunları.</span><span class="sxs-lookup"><span data-stu-id="48606-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="48606-125">Sayfalama</span><span class="sxs-lookup"><span data-stu-id="48606-125">Paging</span></span>|<span data-ttu-id="48606-126">[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.</span><span class="sxs-lookup"><span data-stu-id="48606-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="48606-127">Uygulamaları koleksiyonu için disk belleği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="48606-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="48606-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="48606-128">IsAuthenticated</span></span>|<span data-ttu-id="48606-129">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="48606-129">boolean</span></span>|<span data-ttu-id="48606-130">Olup geçerli kullanıcı Geliştirici portalına açan.</span><span class="sxs-lookup"><span data-stu-id="48606-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="48606-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="48606-131">CanReportIssues</span></span>|<span data-ttu-id="48606-132">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="48606-132">boolean</span></span>|<span data-ttu-id="48606-133">Geçerli kullanıcının bir sorunu dosya izni olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="48606-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="48606-134">Arama</span><span class="sxs-lookup"><span data-stu-id="48606-134">Search</span></span>|<span data-ttu-id="48606-135">Dize</span><span class="sxs-lookup"><span data-stu-id="48606-135">string</span></span>|<span data-ttu-id="48606-136">Bu özellik kullanım dışıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="48606-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="48606-137">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="48606-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="48606-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48606-138">Next steps</span></span>
<span data-ttu-id="48606-139">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="48606-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>