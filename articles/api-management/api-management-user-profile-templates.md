---
title: "Kullanıcı profili şablonları Azure API Management | Microsoft Docs"
description: "Azure API Management'ta Geliştirici portalını kullanıcı profili sayfalarında içeriğini özelleştirmeyi öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="05eb3-103">Azure API Management'te kullanıcı profil şablonları</span><span class="sxs-lookup"><span data-stu-id="05eb3-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="05eb3-104">Azure API Management Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriği özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="05eb3-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve düzenleyiciyi, gibi [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfa denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde sayfaların yapılandırmak için büyük esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="05eb3-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="05eb3-106">Bu bölümdeki şablonları Geliştirici Portalı kullanıcı profili sayfalarında içeriğini özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="05eb3-107">Profili</span><span class="sxs-lookup"><span data-stu-id="05eb3-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="05eb3-108">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="05eb3-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="05eb3-109">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="05eb3-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="05eb3-110">Hesap bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="05eb3-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="05eb3-111">Örnek varsayılan şablonları aşağıdaki belgelerde yer alır ancak değişikliği sürekli geliştirmeler nedeniyle tabidir.</span><span class="sxs-lookup"><span data-stu-id="05eb3-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="05eb3-112">İstenen tek tek şablonları giderek Geliştirici Portalı'nda Canlı varsayılan şablonları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05eb3-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="05eb3-113">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="05eb3-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="05eb3-114"><a name="Profile"></a>Profili</span><span class="sxs-lookup"><span data-stu-id="05eb3-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="05eb3-115">**Profil** şablon kullanıcı profili sayfasını Geliştirici Portalı'nda kullanıcı profili bölümünü özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="05eb3-116">![Kullanıcı profili sayfasını](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM kullanıcı profili sayfası")</span><span class="sxs-lookup"><span data-stu-id="05eb3-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="05eb3-117">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="05eb3-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="05eb3-118">Denetimler</span><span class="sxs-lookup"><span data-stu-id="05eb3-118">Controls</span></span>  
 <span data-ttu-id="05eb3-119">Bu şablon herhangi kullanamazsınız [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="05eb3-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="05eb3-120">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="05eb3-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="05eb3-121">[Profil](#Profile), [uygulamaları](#Applications), ve [abonelikleri](#Subscriptions) şablonları aynı veri modeli paylaşma ve aynı şablon verileri alma.</span><span class="sxs-lookup"><span data-stu-id="05eb3-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="05eb3-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="05eb3-122">Property</span></span>|<span data-ttu-id="05eb3-123">Tür</span><span class="sxs-lookup"><span data-stu-id="05eb3-123">Type</span></span>|<span data-ttu-id="05eb3-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05eb3-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="05eb3-125">FirstName</span><span class="sxs-lookup"><span data-stu-id="05eb3-125">firstName</span></span>|<span data-ttu-id="05eb3-126">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-126">string</span></span>|<span data-ttu-id="05eb3-127">Geçerli kullanıcının adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-127">First name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-128">Soyadı</span><span class="sxs-lookup"><span data-stu-id="05eb3-128">lastName</span></span>|<span data-ttu-id="05eb3-129">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-129">string</span></span>|<span data-ttu-id="05eb3-130">Geçerli kullanıcının soyadı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-131">Şirket adı</span><span class="sxs-lookup"><span data-stu-id="05eb3-131">companyName</span></span>|<span data-ttu-id="05eb3-132">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-132">string</span></span>|<span data-ttu-id="05eb3-133">Geçerli kullanıcının şirket adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="05eb3-134">addresserEmail</span></span>|<span data-ttu-id="05eb3-135">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-135">string</span></span>|<span data-ttu-id="05eb3-136">Geçerli kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="05eb3-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="05eb3-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="05eb3-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="05eb3-138">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-138">string</span></span>|<span data-ttu-id="05eb3-139">Geçerli kullanıcı için analiz görüntülemek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="05eb3-140">Abonelikleri</span><span class="sxs-lookup"><span data-stu-id="05eb3-140">subscriptions</span></span>|<span data-ttu-id="05eb3-141">Koleksiyonu [abonelik](api-management-template-data-model-reference.md#Subscription) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="05eb3-142">Geçerli kullanıcı için abonelikler.</span><span class="sxs-lookup"><span data-stu-id="05eb3-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="05eb3-143">uygulamalar</span><span class="sxs-lookup"><span data-stu-id="05eb3-143">applications</span></span>|<span data-ttu-id="05eb3-144">Koleksiyonu [uygulama](api-management-template-data-model-reference.md#Application) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="05eb3-145">Geçerli kullanıcının uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="05eb3-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-146">changePasswordUrl</span></span>|<span data-ttu-id="05eb3-147">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-147">string</span></span>|<span data-ttu-id="05eb3-148">Geçerli kullanıcının parolasını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="05eb3-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="05eb3-150">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-150">string</span></span>|<span data-ttu-id="05eb3-151">Geçerli kullanıcı için e-posta ve adını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="05eb3-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="05eb3-152">canChangePassword</span></span>|<span data-ttu-id="05eb3-153">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-153">boolean</span></span>|<span data-ttu-id="05eb3-154">Olup geçerli kullanıcı parolalarını değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="05eb3-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="05eb3-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="05eb3-155">isSystemUser</span></span>|<span data-ttu-id="05eb3-156">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-156">boolean</span></span>|<span data-ttu-id="05eb3-157">Geçerli kullanıcının yerleşik bir üyesi olup [grupları](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="05eb3-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="05eb3-158">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="05eb3-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="05eb3-159"><a name="Subscriptions"></a>Abonelikleri</span><span class="sxs-lookup"><span data-stu-id="05eb3-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="05eb3-160">**Abonelikleri** şablon kullanıcı profili sayfasını Geliştirici portalında abonelikleri bölümünü özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="05eb3-161">![Kullanıcı abonelik sayfası](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM kullanıcı abonelik sayfası")</span><span class="sxs-lookup"><span data-stu-id="05eb3-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="05eb3-162">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="05eb3-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="05eb3-163">Denetimler</span><span class="sxs-lookup"><span data-stu-id="05eb3-163">Controls</span></span>  
 <span data-ttu-id="05eb3-164">Bu şablon aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="05eb3-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="05eb3-165">aboneliği iptal etme</span><span class="sxs-lookup"><span data-stu-id="05eb3-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="05eb3-166">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="05eb3-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="05eb3-167">[Profil](#Profile), [uygulamaları](#Applications), ve [abonelikleri](#Subscriptions) şablonları aynı veri modeli paylaşma ve aynı şablon verileri alma.</span><span class="sxs-lookup"><span data-stu-id="05eb3-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="05eb3-168">Özellik</span><span class="sxs-lookup"><span data-stu-id="05eb3-168">Property</span></span>|<span data-ttu-id="05eb3-169">Tür</span><span class="sxs-lookup"><span data-stu-id="05eb3-169">Type</span></span>|<span data-ttu-id="05eb3-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05eb3-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="05eb3-171">FirstName</span><span class="sxs-lookup"><span data-stu-id="05eb3-171">firstName</span></span>|<span data-ttu-id="05eb3-172">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-172">string</span></span>|<span data-ttu-id="05eb3-173">Geçerli kullanıcının adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-173">First name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-174">Soyadı</span><span class="sxs-lookup"><span data-stu-id="05eb3-174">lastName</span></span>|<span data-ttu-id="05eb3-175">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-175">string</span></span>|<span data-ttu-id="05eb3-176">Geçerli kullanıcının soyadı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-177">Şirket adı</span><span class="sxs-lookup"><span data-stu-id="05eb3-177">companyName</span></span>|<span data-ttu-id="05eb3-178">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-178">string</span></span>|<span data-ttu-id="05eb3-179">Geçerli kullanıcının şirket adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="05eb3-180">addresserEmail</span></span>|<span data-ttu-id="05eb3-181">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-181">string</span></span>|<span data-ttu-id="05eb3-182">Geçerli kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="05eb3-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="05eb3-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="05eb3-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="05eb3-184">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-184">string</span></span>|<span data-ttu-id="05eb3-185">Geçerli kullanıcı için analiz görüntülemek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="05eb3-186">Abonelikleri</span><span class="sxs-lookup"><span data-stu-id="05eb3-186">subscriptions</span></span>|<span data-ttu-id="05eb3-187">Koleksiyonu [abonelik](api-management-template-data-model-reference.md#Subscription) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="05eb3-188">Geçerli kullanıcı için abonelikler.</span><span class="sxs-lookup"><span data-stu-id="05eb3-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="05eb3-189">uygulamalar</span><span class="sxs-lookup"><span data-stu-id="05eb3-189">applications</span></span>|<span data-ttu-id="05eb3-190">Koleksiyonu [uygulama](api-management-template-data-model-reference.md#Application) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="05eb3-191">Geçerli kullanıcının uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="05eb3-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-192">changePasswordUrl</span></span>|<span data-ttu-id="05eb3-193">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-193">string</span></span>|<span data-ttu-id="05eb3-194">Geçerli kullanıcının parolasını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="05eb3-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="05eb3-196">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-196">string</span></span>|<span data-ttu-id="05eb3-197">Geçerli kullanıcı için e-posta ve adını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="05eb3-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="05eb3-198">canChangePassword</span></span>|<span data-ttu-id="05eb3-199">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-199">boolean</span></span>|<span data-ttu-id="05eb3-200">Olup geçerli kullanıcı parolalarını değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="05eb3-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="05eb3-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="05eb3-201">isSystemUser</span></span>|<span data-ttu-id="05eb3-202">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-202">boolean</span></span>|<span data-ttu-id="05eb3-203">Geçerli kullanıcının yerleşik bir üyesi olup [grupları](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="05eb3-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="05eb3-204">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="05eb3-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="05eb3-205"><a name="Applications"></a>Uygulamaları</span><span class="sxs-lookup"><span data-stu-id="05eb3-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="05eb3-206">**Uygulamaları** şablon kullanıcı profili sayfasını Geliştirici portalında abonelikleri bölümünü özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="05eb3-207">![Kullanıcı hesabı uygulamalar sayfası](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM kullanıcı hesabı uygulamalar sayfası")</span><span class="sxs-lookup"><span data-stu-id="05eb3-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="05eb3-208">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="05eb3-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="05eb3-209">Denetimler</span><span class="sxs-lookup"><span data-stu-id="05eb3-209">Controls</span></span>  
 <span data-ttu-id="05eb3-210">Bu şablon aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="05eb3-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="05eb3-211">Uygulama eylemleri</span><span class="sxs-lookup"><span data-stu-id="05eb3-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="05eb3-212">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="05eb3-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="05eb3-213">[Profil](#Profile), [uygulamaları](#Applications), ve [abonelikleri](#Subscriptions) şablonları aynı veri modeli paylaşma ve aynı şablon verileri alma.</span><span class="sxs-lookup"><span data-stu-id="05eb3-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="05eb3-214">Özellik</span><span class="sxs-lookup"><span data-stu-id="05eb3-214">Property</span></span>|<span data-ttu-id="05eb3-215">Tür</span><span class="sxs-lookup"><span data-stu-id="05eb3-215">Type</span></span>|<span data-ttu-id="05eb3-216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05eb3-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="05eb3-217">FirstName</span><span class="sxs-lookup"><span data-stu-id="05eb3-217">firstName</span></span>|<span data-ttu-id="05eb3-218">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-218">string</span></span>|<span data-ttu-id="05eb3-219">Geçerli kullanıcının adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-219">First name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-220">Soyadı</span><span class="sxs-lookup"><span data-stu-id="05eb3-220">lastName</span></span>|<span data-ttu-id="05eb3-221">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-221">string</span></span>|<span data-ttu-id="05eb3-222">Geçerli kullanıcının soyadı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-223">Şirket adı</span><span class="sxs-lookup"><span data-stu-id="05eb3-223">companyName</span></span>|<span data-ttu-id="05eb3-224">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-224">string</span></span>|<span data-ttu-id="05eb3-225">Geçerli kullanıcının şirket adı.</span><span class="sxs-lookup"><span data-stu-id="05eb3-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="05eb3-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="05eb3-226">addresserEmail</span></span>|<span data-ttu-id="05eb3-227">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-227">string</span></span>|<span data-ttu-id="05eb3-228">Geçerli kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="05eb3-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="05eb3-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="05eb3-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="05eb3-230">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-230">string</span></span>|<span data-ttu-id="05eb3-231">Geçerli kullanıcı için analiz görüntülemek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="05eb3-232">Abonelikleri</span><span class="sxs-lookup"><span data-stu-id="05eb3-232">subscriptions</span></span>|<span data-ttu-id="05eb3-233">Koleksiyonu [abonelik](api-management-template-data-model-reference.md#Subscription) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="05eb3-234">Geçerli kullanıcı için abonelikler.</span><span class="sxs-lookup"><span data-stu-id="05eb3-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="05eb3-235">uygulamalar</span><span class="sxs-lookup"><span data-stu-id="05eb3-235">applications</span></span>|<span data-ttu-id="05eb3-236">Koleksiyonu [uygulama](api-management-template-data-model-reference.md#Application) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="05eb3-237">Geçerli kullanıcının uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="05eb3-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="05eb3-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-238">changePasswordUrl</span></span>|<span data-ttu-id="05eb3-239">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-239">string</span></span>|<span data-ttu-id="05eb3-240">Geçerli kullanıcının parolasını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="05eb3-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="05eb3-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="05eb3-242">Dize</span><span class="sxs-lookup"><span data-stu-id="05eb3-242">string</span></span>|<span data-ttu-id="05eb3-243">Geçerli kullanıcı için e-posta ve adını değiştirmek için göreli URL'si.</span><span class="sxs-lookup"><span data-stu-id="05eb3-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="05eb3-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="05eb3-244">canChangePassword</span></span>|<span data-ttu-id="05eb3-245">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-245">boolean</span></span>|<span data-ttu-id="05eb3-246">Olup geçerli kullanıcı parolalarını değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="05eb3-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="05eb3-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="05eb3-247">isSystemUser</span></span>|<span data-ttu-id="05eb3-248">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="05eb3-248">boolean</span></span>|<span data-ttu-id="05eb3-249">Geçerli kullanıcının yerleşik bir üyesi olup [grupları](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="05eb3-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="05eb3-250">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="05eb3-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="05eb3-251"><a name="UpdateAccountInfo"></a>Hesap bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="05eb3-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="05eb3-252">**Uodate hesap bilgisi** şablonu özelleştirmenizi sağlar **güncelleştirme hesap bilgileri** Geliştirici portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="05eb3-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="05eb3-253">![Kullanıcı hesabı bilgileri sayfasında Geliştirici Portalı şablonlarını](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM kullanıcı hesabı bilgileri sayfasında Geliştirici Portalı şablonları")</span><span class="sxs-lookup"><span data-stu-id="05eb3-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="05eb3-254">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="05eb3-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="05eb3-255">Denetimler</span><span class="sxs-lookup"><span data-stu-id="05eb3-255">Controls</span></span>  
 <span data-ttu-id="05eb3-256">Bu şablon herhangi kullanamazsınız [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="05eb3-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="05eb3-257">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="05eb3-257">Data model</span></span>  
 <span data-ttu-id="05eb3-258">[Kullanıcı hesabı bilgileri](api-management-template-data-model-reference.md#UserAccountInfo) varlık.</span><span class="sxs-lookup"><span data-stu-id="05eb3-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="05eb3-259">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="05eb3-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="05eb3-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05eb3-260">Next steps</span></span>
<span data-ttu-id="05eb3-261">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="05eb3-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>