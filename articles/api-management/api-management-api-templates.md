---
title: "Azure API Management'te aaaAPI şablonları | Microsoft Docs"
description: "Nasıl toocustomize hello hello Azure API Management'ta Geliştirici portalını hello API sayfalarında içeriğini öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3642fd09-ba98-4358-93a6-c48ab0500431
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: fdfa76167cfaf3b23b22d6321904f34da077fecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-templates-in-azure-api-management"></a><span data-ttu-id="14677-103">Azure API Management'te API şablonları</span><span class="sxs-lookup"><span data-stu-id="14677-103">API templates in Azure API Management</span></span>
<span data-ttu-id="14677-104">Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="14677-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="14677-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="14677-106">Bu bölümdeki Hello şablonları hello Geliştirici Portalı'nda toocustomize hello hello API sayfaların içeriğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-106">hello templates in this section allow you toocustomize hello content of hello API pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="14677-107">API listesi</span><span class="sxs-lookup"><span data-stu-id="14677-107">API list</span></span>](#APIList)  
-   [<span data-ttu-id="14677-108">İşlem</span><span class="sxs-lookup"><span data-stu-id="14677-108">Operation</span></span>](#Product)  
-   [<span data-ttu-id="14677-109">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="14677-109">Code samples</span></span>](#CodeSamples)  
    -   [<span data-ttu-id="14677-110">Curl</span><span class="sxs-lookup"><span data-stu-id="14677-110">Curl</span></span>](#Curl)  
    -   [<span data-ttu-id="14677-111">C#</span><span class="sxs-lookup"><span data-stu-id="14677-111">C#</span></span>](#CSharp)  
    -   [<span data-ttu-id="14677-112">Java</span><span class="sxs-lookup"><span data-stu-id="14677-112">Java</span></span>](#Stub)  
    -   [<span data-ttu-id="14677-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="14677-113">JavaScript</span></span>](#JavaScript)  
    -   [<span data-ttu-id="14677-114">Objective C</span><span class="sxs-lookup"><span data-stu-id="14677-114">Objective C</span></span>](#ObjectiveC)  
    -   [<span data-ttu-id="14677-115">PHP</span><span class="sxs-lookup"><span data-stu-id="14677-115">PHP</span></span>](#PHP)  
    -   [<span data-ttu-id="14677-116">Python</span><span class="sxs-lookup"><span data-stu-id="14677-116">Python</span></span>](#Python)  
    -   [<span data-ttu-id="14677-117">Ruby</span><span class="sxs-lookup"><span data-stu-id="14677-117">Ruby</span></span>](#Ruby)  

> [!NOTE]
>  <span data-ttu-id="14677-118">Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="14677-118">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="14677-119">İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14677-119">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="14677-120">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="14677-120">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="14677-121"><a name="APIList"></a>API listesi</span><span class="sxs-lookup"><span data-stu-id="14677-121"><a name="APIList"></a> API list</span></span>  
 <span data-ttu-id="14677-122">Merhaba **API listesi** şablonu verir hello API listesi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="14677-122">hello **API list** template allows you toocustomize hello body of hello API list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="14677-123">![Geliştirici Portalı API listesi](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM Geliştirici Portalı şablonları API listesi")</span><span class="sxs-lookup"><span data-stu-id="14677-123">![Developer Portal API List](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM Developer Portal Templates API List")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="14677-124">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-124">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ApisStrings|PageTitleApis" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if apis.size > 0 %}  
    <ol class="list-unstyled">  
    {% for api in apis %}  
        <li>  
        <h3>  
          <a href="/docs/services/{{api.id}}">{{api.name}}</a>  
        </h3>  
       {{api.description}}  
      </li>  
    {% endfor %}  
    </ol>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="14677-125">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-125">Controls</span></span>  
 <span data-ttu-id="14677-126">Merhaba `API list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-126">hello `API list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="14677-127">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="14677-127">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="14677-128">arama denetimi</span><span class="sxs-lookup"><span data-stu-id="14677-128">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="14677-129">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-129">Data model</span></span>  
  
|<span data-ttu-id="14677-130">Özellik</span><span class="sxs-lookup"><span data-stu-id="14677-130">Property</span></span>|<span data-ttu-id="14677-131">Tür</span><span class="sxs-lookup"><span data-stu-id="14677-131">Type</span></span>|<span data-ttu-id="14677-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14677-132">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="14677-133">API'leri</span><span class="sxs-lookup"><span data-stu-id="14677-133">apis</span></span>|<span data-ttu-id="14677-134">Koleksiyonu [API özeti](api-management-template-data-model-reference.md#APISummary) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="14677-134">Collection of [API summary](api-management-template-data-model-reference.md#APISummary) entities.</span></span>|<span data-ttu-id="14677-135">Merhaba API'leri görünür toohello geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="14677-135">hello APIs visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="14677-136">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-136">Sample template data</span></span>  
  
```json  
{  
    "apis": [  
        {  
            "id": "570275f1b16653124c8f9ba3",  
            "name": "Basic Calculator",  
            "description": "Arithmetics is just a call away!"  
        },  
        {  
            "id": "57026e30de15d80041040001",  
            "name": "Echo API",  
            "description": null  
        }  
    ],  
    "pageTitle": "APIs"  
}  
```  
  
##  <span data-ttu-id="14677-137"><a name="Product"></a>İşlemi</span><span class="sxs-lookup"><span data-stu-id="14677-137"><a name="Product"></a> Operation</span></span>  
 <span data-ttu-id="14677-138">Merhaba **işlemi** şablonu verir hello işlemi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="14677-138">hello **Operation** template allows you toocustomize hello body of hello operation page in hello developer portal.</span></span>  
  
 <span data-ttu-id="14677-139">![Geliştirici Portalı işlemi sayfa](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM Geliştirici Portalı şablonlarını işlemi")</span><span class="sxs-lookup"><span data-stu-id="14677-139">![Developer Portal Operation page](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM Developer Portal templates Operation page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="14677-140">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-140">Default template</span></span>  
  
```xml  
<h2>{{api.name}}</h2>  
<p>{{api.description }}</p>  
  
<div class="panel">  
    <h3>{{operation.name}}</h3>  
    <p>{{operation.description }}</p>  
    <a class="btn btn-primary" href="{{consoleUrl}}" id="btnOpenConsole" role="button">  
        Try it  
    </a>  
</div>  
  
<h4>{% localized "Documentation|SectionHeadingRequestUrl" %}</h4>  
<div class="panel">  
    <div class="panel-body">  
        <label>{{ sampleUrl | escape }}</label>  
    </div>  
</div>  
  
{% if operation.request %}  
    {% if operation.request.parameters.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestParameters" %}</h4>  
  
        <div class="panel">  
            {% for parameter in operation.request.parameters %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{parameter.name}}</label>  
                        {% unless parameter.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{parameter.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{parameter.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.headers.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestHeaders" %}</h4>  
        <div class="panel">  
            {% for header in operation.request.headers %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{header.name}}</label>  
                        {%unless header.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{header.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{header.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.description or operation.request.representations.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestBody" %}</h4>  
        <div class="panel">  
            {% if operation.request.description %}  
                <p>{{operation.request.description }}</p>     
            {% endif %}  
  
            {% if operation.request.representations.size > 0 %}  
                <div role="tabpanel">  
                    <ul class="nav nav-tabs" role="tablist">  
                        {% for representation in operation.request.representations %}  
                            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                <a href="#requesttab{{forloop.index}}" role="tab" data-toggle="tab">  
                                    {{representation.contentType}}  
                                </a>  
                            </li>  
                        {% endfor %}  
                    </ul>  
                    <div class="tab-content tab-content-boxed">  
                        {% for representation in operation.request.representations %}  
                            <div id="requesttab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                {% if representation.sample or representation.schema %}   
                                <div role="tabpanel">  
                                    {% if representation.sample and representation.schema %}   
                                    <ul class="nav nav-tabs-borderless" role="tablist">  
                                        <li role="presentation" class="active">  
                                            <a href="#requesttab{{forloop.index}}sample" role="tab" data-toggle="tab">Sample</a>  
                                        </li>  
                                        <li role="presentation">  
                                            <a href="#requesttab{{forloop.index}}schema" role="tab" data-toggle="tab">Schema</a>  
                                        </li>  
                                    </ul>  
                                    {% endif %}  
  
                                    <div class="tab-content">  
                                        {% if representation.sample %}  
                                        <div id="requesttab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
  
                                        {% if representation.schema %}  
                                        <div id="requesttab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
                                    </div>  
                                </div>  
                                {% endif %}  
                            </div>  
                        {% endfor %}  
                    </div>  
                </div>  
            {% endif %}  
  
            <div class="clearfix"></div>  
        </div>  
    {% endif %}  
{% endif %}  
  
{% if operation.responses.size > 0 %}  
    {% for response in operation.responses %}  
        {% if response.description or response.representations.size > 0 %}  
            <h4>{% localized "Documentation|SectionHeadingResponse" %} {{response.statusCode}}</h4>  
  
            <div class="panel">  
                {% if response.description %}  
                    <p>{{ response.description }}</p>  
                {% endif %}  
  
                {% if response.representations.size > 0 %}  
                    <div role="tabpanel">  
                        <ul class="nav nav-tabs" role="tablist">  
                            {% for representation in response.representations %}  
                                <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                    <a href="#response{{response.statusCode}}tab{{forloop.index}}" role="tab" data-toggle="tab">  
                                        {{representation.contentType}}  
                                    </a>  
                                </li>  
                            {% endfor %}  
                        </ul>  
                        <div class="tab-content tab-content-boxed">  
                            {% for representation in response.representations %}  
                                <div id="response{{response.statusCode}}tab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                    {% if representation.sample or representation.schema %}  
                                    <div role="tabpanel">  
  
                                        {% if representation.sample and representation.schema %}  
                                        <ul class="nav nav-tabs-borderless" role="tablist">  
                                            <li role="presentation" class="active">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}sample" role="tab" data-toggle="tab">  
                                                    Sample  
                                                </a>  
                                            </li>  
                                            <li role="presentation">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}schema" role="tab" data-toggle="tab">  
                                                    Schema  
                                                </a>  
                                            </li>  
                                        </ul>  
                                        {% endif %}  
  
                                        <div class="tab-content">  
                                            {% if representation.sample %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
  
                                            {% if representation.schema %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
                                        </div>  
                                    </div>  
                                    {% endif %}  
                                </div>  
                            {% endfor %}  
                        </div>  
                    </div>  
                {% endif %}  
  
                <div class="clearfix"></div>  
            </div>  
  
        {% endif %}  
    {% endfor %}  
{% endif %}  
  
<h4>{% localized "Documentation|SectionHeadingCodeSamples" %}</h4>  
<div role="tabpanel">  
    <ul class="nav nav-tabs" role="tablist">  
        {% for sample in samples %}  
            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                <a href="#{{sample.brush}}" aria-controls="{{sample.brush}}" role="tab" data-toggle="tab">  
                    {{sample.title}}  
                </a>  
            </li>  
        {% endfor %}  
    </ul>  
    <div class="tab-content tab-content-boxed" title="{% localized "Documentation|TooltipTextDoubleClickToSelectAll=""" %}">  
        {% for sample in samples %}  
            <div role="tabpanel" class="tab-pane tab-content-boxed {% if forloop.first %} active{% endif %} snippet snippet-resizable" id="{{sample.brush}}" >  
                <pre><code class="{{sample.brush}}">{% partial sample.template for sample in samples %}</code></pre>  
            </div>  
        {% endfor %}  
    </div>  
    <div class="clearfix"></div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="14677-141">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-141">Controls</span></span>  
 <span data-ttu-id="14677-142">Merhaba `Operation` şablon herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-142">hello `Operation` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="14677-143">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-143">Data model</span></span>  
  
|<span data-ttu-id="14677-144">Özellik</span><span class="sxs-lookup"><span data-stu-id="14677-144">Property</span></span>|<span data-ttu-id="14677-145">Tür</span><span class="sxs-lookup"><span data-stu-id="14677-145">Type</span></span>|<span data-ttu-id="14677-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14677-146">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="14677-147">ApiId</span><span class="sxs-lookup"><span data-stu-id="14677-147">apiId</span></span>|<span data-ttu-id="14677-148">Dize</span><span class="sxs-lookup"><span data-stu-id="14677-148">string</span></span>|<span data-ttu-id="14677-149">Merhaba geçerli API Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="14677-149">hello id of hello current API.</span></span>|  
|<span data-ttu-id="14677-150">apiName</span><span class="sxs-lookup"><span data-stu-id="14677-150">apiName</span></span>|<span data-ttu-id="14677-151">Dize</span><span class="sxs-lookup"><span data-stu-id="14677-151">string</span></span>|<span data-ttu-id="14677-152">Merhaba API Hello adı.</span><span class="sxs-lookup"><span data-stu-id="14677-152">hello name of hello API.</span></span>|  
|<span data-ttu-id="14677-153">apiDescription</span><span class="sxs-lookup"><span data-stu-id="14677-153">apiDescription</span></span>|<span data-ttu-id="14677-154">Dize</span><span class="sxs-lookup"><span data-stu-id="14677-154">string</span></span>|<span data-ttu-id="14677-155">Merhaba API açıklaması.</span><span class="sxs-lookup"><span data-stu-id="14677-155">A description of hello API.</span></span>|  
|<span data-ttu-id="14677-156">api</span><span class="sxs-lookup"><span data-stu-id="14677-156">api</span></span>|<span data-ttu-id="14677-157">[API özeti](api-management-template-data-model-reference.md#APISummary) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-157">[API summary](api-management-template-data-model-reference.md#APISummary) entity.</span></span>|<span data-ttu-id="14677-158">Merhaba geçerli API.</span><span class="sxs-lookup"><span data-stu-id="14677-158">hello current API.</span></span>|  
|<span data-ttu-id="14677-159">işlemi</span><span class="sxs-lookup"><span data-stu-id="14677-159">operation</span></span>|[<span data-ttu-id="14677-160">İşlem</span><span class="sxs-lookup"><span data-stu-id="14677-160">Operation</span></span>](api-management-template-data-model-reference.md#Operation)|<span data-ttu-id="14677-161">şu anda görüntülenen hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="14677-161">hello currently displayed operation.</span></span>|  
|<span data-ttu-id="14677-162">sampleUrl</span><span class="sxs-lookup"><span data-stu-id="14677-162">sampleUrl</span></span>|<span data-ttu-id="14677-163">Dize</span><span class="sxs-lookup"><span data-stu-id="14677-163">string</span></span>|<span data-ttu-id="14677-164">Merhaba geçerli işlem için Hello URL.</span><span class="sxs-lookup"><span data-stu-id="14677-164">hello URL for hello current operation.</span></span>|  
|<span data-ttu-id="14677-165">operationMenu</span><span class="sxs-lookup"><span data-stu-id="14677-165">operationMenu</span></span>|[<span data-ttu-id="14677-166">İşlemi menüsü</span><span class="sxs-lookup"><span data-stu-id="14677-166">Operation menu</span></span>](api-management-template-data-model-reference.md#Menu)|<span data-ttu-id="14677-167">Bu API işlemlerinin menüsü.</span><span class="sxs-lookup"><span data-stu-id="14677-167">A menu of operations for this API.</span></span>|  
|<span data-ttu-id="14677-168">consoleUrl</span><span class="sxs-lookup"><span data-stu-id="14677-168">consoleUrl</span></span>|<span data-ttu-id="14677-169">URI</span><span class="sxs-lookup"><span data-stu-id="14677-169">URI</span></span>|<span data-ttu-id="14677-170">Merhaba URI hello **deneyin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="14677-170">hello URI for hello **Try it** button.</span></span>|  
|<span data-ttu-id="14677-171">Örnekleri</span><span class="sxs-lookup"><span data-stu-id="14677-171">samples</span></span>|<span data-ttu-id="14677-172">Koleksiyonu [kod örneği](api-management-template-data-model-reference.md#Sample) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="14677-172">Collection of [Code sample](api-management-template-data-model-reference.md#Sample) entities.</span></span>|<span data-ttu-id="14677-173">Merhaba kod örnekleri hello geçerli işlem için...</span><span class="sxs-lookup"><span data-stu-id="14677-173">hello code samples for hello current operation..</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="14677-174">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-174">Sample template data</span></span>  
  
```json  
{  
    "apiId": "570275f1b16653124c8f9ba3",  
    "apiName": "Basic Calculator",  
    "apiDescription": "Arithmetics is just a call away!",  
    "api": {  
        "id": "570275f1b16653124c8f9ba3",  
        "name": "Basic Calculator",  
        "description": "Arithmetics is just a call away!"  
    },  
    "operation": {  
        "id": "570275f2b1665305c811cf49",  
        "name": "Add two integers",  
        "description": "Produces a sum of two numbers.",  
        "scheme": "https",  
        "uriTemplate": "calc/add?a={a}&b={b}",  
        "host": "sdcontoso5.azure-api.net",  
        "httpMethod": "GET",  
        "request": {  
            "description": null,  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": [  
                {  
                    "name": "a",  
                    "description": "First operand. Default value is <code>51</code>.",  
                    "value": "51",  
                    "options": [  
                        "51"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                },  
                {  
                    "name": "b",  
                    "description": "Second operand. Default value is <code>49</code>.",  
                    "value": "49",  
                    "options": [  
                        "49"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                }  
            ],  
            "representations": []  
        },  
        "responses": []  
    },  
    "sampleUrl": "https://sdcontoso5.azure-api.net/calc/add?a={a}&b={b}",  
    "operationMenu": {  
        "ApiId": "570275f1b16653124c8f9ba3",  
        "CurrentOperationId": "570275f2b1665305c811cf49",  
        "Action": "Operation",  
        "MenuItems": [  
            {  
                "Id": "570275f2b1665305c811cf49",  
                "Title": "Add two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4c",  
                "Title": "Divide two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4b",  
                "Title": "Multiply two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4a",  
                "Title": "Subtract two integers",  
                "HttpMethod": "GET"  
            }  
        ]  
    },  
    "consoleUrl": "/docs/services/570275f1b16653124c8f9ba3/operations/570275f2b1665305c811cf49/console",  
    "samples": [  
        {  
            "title": "Curl",  
            "snippet": null,  
            "brush": "plain",  
            "template": "DocumentationSamplesCurl",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "C#",  
            "snippet": null,  
            "brush": "csharp",  
            "template": "DocumentationSamplesCsharp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Java",  
            "snippet": null,  
            "brush": "java",  
            "template": "DocumentationSamplesJava",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "JavaScript",  
            "snippet": null,  
            "brush": "xml",  
            "template": "DocumentationSamplesJs",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "ObjC",  
            "snippet": null,  
            "brush": "objc",  
            "template": "DocumentationSamplesObjc",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "PHP",  
            "snippet": null,  
            "brush": "php",  
            "template": "DocumentationSamplesPhp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Python",  
            "snippet": null,  
            "brush": "python",  
            "template": "DocumentationSamplesPython",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Ruby",  
            "snippet": null,  
            "brush": "ruby",  
            "template": "DocumentationSamplesRuby",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="14677-175"><a name="CodeSamples"></a>Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="14677-175"><a name="CodeSamples"></a> Code samples</span></span>  
 <span data-ttu-id="14677-176">Merhaba aşağıdaki şablonlardan toocustomize hello gövde hello tek tek kod örnekleri hello işlemi sayfasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-176">hello following templates allow you toocustomize hello body of hello individual code samples on hello operation page.</span></span>  
  
 <span data-ttu-id="14677-177">![Geliştirici Portalı şablonları kod örnekleri](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM Geliştirici Portalı şablonları kod örnekleri")</span><span class="sxs-lookup"><span data-stu-id="14677-177">![Developer Portal Templates Code samples](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM Developer Portal Templates Code samples")</span></span>  
  
-   [<span data-ttu-id="14677-178">Curl</span><span class="sxs-lookup"><span data-stu-id="14677-178">Curl</span></span>](#Curl)  
  
-   [<span data-ttu-id="14677-179">C#</span><span class="sxs-lookup"><span data-stu-id="14677-179">C#</span></span>](#CSharp)  
  
-   [<span data-ttu-id="14677-180">Java</span><span class="sxs-lookup"><span data-stu-id="14677-180">Java</span></span>](#Stub)  
  
-   [<span data-ttu-id="14677-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="14677-181">JavaScript</span></span>](#JavaScript)  
  
-   [<span data-ttu-id="14677-182">Objective C</span><span class="sxs-lookup"><span data-stu-id="14677-182">Objective C</span></span>](#ObjectiveC)  
  
-   [<span data-ttu-id="14677-183">PHP</span><span class="sxs-lookup"><span data-stu-id="14677-183">PHP</span></span>](#PHP)  
  
-   [<span data-ttu-id="14677-184">Python</span><span class="sxs-lookup"><span data-stu-id="14677-184">Python</span></span>](#Python)  
  
-   [<span data-ttu-id="14677-185">Ruby</span><span class="sxs-lookup"><span data-stu-id="14677-185">Ruby</span></span>](#Ruby)  
  
###  <span data-ttu-id="14677-186"><a name="Curl"></a>Curl</span><span class="sxs-lookup"><span data-stu-id="14677-186"><a name="Curl"></a> Curl</span></span>  
 <span data-ttu-id="14677-187">Merhaba **DocumentationSamplesCurl** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-187">hello **DocumentationSamplesCurl** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-188">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-188">Default template</span></span>  
  
```xml  
@ECHO OFF  
  
curl -v -X {{method}} "{{scheme}}://{{host}}{{path}}{{query | escape }}"  
{% for header in headers -%}  
-H "{{ header.name }}: {{ header.value }}"  
{% endfor -%}  
{% if body -%}   
--data-ascii "{{ body | replace:'"','^"' }}"   
{% endif -%}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-189">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-189">Controls</span></span>  
 <span data-ttu-id="14677-190">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-190">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-191">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-191">Data model</span></span>  
 <span data-ttu-id="14677-192">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-192">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-193">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-193">Sample template data</span></span>  
  
```json  
{  
    "title": "Curl",  
    "snippet": null,  
    "brush": "plain",  
    "template": "DocumentationSamplesCurl",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-194"><a name="CSharp"></a>C#</span><span class="sxs-lookup"><span data-stu-id="14677-194"><a name="CSharp"></a> C#</span></span>  
 <span data-ttu-id="14677-195">Merhaba **DocumentationSamplesCsharp** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-195">hello **DocumentationSamplesCsharp** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-196">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-196">Default template</span></span>  
  
```xml  
using System;  
using System.Net.Http.Headers;  
using System.Text;  
using System.Net.Http;  
using System.Web;  
  
namespace CSHttpClientSample  
{  
    static class Program  
    {  
        static void Main()  
        {  
            MakeRequest();  
            Console.WriteLine("Hit ENTER tooexit...");  
            Console.ReadLine();  
        }  
  
        static async void MakeRequest()  
        {  
            var client = new HttpClient();  
            var queryString = HttpUtility.ParseQueryString(string.Empty);  
  
{% if headers.size > 0 -%}  
            // Request headers  
{% for header in headers -%}  
{% case header.Name -%}  
{% when "Accept"%}  
            client.DefaultRequestHeaders.Accept.Add(MediaTypeWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Charset" -%}  
            client.DefaultRequestHeaders.AcceptCharset.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Encoding" -%}  
            client.DefaultRequestHeaders.AcceptEncoding.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Language" -%}  
            client.DefaultRequestHeaders.AcceptLanguage.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Cache-Control" -%}  
            client.DefaultRequestHeaders.CacheControl = CacheControlHeaderValue.Parse("{{header.value}}");  
{% when "Connection" -%}  
            client.DefaultRequestHeaders.Connection.Add("{{header.value}}");  
{% when "Date" -%}  
            client.DefaultRequestHeaders.Date = DateTimeOffset.Parse("{{header.value}}");  
{% when "Expect" -%}  
            client.DefaultRequestHeaders.Expect.Add(NameValueWithParametersHeaderValue.Parse("{{header.value}}"));  
{% when "If-Match" -%}  
            client.DefaultRequestHeaders.IfMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Modified-Since" -%}  
            client.DefaultRequestHeaders.IfModifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "If-None-Match" -%}  
            client.DefaultRequestHeaders.IfNoneMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Range" -%}  
            client.DefaultRequestHeaders.IfRange = RangeConditionHeaderValue.Parse("{{header.value}}");  
{% when "If-Unmodified-Since" -%}  
            client.DefaultRequestHeaders.IfUnmodifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "Max-Forwards" -%}  
            client.DefaultRequestHeaders.MaxForwards = int.Parse("{{header.value}}");  
{% when "Pragma" -%}  
            client.DefaultRequestHeaders.Pragma.Add(NameValueHeaderValue.Parse("{{header.value}}"));  
{% when "Range" -%}  
            client.DefaultRequestHeaders.Range = RangeHeaderValue.Parse("{{header.value}}");  
{% when "Referer" -%}  
            client.DefaultRequestHeaders.Referrer = new Uri("{{header.value}}");  
{% when "TE" -%}  
            client.DefaultRequestHeaders.TE.Add(TransferCodingWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Transfer-Encoding" -%}  
            client.DefaultRequestHeaders.TransferEncoding.Add(TransferCodingHeaderValue.Parse("{{header.value}}"));  
{% when "Upgrade" -%}  
            client.DefaultRequestHeaders.Upgrade.Add(ProductHeaderValue.Parse("{{header.value}}"));  
{% when "User-Agent" -%}  
            client.DefaultRequestHeaders.UserAgent.Add(ProductInfoHeaderValue.Parse("{{header.value}}"));  
{% when "Via" -%}                
            client.DefaultRequestHeaders.Via.Add(ViaHeaderValue.Parse("{{header.value}}"));  
{% when "Warning" -%}  
            client.DefaultRequestHeaders.Warning.Add(WarningHeaderValue.Parse("{{header.value}}"));  
{% when "Content-Type" -%}  
{% else -%}  
            client.DefaultRequestHeaders.Add("{{header.Name}}", "{{header.value}}");  
{% endcase -%}  
{% endfor -%}  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            queryString["{{parameter.Name}}"] = "{{parameter.Value}}";  
{% endfor -%}  
{% endif -%}  
            var uri = "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + queryString;  
  
{% case method -%}  
  
{% when "POST" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
               content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
               response = await client.PostAsync(uri, content);  
            }  
  
{% when "GET" -%}  
            var response = await client.GetAsync(uri);  
{% when "DELETE" -%}  
            var response = await client.DeleteAsync(uri);  
{% when "PUT" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
                content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
                response = await client.PutAsync(uri, content);  
            }  
{% when "HEAD" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Head, uri));  
{% when "OPTIONS" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Options, uri));  
{% when "TRACE" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Trace, uri));  
  
            if (response.Content != null)  
            {  
                var responseString = await response.Content.ReadAsStringAsync();  
                Console.WriteLine(responseString);      
            }  
{% endcase -%}  
        }  
    }  
}     
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-197">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-197">Controls</span></span>  
 <span data-ttu-id="14677-198">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-198">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-199">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-199">Data model</span></span>  
 <span data-ttu-id="14677-200">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-200">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-201">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-201">Sample template data</span></span>  
  
```json  
{  
    "title": "C#",  
    "snippet": null,  
    "brush": "csharp",  
    "template": "DocumentationSamplesCsharp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-202"><a name="Stub"></a>Java</span><span class="sxs-lookup"><span data-stu-id="14677-202"><a name="Stub"></a> Java</span></span>  
 <span data-ttu-id="14677-203">Merhaba **DocumentationSamplesJava** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-203">hello **DocumentationSamplesJava** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-204">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-204">Default template</span></span>  
  
```xml  
// // This sample uses hello Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
import java.net.URI;  
import org.apache.http.HttpEntity;  
import org.apache.http.HttpResponse;  
import org.apache.http.client.HttpClient;  
import org.apache.http.client.methods.HttpGet;  
import org.apache.http.client.utils.URIBuilder;  
import org.apache.http.impl.client.HttpClients;  
import org.apache.http.util.EntityUtils;  
  
public class JavaSample   
{  
    public static void main(String[] args)   
    {  
        HttpClient httpclient = HttpClients.createDefault();  
  
        try  
        {  
            URIBuilder builder = new URIBuilder("{{scheme}}://{{host}}{{path}}");  
  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
            builder.setParameter("{{parameter.name}}", "{{parameter.value}}");  
{% endfor -%}  
{% endif -%}  
  
            URI uri = builder.build();  
            Http{{ method | downcase | capitalize }} request = new Http{{ method | downcase | capitalize }}(uri);  
{% for header in headers -%}  
            request.setHeader("{{header.Name}}", "{{header.value}}");  
{% endfor %}  
  
{% if body -%}  
            // Request body  
            StringEntity reqEntity = new StringEntity("{{ body | replace:'"','\"' }}");  
            request.setEntity(reqEntity);  
{% endif -%}  
  
            HttpResponse response = httpclient.execute(request);  
            HttpEntity entity = response.getEntity();  
  
            if (entity != null)   
            {  
                System.out.println(EntityUtils.toString(entity));  
            }  
        }  
        catch (Exception e)  
        {  
            System.out.println(e.getMessage());  
        }  
    }  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-205">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-205">Controls</span></span>  
 <span data-ttu-id="14677-206">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-206">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-207">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-207">Data model</span></span>  
 <span data-ttu-id="14677-208">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-208">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-209">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-209">Sample template data</span></span>  
  
```json  
{  
    "title": "Java",  
    "snippet": null,  
    "brush": "java",  
    "template": "DocumentationSamplesJava",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-210"><a name="JavaScript"></a>JavaScript</span><span class="sxs-lookup"><span data-stu-id="14677-210"><a name="JavaScript"></a> JavaScript</span></span>  
 <span data-ttu-id="14677-211">Merhaba **DocumentationSamplesJs** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-211">hello **DocumentationSamplesJs** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-212">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-212">Default template</span></span>  
  
```xml  
<!DOCTYPE html>  
<html>  
<head>  
    <title>JSSample</title>  
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>  
</head>  
<body>  
  
<script type="text/javascript">  
    $(function() {  
        var params = {  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            "{{parameter.name}}": "{{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
        };  
  
        $.ajax({  
            url: "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + $.param(params),  
{% if headers.size > 0 -%}  
            beforeSend: function(xhrObj){  
                // Request headers  
{% for header in headers -%}  
                xhrObj.setRequestHeader("{{header.name}}","{{header.value}}");  
{% endfor -%}  
            },  
{% endif -%}  
            type: "{{method}}",  
{% if body -%}  
            // Request body  
            data: "{{ body | replace:'"','\"' }}",  
{% endif -%}  
        })  
        .done(function(data) {  
            alert("success");  
        })  
        .fail(function() {  
            alert("error");  
        });  
    });  
</script>  
</body>  
</html>  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-213">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-213">Controls</span></span>  
 <span data-ttu-id="14677-214">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-214">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-215">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-215">Data model</span></span>  
 <span data-ttu-id="14677-216">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-216">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-217">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-217">Sample template data</span></span>  
  
```json  
{  
    "title": "JavaScript",  
    "snippet": null,  
    "brush": "xml",  
    "template": "DocumentationSamplesJs",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-218"><a name="ObjectiveC"></a>Objective C</span><span class="sxs-lookup"><span data-stu-id="14677-218"><a name="ObjectiveC"></a> Objective C</span></span>  
 <span data-ttu-id="14677-219">Merhaba **DocumentationSamplesObjc** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-219">hello **DocumentationSamplesObjc** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-220">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-220">Default template</span></span>  
  
```xml  
#import <Foundation/Foundation.h>  
  
int main(int argc, const char * argv[])  
{  
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];  
  
    NSString* path = @"{{scheme}}://{{host}}{{path}}";  
    NSArray* array = @[  
                         // Request parameters  
                         @"entities=true",  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
                         @"{{parameter.name}}={{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
                      ];  
  
    NSString* string = [array componentsJoinedByString:@"&"];  
    path = [path stringByAppendingFormat:@"?%@", string];  
  
    NSLog(@"%@", path);  
  
    NSMutableURLRequest* _request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:path]];  
    [_request setHTTPMethod:@"{{method}}"];  
{% if headers.size > 0 -%}  
    // Request headers  
{% for header in headers -%}  
    [_request setValue:@"{{header.value}}" forHTTPHeaderField:@"{{header.name}}"];  
{% endfor -%}  
{% endif -%}  
{% if body -%}  
    // Request body  
    [_request setHTTPBody:[@"{{ body | replace:'"','\"' }}" dataUsingEncoding:NSUTF8StringEncoding]];  
{% endif -%}  
  
    NSURLResponse *response = nil;  
    NSError *error = nil;  
    NSData* _connectionData = [NSURLConnection sendSynchronousRequest:_request returningResponse:&response error:&error];  
  
    if (nil != error)  
    {  
        NSLog(@"Error: %@", error);  
    }  
    else  
    {  
        NSError* error = nil;  
        NSMutableDictionary* json = nil;  
        NSString* dataString = [[NSString alloc] initWithData:_connectionData encoding:NSUTF8StringEncoding];  
        NSLog(@"%@", dataString);  
  
        if (nil != _connectionData)  
        {  
            json = [NSJSONSerialization JSONObjectWithData:_connectionData options:NSJSONReadingMutableContainers error:&error];  
        }  
  
        if (error || !json)  
        {  
            NSLog(@"Could not parse loaded json with error:%@", error);  
        }  
  
        NSLog(@"%@", json);  
        _connectionData = nil;  
    }  
  
    [pool drain];  
  
    return 0;  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-221">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-221">Controls</span></span>  
 <span data-ttu-id="14677-222">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-222">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-223">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-223">Data model</span></span>  
 <span data-ttu-id="14677-224">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-224">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-225">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-225">Sample template data</span></span>  
  
```json  
{  
    "title": "ObjC",  
    "snippet": null,  
    "brush": "objc",  
    "template": "DocumentationSamplesObjc",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-226"><a name="PHP"></a>PHP</span><span class="sxs-lookup"><span data-stu-id="14677-226"><a name="PHP"></a> PHP</span></span>  
 <span data-ttu-id="14677-227">Merhaba **DocumentationSamplesPhp** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-227">hello **DocumentationSamplesPhp** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-228">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-228">Default template</span></span>  
  
```xml  
<?php  
// This sample uses hello Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
require_once 'HTTP/Request2.php';  
  
$request = new Http_Request2('{{scheme}}://{{host}}{{path}}');  
$url = $request->getUrl();  
  
{% if headers.size > 0 -%}  
$headers = array(  
    // Request headers  
{% for header in headers -%}  
    '{{header.name}}' => '{{header.value}}',  
{% endfor -%}  
);  
  
$request->setHeader($headers);  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
$parameters = array(  
    // Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}',  
{% endfor -%}  
);  
  
$url->setQueryVariables($parameters);  
{% endif -%}  
  
$request->setMethod(HTTP_Request2::METHOD_{{method}});  
  
{% if body -%}  
// Request body  
$request->setBody("{{ body | replace:'"','\"' }}");  
{% endif -%}  
  
try  
{  
    $response = $request->send();  
    echo $response->getBody();  
}  
catch (HttpException $ex)  
{  
    echo $ex;  
}  
  
?>  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-229">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-229">Controls</span></span>  
 <span data-ttu-id="14677-230">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-230">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-231">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-231">Data model</span></span>  
 <span data-ttu-id="14677-232">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-232">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-233">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-233">Sample template data</span></span>  
  
```json  
{  
    "title": "PHP",  
    "snippet": null,  
    "brush": "php",  
    "template": "DocumentationSamplesPhp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-234"><a name="Python"></a>Python</span><span class="sxs-lookup"><span data-stu-id="14677-234"><a name="Python"></a> Python</span></span>  
 <span data-ttu-id="14677-235">Merhaba **DocumentationSamplesPython** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-235">hello **DocumentationSamplesPython** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-236">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-236">Default template</span></span>  
  
```xml  
########### Python 2.7 #############  
import httplib, urllib, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = httplib.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = httplib.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
  
########### Python 3.2 #############  
import http.client, urllib.request, urllib.parse, urllib.error, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.parse.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = http.client.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = http.client.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-237">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-237">Controls</span></span>  
 <span data-ttu-id="14677-238">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-238">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-239">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-239">Data model</span></span>  
 <span data-ttu-id="14677-240">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-240">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-241">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-241">Sample template data</span></span>  
  
```json  
{  
    "title": "Python",  
    "snippet": null,  
    "brush": "python",  
    "template": "DocumentationSamplesPython",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="14677-242"><a name="Ruby"></a>Ruby</span><span class="sxs-lookup"><span data-stu-id="14677-242"><a name="Ruby"></a> Ruby</span></span>  
 <span data-ttu-id="14677-243">Merhaba **DocumentationSamplesRuby** şablon hello işlemi sayfasının hello kod örnekleri bölümünde örnek kod toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="14677-243">hello **DocumentationSamplesRuby** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="14677-244">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="14677-244">Default template</span></span>  
  
```xml  
require 'net/http'  
  
uri = URI('{{scheme}}://{{host}}{{path}}')  
uri.query = URI.encode_www_form({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}'{% unless forloop.last %},{% endunless %}  
{% endfor -%}  
{% endif -%}  
})  
  
request = Net::HTTP::{{ method | downcase | capitalize }}.new(uri.request_uri)  
{% for header in headers -%}  
# Request headers  
request['{{header.name}}'] = '{{header.value}}'  
{% endfor -%}  
{% if body -%}  
# Request body  
request.body = "{{ body | replace:'"','\"' }}"  
{% endif -%}  
  
response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|  
    http.request(request)  
end  
  
puts response.body  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="14677-245">Denetimler</span><span class="sxs-lookup"><span data-stu-id="14677-245">Controls</span></span>  
 <span data-ttu-id="14677-246">Merhaba kod örnek şablonları herhangi hello kullanımını izin verme [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="14677-246">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="14677-247">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="14677-247">Data model</span></span>  
 <span data-ttu-id="14677-248">[Kod örneği](api-management-template-data-model-reference.md#Sample) varlık.</span><span class="sxs-lookup"><span data-stu-id="14677-248">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="14677-249">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="14677-249">Sample template data</span></span>  
  
```json  
{  
    "title": "Ruby",  
    "snippet": null,  
    "brush": "ruby",  
    "template": "DocumentationSamplesRuby",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```

## <a name="next-steps"></a><span data-ttu-id="14677-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14677-250">Next steps</span></span>
<span data-ttu-id="14677-251">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="14677-251">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
