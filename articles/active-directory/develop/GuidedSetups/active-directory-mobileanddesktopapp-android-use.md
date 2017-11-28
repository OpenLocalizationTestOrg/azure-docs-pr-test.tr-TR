---
title: "Azure AD v2 Android başlamak - kullanın | Microsoft Docs"
description: "Nasıl bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren API'larını çağırma"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7963a07a2b9d529e89302f32e5ffd56c51687ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="56c91-103">Microsoft Graph API için bir belirteç almak üzere Microsoft kimlik doğrulama kitaplığı (MSAL) kullanın</span><span class="sxs-lookup"><span data-stu-id="56c91-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

1.  <span data-ttu-id="56c91-104">Açık: `MainActivity` (altında `app`  >  `java`  >  `{domain}.{appname}`)</span><span class="sxs-lookup"><span data-stu-id="56c91-104">Open: `MainActivity` (under `app` > `java` > `{domain}.{appname}`)</span></span>
2.  <span data-ttu-id="56c91-105">Aşağıdaki içeri aktarmaları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="56c91-105">Add the following imports:</span></span>

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="56c91-106">Değiştir `MainActivity` aşağıda ile sınıfı:</span><span class="sxs-lookup"><span data-stu-id="56c91-106">Replace the `MainActivity` class with below:</span></span>
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter the application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt to get a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined to handle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined to handle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in the cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need to do an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store the authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update the UI to post call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed to acquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with the STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled the authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use the access
         * token to call the Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store the auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update the UI to post call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed to acquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with the STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled the authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set the UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL to acquireToken for the end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles the redirect from the System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="56c91-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="56c91-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="56c91-108">Etkileşimli bir kullanıcı belirteci alma</span><span class="sxs-lookup"><span data-stu-id="56c91-108">Getting a user token interactive</span></span>
