## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="c2899-101">Bir Azure Resource Manager belirteç edinme</span><span class="sxs-lookup"><span data-stu-id="c2899-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="c2899-102">Azure Active Directory kaynakları hello Azure Resource Manager kullanarak gerçekleştirdiğiniz tüm hello görevler kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2899-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="c2899-103">diğer yaklaşımlar görmek için hello burada gösterilen örnek parola kimlik doğrulaması kullanır, [Azure Resource Manager kimlik doğrulama istekleri][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="c2899-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="c2899-104">Aşağıdaki kodu toohello hello eklemek **ana** Program.cs tooretrieve hello uygulama kimliği ve parola kullanarak Azure AD'den bir belirteç yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c2899-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="c2899-105">Oluşturma bir **ResourceManagementClient** kullanan kodu toohello hello sonuna aşağıdaki hello ekleyerek belirteci hello nesne **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="c2899-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="c2899-106">Oluşturma veya bir başvuru için kullanmakta olduğunuz hello kaynak grubu elde:</span><span class="sxs-lookup"><span data-stu-id="c2899-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx