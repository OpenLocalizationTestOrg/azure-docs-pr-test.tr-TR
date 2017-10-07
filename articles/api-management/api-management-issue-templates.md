---
title: "Azure API Management'te aaaIssue şablonları | Microsoft Docs"
description: "Nasıl toocustomize hello hello sorunu hello Azure API Management'ta Geliştirici portalını sayfalarında içeriğini öğrenin."
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="7b6b6-103">Azure API Management şablonları verme</span><span class="sxs-lookup"><span data-stu-id="7b6b6-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="7b6b6-104">Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7b6b6-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7b6b6-106">Bu bölümdeki Hello şablonları hello Geliştirici Portalı'nda toocustomize hello hello sorunu sayfaların içeriğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="7b6b6-107">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="7b6b6-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="7b6b6-108">Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="7b6b6-109">İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="7b6b6-110">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7b6b6-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="7b6b6-111"><a name="IssueList"></a>Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="7b6b6-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="7b6b6-112">Merhaba **sorun listesi** şablonu verir hello sorun listesi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="7b6b6-113">![Sorun listesi Geliştirici Portalı](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM sorun listesi Geliştirici Portalı")</span><span class="sxs-lookup"><span data-stu-id="7b6b6-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7b6b6-114">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7b6b6-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7b6b6-115">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7b6b6-115">Controls</span></span>  
 <span data-ttu-id="7b6b6-116">Merhaba `Issue list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7b6b6-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7b6b6-117">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="7b6b6-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="7b6b6-118">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7b6b6-118">Data model</span></span>  
  
|<span data-ttu-id="7b6b6-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="7b6b6-119">Property</span></span>|<span data-ttu-id="7b6b6-120">Tür</span><span class="sxs-lookup"><span data-stu-id="7b6b6-120">Type</span></span>|<span data-ttu-id="7b6b6-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7b6b6-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7b6b6-122">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="7b6b6-122">Issues</span></span>|<span data-ttu-id="7b6b6-123">Koleksiyonu [sorunu](api-management-template-data-model-reference.md#Issue) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="7b6b6-124">Merhaba sorunları görünür toohello geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="7b6b6-125">Sayfalama</span><span class="sxs-lookup"><span data-stu-id="7b6b6-125">Paging</span></span>|<span data-ttu-id="7b6b6-126">[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="7b6b6-127">Hello disk belleği bilgileri hello uygulamaları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="7b6b6-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="7b6b6-128">IsAuthenticated</span></span>|<span data-ttu-id="7b6b6-129">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7b6b6-129">boolean</span></span>|<span data-ttu-id="7b6b6-130">Merhaba geçerli kullanıcının oturum açmış toohello Geliştirici Portalı olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="7b6b6-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="7b6b6-131">CanReportIssues</span></span>|<span data-ttu-id="7b6b6-132">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7b6b6-132">boolean</span></span>|<span data-ttu-id="7b6b6-133">Merhaba geçerli kullanıcının izinlerini toofile bir sorun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="7b6b6-134">Arama</span><span class="sxs-lookup"><span data-stu-id="7b6b6-134">Search</span></span>|<span data-ttu-id="7b6b6-135">Dize</span><span class="sxs-lookup"><span data-stu-id="7b6b6-135">string</span></span>|<span data-ttu-id="7b6b6-136">Bu özellik kullanım dışıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b6b6-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7b6b6-137">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7b6b6-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="7b6b6-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b6b6-138">Next steps</span></span>
<span data-ttu-id="7b6b6-139">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7b6b6-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