<span data-ttu-id="56c91-109">Çağırma `AcquireTokenAsync` yöntemi, oturum açmak için kullanıcıdan bir pencere sonuçlanıyor.</span><span class="sxs-lookup"><span data-stu-id="56c91-109">Calling the `AcquireTokenAsync` method results in a window prompting the user to sign in.</span></span> <span data-ttu-id="56c91-110">Uygulamalar genellikle gerektirir etkileşimli olarak korunan bir kaynağa erişmek için ihtiyaç duydukları ilk kez oturum açmak bir kullanıcı ya da (örneğin kullanıcının parolasının süresi) belirteci başarısız edinmeye sessiz bir işlem.</span><span class="sxs-lookup"><span data-stu-id="56c91-110">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="56c91-111">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="56c91-111">Getting a user token silently</span></span>
<span data-ttu-id="56c91-112">`AcquireTokenSilentAsync`belirteç satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="56c91-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="56c91-113">Sonra `AcquireTokenAsync` ilk kez yürütüldüğünde `AcquireTokenSilentAsync` veya belirteçleri yenileme isteği için çağrıları sessizce gerçekleştirilmediğinden sonraki çağrılar için-korunan kaynaklara erişim belirteçleri almak için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="56c91-113">After `AcquireTokenAsync` is executed for the first time, `AcquireTokenSilentAsync` is the method commonly used to obtain tokens to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="56c91-114">Sonuç olarak, `AcquireTokenSilentAsync` başarısız olur – örneğin kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti.</span><span class="sxs-lookup"><span data-stu-id="56c91-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="56c91-115">MSAL algıladığında, etkileşimli bir eylem gerektirmeyen tarafından sorunu çözmek için harekete bir `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="56c91-115">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="56c91-116">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="56c91-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="56c91-117">Karşı çağırmaya `AcquireTokenAsync` hemen hangi sonuçları oturum açma kullanıcıdan içinde.</span><span class="sxs-lookup"><span data-stu-id="56c91-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting the user to sign-in.</span></span> <span data-ttu-id="56c91-118">Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik uygulamada kullanıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="56c91-118">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="56c91-119">Destekli Bu kurulum tarafından oluşturulan örnek bu deseni kullanır: örnek yürütme eylemi ilk zamanında görebilirsiniz: hiçbir kullanıcı, uygulamayı her zamankinden kullanıldığından `PublicClientApp.Users.FirstOrDefault` bir null değer içerir ve bir `MsalUiRequiredException` özel durum.</span><span class="sxs-lookup"><span data-stu-id="56c91-119">The sample generated by this guided setup uses this pattern: you can see it in action the first time you execute the sample: because no user ever used the application, `PublicClientApp.Users.FirstOrDefault` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="56c91-120">Ardından örnek kodda çağırarak özel durumu işler `AcquireTokenAsync` oturum açma kullanıcıdan içinde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="56c91-120">The code in the sample then handles the exception by calling `AcquireTokenAsync` resulting in prompting the user to sign-in.</span></span>
2.  <span data-ttu-id="56c91-121">Uygulamalar bir etkileşimli oturum açma kullanıcı oturum açmak için doğru zamanı seçebilir ya da uygulama deneyebilirsiniz gerekli olan kullanıcı için görsel bir gösterge de yapabilirsiniz `AcquireTokenSilentAsync` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="56c91-121">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="56c91-122">Bunun yaygın olarak kullanılan kullanıcı uygulamanın işlevselliğini kesintiye olmadan erişebilir - Örneğin, çevrimdışı içeriği uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="56c91-122">This is commonly used when the user is able to access functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="56c91-123">Bu durumda, kullanıcı ne zaman korumalı kaynağa erişmek için ya da eski bilgileri yenilemek için oturum açmak istedikleri veya uygulamanızın denemeye karar verebilirsiniz karar verebilir `AcquireTokenSilentAsync` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="56c91-123">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="56c91-124">Yalnızca edinilen belirteçle kullanarak Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="56c91-124">Call the Microsoft Graph API using the token you just obtained</span></span>
1.  <span data-ttu-id="56c91-125">İçine aşağıdaki yöntemleri ekleyin `MainActivity` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="56c91-125">Add the following methods into the `MainActivity` class:</span></span>

```java
/* Use Volley to make an HTTP request to the /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request to graph");

    /* Make sure we have a token to send to graph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed to put parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send to UI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET to Queue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets the Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="56c91-126">Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="56c91-126">More information about making a REST call against a protected API</span></span>

<span data-ttu-id="56c91-127">Bu örnek uygulamasında `callGraphAPI` çağrıları `getAccessToken` ve bir HTTP yapar `GET` bir belirteç gerekiyor ve içerik döndüren bir kaynak isteği.</span><span class="sxs-lookup"><span data-stu-id="56c91-127">In this sample application, `callGraphAPI` calls `getAccessToken` and then makes an HTTP `GET` request against a resource that requires a token and returns the content.</span></span> <span data-ttu-id="56c91-128">Bu yöntem alınan belirteç ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="56c91-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="56c91-129">Bu örnek için Microsoft Graph API kaynaktır *bana* endpoint – kullanıcı profili bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="56c91-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="setup-sign-out"></a><span data-ttu-id="56c91-130">Kurulum oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="56c91-130">Setup Sign-out</span></span>

1.  <span data-ttu-id="56c91-131">İçine aşağıdaki yöntemleri ekleyin `MainActivity` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="56c91-131">Add the following methods into the `MainActivity` class:</span></span>

```java
/* Clears a user's tokens from the cache.
 * Logically similar to "sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt to get a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set the UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="56c91-132">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="56c91-132">More information</span></span>

<span data-ttu-id="56c91-133">`onSignOutClicked`kaldırır kullanıcı MSAL kullanıcı önbelleğinden – bu etkin etkileşimli olarak yapılırsa bir belirteç almak için gelecekteki bir isteği yalnızca başarılı şekilde geçerli kullanıcının unuttunuz MSAL söyler.</span><span class="sxs-lookup"><span data-stu-id="56c91-133">`onSignOutClicked` above removes the user from MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>
<span data-ttu-id="56c91-134">Bu örnek uygulamasında tek bir kullanıcı desteklese de MSAL nerede birden fazla hesap oturum açmış aynı anda – bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu örneğidir senaryolarını destekler.</span><span class="sxs-lookup"><span data-stu-id="56c91-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->
