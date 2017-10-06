---
title: "Azure Active Directory kimlik doğrulama iş Azure uygulamasıyla aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir ASP.NET MVC satır iş kolu uygulamanızın Azure App Service, kimlik doğrulamasını yapar Azure Active Directory ile"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur
Bu makale size nasıl gösterir toocreate bir .NET satır iş kolu uygulaması [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) hello kullanarak [kimlik doğrulama / yetkilendirme](../app-service/app-service-authentication-overview.md) özelliği. Ayrıca gösterir nasıl toouse hello [Azure Active Directory grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) hello uygulamasındaki tooquery dizin verileri.

kullandığınız hello Azure Active Directory Kiracı yalnızca Azure directory olabilir. Veya olabilir [şirket içi Active Directory ile eşitlenen](../active-directory/active-directory-aadconnect.md) toocreate çoklu oturum açma deneyimini şirket içi ve uzak çalışanlar için. Bu makalede Azure hesabınız için hello varsayılan dizini kullanır.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Yapı
App Service Web Apps basit bir iş kolu satır oluştur-okunur-güncelleştir-Sil (CRUD) uygulama parçaları ile Merhaba özellikler aşağıdaki öğeleri iş oluşturacak:

* Azure Active Directory karşı kullanıcıların kimliğini doğrular
* Sorgular directory kullanıcıları ve grupları kullanarak [Azure Active Directory grafik API'si](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Kullanım hello ASP.NET MVC *doğrulaması yok* şablonu

Azure'da satır iş kolu uygulamanız için rol tabanlı erişim denetimi (RBAC) gerekiyorsa, bkz: [sonraki adım](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Ne gerekiyor
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Bu öğreticiyi toocomplete hello:

* Bir Azure Active Directory Kiracı çeşitli gruplarındaki kullanıcılar ile
* Hello Azure Active Directory kiracısı üzerinde izinleri toocreate uygulamalar
* Visual Studio 2013 güncelleştirme 4 veya üstü
* [Azure SDK 2.8.1 ile veya daha yenisi](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Oluşturma ve bir web uygulaması tooAzure dağıtma
1. Visual Studio'dan tıklatın **dosya** > **yeni** > **proje**.
2. Seçin **ASP.NET Web uygulaması**, projenizi adlandırın ve tıklayın **Tamam**.
3. Select hello **MVC** şablon hello kimlik doğrulaması da değiştirmem**doğrulaması yok**. Emin olun **hello bulut ana** seçilir ve tıklatın **Tamam**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. Merhaba, **App Service Oluştur** iletişim kutusunda, tıklatın **Hesap Ekle** (ve ardından **Hesap Ekle** hello açılır içinde) tooyour Azure hesabı toolog.
5. Oturum açtıktan sonra web uygulamanızı yapılandırın. Merhaba ilgili tıklayarak bir kaynak grubu ve yeni bir uygulama hizmeti planı oluştur **yeni** düğmesi. Tıklatın **diğer Azure hizmetlerini keşfedin** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. Merhaba, **Hizmetleri** sekmesini tıklatın,  **+**  tooadd uygulamanız için bir SQL veritabanı. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. İçinde **SQL veritabanını yapılandırma**, tıklatın **yeni** toocreate bir SQL Server örneği.
8. İçinde **SQL Server'ı Yapılandır**, SQL Server örneğinizi yapılandırın. Ardından **Tamam**, **Tamam**, ve **oluşturma** tookick azure'da hello uygulama oluşturma devre dışı.
9. İçinde **Azure App Service etkinliği**, başlangıç uygulaması oluşturma işleminin bittiği görebilirsiniz. Tıklatın  **Yayımla &lt;* appname*> toothis Web uygulaması şimdi **, ardından **Yayımla**. 
   
    Visual Studio tamamlandıktan sonra hello açar uygulama yayımlama hello tarayıcıda. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Kimlik doğrulama ve dizin erişimi yapılandırma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüden **uygulama hizmetleri** > **&lt;*appname*> ** > **kimlik doğrulama / yetkilendirme**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Azure Active Directory authentication'ı tıklatarak açmak **üzerinde** > **Azure Active Directory** > **Express** > **Tamam**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Tıklatın **kaydetmek** hello komut çubuğunda.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Merhaba kimlik doğrulama ayarları başarıyla kaydedildi sonra tooyour uygulamayı yeniden hello tarayıcıda gezinme deneyin. Varsayılan ayarlarınızı hello tüm uygulama kimlik doğrulamasını zorunlu. Zaten oturum açmadıysanız, yeniden yönlendirilen tooa oturum açma ekranı olduğunuz. Oturum açtıktan sonra uygulamanızı HTTPS ile güvenli bakın. Ardından, tooenable erişim toodirectory veri gerekir. 
5. Toohello gidin [Klasik portal](https://manage.windowsazure.com).
6. Merhaba sol menüden **Active Directory** > **varsayılan dizin** > **uygulamaları**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Uygulama hizmeti, tooenable hello için yetkilendirme oluşturulan hello Azure Active Directory Uygulama budur / kimlik doğrulama özelliği.
7. Tıklatın **kullanıcılar** ve **grupları** toomake, bazı kullanıcılar ve gruplar hello dizinine sahip olduğunuzdan emin. Değilse, birkaç test kullanıcıları ve grupları oluşturun.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Tıklatın **yapılandırma** tooconfigure bu uygulama.
9. Toohello aşağı **anahtarları** bölüm ve bir süre seçerek bir anahtar ekleyin. Ardından **izinlere temsilci** seçip **dizin verilerini okuma**. 
   **Kaydet** düğmesine tıklayın.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Ayarlarınız kaydedildikten sonra geri toohello kaydırma **anahtarları** hello'ye tıklayın **kopyalama** düğmesini toocopy hello istemci anahtarı. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Bu sayfayı terk şimdi giderseniz, bu istemci anahtar herhangi bir zamanda yeniden mümkün tooaccess olmayacaktır.
    > 
    > 
11. Ardından, tooconfigure bu anahtarla web uygulamanız gerekir. İçinde toohello oturum [Azure kaynak Gezgini](https://resources.azure.com) Azure hesabınızla.
12. Merhaba hello sayfanın en üstünde, tıklatın **okuma/yazma** toomake değişiklikleri hello Azure kaynak Gezgini.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Hello abonelikleri bulunan uygulamanız için kimlik doğrulama ayarlarını Bul >  **&lt;* varlığıyla subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **sağlayıcıları** > **Microsoft.Web**  >  **siteleri** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. **Düzenle**’ye tıklayın.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Hello bölmesini düzenleme hello ayarlamak `clientSecret` ve `additionalLoginParams` aşağıdaki gibi özellikleri.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Tıklatın **Put** en üst toosubmit değişikliklerinizi hello.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Şimdi, tooaccess hello Azure Active Directory grafik API'sini belirteci, yalnızca gidin hello yetkilendirme varsa tootest  **https://&lt;*appname*> içinde.azurewebsites.net/.auth/me**, Tarayıcı. Her şeyin doğru şekilde yapılandırdıysanız, hello görmelisiniz `access_token` hello JSON yanıt özelliği.
    
    Merhaba `~/.auth/me` URL yolu App Service kimlik doğrulaması tarafından yönetilen /, tüm hello ilgili bilgileri kimlik doğrulaması tooyour oturumu yetkilendirme toogive. Daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme Azure App Service'te](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Merhaba `access_token` bir sona erme süresi vardır. Ancak, App Service kimlik doğrulama / yetkilendirme belirteci yenileme işlevleri ile sağlayan `~/.auth/refresh`. Hakkında daha fazla bilgi için toouse, bkz: [App Service Belirteç Deposu](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Ardından, dizin verileri ile faydalı bir şey yapar.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>İş işlevselliği tooyour uygulama Ekle
Şimdi, basit bir CRUD iş öğeleri İzleyici oluşturun.  

1. Merhaba ~\Models klasöründe WorkItem.cs adlı bir sınıf dosyası oluşturun ve değiştirin `public class WorkItem {...}` koddan hello ile:
   
     System.ComponentModel.DataAnnotations kullanarak;
   
     İş öğesi {ortak sınıfı
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     Ortak enum WorkItemStatus {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Merhaba proje toomake yeni model erişilebilir toohello yapı iskelesi mantığınızı Visual Studio'da derleme.
3. Yeni iskele kurulmuş Öğe Ekle `WorkItemsController` toohello ~\Controllers klasörü (sağ **denetleyicileri**, çok noktası**Ekle**seçip **yeni iskele kurulmuş öğe**). 
4. Seçin **Entity Framework kullanarak MVC 5 denetleyici, görünümleri olan** tıklatıp **Ekle**.
5. Oluşturduğunuz select hello modeli ardından  **+**  ve ardından **Ekle** tooadd bir veri bağlamı ve ardından **Ekle**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. Merhaba ~\Views\WorkItems\Create.cshtml (otomatik olarak kurulmuş bir öğe), bulma `Html.BeginForm` yardımcı yöntem ve hello aşağıdaki vurgulanan değişiklikler yapın:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Unutmayın `token` ve `tenant` hello tarafından kullanılan `AadPicker` nesne toomake Azure Active Directory grafik API'sini çağırır. Ekleyeceksiniz `AadPicker` daha sonra.     
   
   > [!NOTE]
   > Yalnızca de alabilirsiniz `token` ve `tenant` hello istemci tarafındaki ile `~/.auth/me`, ancak bu bir ek sunucu araması olacaktır. Örneğin:
   > 
   > $.ajax ({veri türü: "json", url: "/.auth/me", başarı: işlevi (veri) {var belirteci verileri [0] = .access_token; var Kiracı verileri [0] .user_claims .find = (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});
   > 
   > 
7. Merhaba sahip aynı değişiklik ~ \Views\WorkItems\Edit.cshtml.
8. Merhaba `AadPicker` nesne tanımlanmış bir betikte tooadd tooyour proje gerekir. Merhaba ~\Scripts klasöre sağ tıklayın, çok noktası**Ekle**, tıklatıp **JavaScript dosyası**. Tür `AadPickerLibrary` hello filename ve tıklatın **Tamam**.
9. Merhaba içeriğine kopyalama [burada](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) içine ~ \Scripts\AadPickerLibrary.js.
   
   Merhaba komut dosyasında hello `AadPicker` nesne çağrıları [Azure Active Directory grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch kullanıcıların ve grupların hello giriş eşleştirmek için.  
10. ~\Scripts\AadPickerLibrary.js de hello kullanır [jQuery UI otomatik tamamlama pencere](https://jqueryui.com/autocomplete/). Bu nedenle tooadd jQuery UI tooyour proje gerekir. Projenize sağ tıklatın ve **NuGet paketlerini Yönet**.
11. Hello NuGet Paket Yöneticisi, Gözat ' ı tıklatın. türü **jquery UI** hello arama çubuğu ve tıklatın **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Merhaba sağ bölmede **yükleme**, ardından **Tamam** tooproceed.
13. ~\App_Start\BundleConfig.cs açın ve aşağıdaki vurgulanan değişiklikler hello yapın:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Daha fazla kullanıcı yolu toomanage JavaScript ve CSS dosyaları, uygulamanızda vardır. Ancak, kolaylık sağlamak için yalnızca toopiggyback her görünümü ile yüklenen hello paketleri üzerinde oluşturacağız.
14. Son olarak, içinde ~ \Global.asax, hello kod satırı aşağıdaki hello eklemek `Application_Start()` yöntemi. `Ctrl`+`.`Her adlandırma çözümleme hatası çok Düzelt.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Merhaba varsayılan MVC şablonundaki kullandığından bu kod satırı gereksinim <code>[ValidateAntiForgeryToken]</code> decoration bazı hello eylemler. Tarafından açıklanan toohello davranışı nedeniyle [Brock Allen](https://twitter.com/BrockLAllen) adresindeki [MVC 4, AntiForgeryToken ve talep](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) HTTP POST sahteciliğe karşı koruma belirteci doğrulaması başarısız:
    > 
    > * Azure Active Directory, varsayılan olarak hello sahteciliğe karşı koruma belirteci tarafından gerekli olan hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider göndermez.
    > * Azure Active Directory dizin AD FS ile eşitlenen ise, AD FS toosend el ile yapılandırabilmenize karşın hello AD FS güven varsayılan hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider talep ya da, göndermez Bu talep.
    > 
    > `ClaimTypes.NameIdentifies`Merhaba talep belirtir `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, hangi Azure Active Directory sağlayın.  
    > 
    > 
15. Şimdi, değişikliklerinizi yayımlayın. Projenize sağ tıklatın ve **Yayımla**.
16. Tıklatın **ayarları**olduğunu denetleyin bir bağlantı dizesi tooyour SQL veritabanı, seçin **güncelleştirme veritabanı** toomake hello modeliniz için şema değişiklikleri ve tıklayın **Yayımla** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. Merhaba tarayıcıda toohttps gidin: / /&lt;*appname*> tıklayın ve.azurewebsites.net/workitems **Yeni Oluştur**.
18. Tıklatın hello **AssignedToName** kutusu. Artık Azure Active Directory kiracınızda bir açılır kullanıcılar ve gruplar da görmeniz gerekir. Toofilter yazın veya hello kullanın `Up` veya `Down` anahtar veya tooselect hello kullanıcıyı veya grubu tıklatın. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Tıklatın **oluşturma** toosave hello değişiklikleri. Ardından **Düzenle** oluşturulan hello çalışma öğesi tooobserve hello aynı davranışı.

Congrats, artık bir iş kolu satır uygulama Azure'da dizin erişimle çalıştırdığınız! Grafik API'si hello ile yapabileceğiniz çok daha fazla yoktur. Bkz: [Azure AD Graph API Başvurusu](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Sonraki adım
Azure'da satır iş kolu uygulamanız için rol tabanlı erişim denetimi (RBAC) gerekiyorsa, bkz: [WebApp RoleClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) hello Azure Active Directory ekibinden bir örnek için. Size bir nasıl gösterir Azure Active Directory uygulamanız için tooenable rolleri ve hello kullanıcılar yetki `[Authorize]` decoration.

İş uygulamanızı tooon içi veri erişimi gerektirir, bkz: [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Ek kaynaklar
* [Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti](../app-service/app-service-authentication-overview.md)
* [Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması](web-sites-authentication-authorization.md)
* [AD FS kimlik doğrulaması ile bir satır iş kolu uygulaması oluşturma](web-sites-dotnet-lob-application-adfs.md)
* [Uygulama hizmeti kimlik doğrulama ve hello Azure AD grafik API'si](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Microsoft Azure Active Directory örnekler ve belgeler](https://github.com/AzureADSamples)
* [Azure Active Directory desteklenen belirteç ve talep türleri](http://msdn.microsoft.com/library/azure/dn195587.aspx)
