---
title: Sichern von .NET-Microservices und Webanwendungen
description: Sicherheit in .NET-Microservices und -Webanwendungen – Lernen Sie die Authentifizierungsoptionen in ASP.NET Core-Webanwendungen kennen.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 0894465858e3503e2eddb5299b404f7ba95fdd6a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295204"
---
# <a name="make-secure-net-microservices-and-web-applications"></a><span data-ttu-id="2ef82-103">Erstellen sicherer .NET-Microservices und -Webanwendungen</span><span class="sxs-lookup"><span data-stu-id="2ef82-103">Make secure .NET Microservices and Web Applications</span></span>

<span data-ttu-id="2ef82-104">Das Thema Sicherheit in Microservices und Webanwendungen hat so viele Aspekte, dass zu seiner Behandlung gleich mehrere Bücher wie dieses erforderlich wären – daher wollen wir uns in diesem Abschnitt auf Authentifizierung, Autorisierung und Anwendungsgeheimnisse konzentrieren.</span><span class="sxs-lookup"><span data-stu-id="2ef82-104">There are so many aspects about security in microservices and web applications that the topic could easy take several books like this one so, in this section, we'll focus on authentication, authorization, and application secrets.</span></span>

## <a name="implement-authentication-in-net-microservices-and-web-applications"></a><span data-ttu-id="2ef82-105">Implementieren von Authentifizierung in .NET-Microservices und -Webanwendungen</span><span class="sxs-lookup"><span data-stu-id="2ef82-105">Implement authentication in .NET microservices and web applications</span></span>

<span data-ttu-id="2ef82-106">Ressourcen und APIs, die durch einen Dienst veröffentlicht wurden, müssen oftmals auf bestimmte vertrauenswürdige Benutzer oder Clients beschränkt werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-106">It's often necessary for resources and APIs published by a service to be limited to certain trusted users or clients.</span></span> <span data-ttu-id="2ef82-107">Der erste Schritt zur Durchführung dieser Entscheidungen über die Vertrauenswürdigkeit auf API-Ebene ist die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="2ef82-107">The first step to making these sorts of API-level trust decisions is authentication.</span></span> <span data-ttu-id="2ef82-108">Authentifizierung bezeichnet den Vorgang der zuverlässigen Überprüfung der Identität eines Benutzers.</span><span class="sxs-lookup"><span data-stu-id="2ef82-108">Authentication is the process of reliably verify a user’s identity.</span></span>

<span data-ttu-id="2ef82-109">In Microservice-Szenarios wird die Authentifizierung in der Regel zentral verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="2ef82-109">In microservice scenarios, authentication is typically handled centrally.</span></span> <span data-ttu-id="2ef82-110">Wenn Sie ein API-Gateway verwenden, ist dieses Gateway ein guter Ort, um die Authentifizierung durchzuführen, so wie in Abbildung 9-1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-110">If you're using an API Gateway, the gateway is a good place to authenticate, as shown in Figure 9-1.</span></span> <span data-ttu-id="2ef82-111">Wenn Sie nach diesem Ansatz vorgehen, stellen Sie sicher, dass die einzelnen Microservices nicht direkt (ohne das API-Gateway) erreicht werden können, außer es kann zusätzliche Sicherheit garantiert werden, um Benachrichtigen danach zu authentifizieren, ob sie vom Gateway stammen oder nicht.</span><span class="sxs-lookup"><span data-stu-id="2ef82-111">If you use this approach, make sure that the individual microservices cannot be reached directly (without the API Gateway) unless additional security is in place to authenticate messages whether they come from the gateway or not.</span></span>

![Wenn die Authentifizierung im API-Gateway zentralisiert ist, fügt dieses Anforderungen beim Weiterleiten an die Microservices Benutzerinformationen hinzu.](./media/image1.png)

<span data-ttu-id="2ef82-113">**Abbildung 9-1**.</span><span class="sxs-lookup"><span data-stu-id="2ef82-113">**Figure 9-1**.</span></span> <span data-ttu-id="2ef82-114">Zentrale Authentifizierung mit einem API-Gateway</span><span class="sxs-lookup"><span data-stu-id="2ef82-114">Centralized authentication with an API Gateway</span></span>

<span data-ttu-id="2ef82-115">Wenn auf Dienste direkt zugegriffen werden kann, kann ein Authentifizierungsdienst wie Azure Active Directory oder ein dedizierter Authentifizierungs-Microservice, der als Sicherheitstokendienst (STS) fungiert, zum Authentifizieren von Benutzern verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-115">If services can be accessed directly, an authentication service like Azure Active Directory or a dedicated authentication microservice acting as a security token service (STS) can be used to authenticate users.</span></span> <span data-ttu-id="2ef82-116">Entscheidungen über die Vertrauenswürdigkeit werden zwischen Diensten mit Sicherheitstoken oder Cookies freigegeben.</span><span class="sxs-lookup"><span data-stu-id="2ef82-116">Trust decisions are shared between services with security tokens or cookies.</span></span> <span data-ttu-id="2ef82-117">(Diese Token können bei Bedarf zwischen ASP.NET Core-Anwendungen durch Implementierung der [gemeinsamen Nutzung von Cookies](/aspnet/core/security/cookie-sharing) freigegeben werden.) Dieses Muster ist in Abbildung 9-2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-117">(These tokens can be shared between ASP.NET Core applications, if needed, by implementing [cookie sharing](/aspnet/core/security/cookie-sharing).) This pattern is illustrated in Figure 9-2.</span></span>

![Beim direkten Zugriff auf Microservices wird die Vertrauensstellung, die Authentifizierung und Autorisierung beinhaltet, mithilfe eines Sicherheitstokens behandelt, das von einem von den Microservices gemeinsam verwendeten, dedizierten Microservice herausgegeben wird.](./media/image2.png)

<span data-ttu-id="2ef82-119">**Abbildung 9-2:**</span><span class="sxs-lookup"><span data-stu-id="2ef82-119">**Figure 9-2**.</span></span> <span data-ttu-id="2ef82-120">Authentifizierung durch Identitäts-Microservice; das Vertrauen ist mithilfe eines Autorisierungstokens freigegeben.</span><span class="sxs-lookup"><span data-stu-id="2ef82-120">Authentication by identity microservice; trust is shared using an authorization token</span></span>

### <a name="authenticate-with-aspnet-core-identity"></a><span data-ttu-id="2ef82-121">Authentifizierung mit ASP.NET Core Identity</span><span class="sxs-lookup"><span data-stu-id="2ef82-121">Authenticate with ASP.NET Core Identity</span></span>

<span data-ttu-id="2ef82-122">Der primäre Mechanismus in ASP.NET Core zur Identifizierung eines Anwendungsbenutzers ist das Mitgliedschaftssystem [ASP.NET Core Identity](/aspnet/core/security/authentication/identity).</span><span class="sxs-lookup"><span data-stu-id="2ef82-122">The primary mechanism in ASP.NET Core for identifying an application’s users is the [ASP.NET Core Identity](/aspnet/core/security/authentication/identity) membership system.</span></span> <span data-ttu-id="2ef82-123">ASP.NET Core Identity speichert Benutzerinformationen (einschließlich Anmeldeinformationen, Rollen und Ansprüche) in einem Datenspeicher, der vom Entwickler konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="2ef82-123">ASP.NET Core Identity stores user information (including sign-in information, roles, and claims) in a data store configured by the developer.</span></span> <span data-ttu-id="2ef82-124">Normalerweise ist der ASP.NET Core Identity-Datenspeicher ein Entity Framework-Speicher, der im `Microsoft.AspNetCore.Identity.EntityFrameworkCore`-Paket bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="2ef82-124">Typically, the ASP.NET Core Identity data store is an Entity Framework store provided in the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` package.</span></span> <span data-ttu-id="2ef82-125">Jedoch können benutzerdefinierte Speicher oder andere Pakete von Drittanbietern zum Speichern von Identitätsinformationen in Azure Table Storage, CosmosDB oder anderen Speicherorten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-125">However, custom stores or other third-party packages can be used to store identity information in Azure Table Storage, CosmosDB, or other locations.</span></span>

<span data-ttu-id="2ef82-126">Der folgende Code wird aus der Projektvorlage der ASP.NET Core-Webanwendung genommen, für die eine einzelne Benutzerkontoauthentifizierung ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="2ef82-126">The following code is taken from the ASP.NET Core Web Application project template with individual user account authentication selected.</span></span> <span data-ttu-id="2ef82-127">Er stellt dar, wie ASP.NET Core Identiy mithilfe von EntityFramework.Core in der Startup.ConfigureServices-Methode konfiguriert wird.</span><span class="sxs-lookup"><span data-stu-id="2ef82-127">It shows how to configure ASP.NET Core Identity using EntityFramework.Core in the Startup.ConfigureServices method.</span></span>

```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
```

<span data-ttu-id="2ef82-128">Sobald ASP.NET Core Identity konfiguriert ist, aktivieren Sie den Dienst, indem Sie „app.UseIdentity“ in der `Startup.Configure`-Methode des Diensts aufrufen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-128">Once ASP.NET Core Identity is configured, you enable it by calling app.UseIdentity in the service’s `Startup.Configure` method.</span></span>

<span data-ttu-id="2ef82-129">Durch die Verwendung von ASP.NET Core Identity sind mehrere Szenarios möglich:</span><span class="sxs-lookup"><span data-stu-id="2ef82-129">Using ASP.NET Core Identity enables several scenarios:</span></span>

- <span data-ttu-id="2ef82-130">Erstellen Sie neue Benutzerinformationen mithilfe des UserManager-Typs (userManager.CreateAsync).</span><span class="sxs-lookup"><span data-stu-id="2ef82-130">Create new user information using the UserManager type (userManager.CreateAsync).</span></span>

- <span data-ttu-id="2ef82-131">Authentifizieren Sie Benutzer mithilfe des SignInManager-Typs.</span><span class="sxs-lookup"><span data-stu-id="2ef82-131">Authenticate users using the SignInManager type.</span></span> <span data-ttu-id="2ef82-132">Sie können `signInManager.SignInAsync` für die direkte Anmeldung verwenden oder mithilfe von `signInManager.PasswordSignInAsync` die Richtigkeit des Benutzerkennworts bestätigen und diesen anschließend anmelden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-132">You can use `signInManager.SignInAsync` to sign in directly, or `signInManager.PasswordSignInAsync` to confirm the user’s password is correct and then sign them in.</span></span>

- <span data-ttu-id="2ef82-133">Identifizieren Sie einen Benutzer auf Grundlage von Informationen, die in einem Cookie gespeichert sind (das von der ASP.NET Core Identity-Middleware gelesen wird), damit nachfolgende Anforderungen von einem Browser die Identität und Ansprüche eines angemeldeten Benutzers enthalten.</span><span class="sxs-lookup"><span data-stu-id="2ef82-133">Identify a user based on information stored in a cookie (which is read by ASP.NET Core Identity middleware) so that subsequent requests from a browser will include a signed-in user’s identity and claims.</span></span>

<span data-ttu-id="2ef82-134">ASP.NET Core Identity unterstützt auch die [zweistufige Authentifizierung](/aspnet/core/security/authentication/2fa).</span><span class="sxs-lookup"><span data-stu-id="2ef82-134">ASP.NET Core Identity also supports [two-factor authentication](/aspnet/core/security/authentication/2fa).</span></span>

<span data-ttu-id="2ef82-135">ASP.NET Core Identity ist eine empfohlene Lösung für Authentifizierungsszenarios, die einen Datenspeicher für lokale Benutzerdaten verwenden und die Identität zwischen Anforderungen mithilfe von Cookies (was typisch für MVC-Webanwendungen ist) beibehalten.</span><span class="sxs-lookup"><span data-stu-id="2ef82-135">For authentication scenarios that make use of a local user data store and that persist identity between requests using cookies (as is typical for MVC web applications), ASP.NET Core Identity is a recommended solution.</span></span>

### <a name="authenticate-with-external-providers"></a><span data-ttu-id="2ef82-136">Authentifizierung mithilfe externer Anbieter</span><span class="sxs-lookup"><span data-stu-id="2ef82-136">Authenticate with external providers</span></span>

<span data-ttu-id="2ef82-137">ASP.NET Core unterstützt auch die Verwendung von [externen Authentifizierungsanbietern](/aspnet/core/security/authentication/social/), damit sich Benutzer über [OAuth 2.0](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)-Flows anmelden können.</span><span class="sxs-lookup"><span data-stu-id="2ef82-137">ASP.NET Core also supports using [external authentication providers](/aspnet/core/security/authentication/social/) to let users sign in via [OAuth 2.0](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) flows.</span></span> <span data-ttu-id="2ef82-138">Das bedeutet, dass sich Benutzer mithilfe von vorhandenen Authentifizierungsprozessen von Anbietern wie Microsoft, Google, Facebook oder Twitter anmelden können und diese Identitäten ASP.NET Core Identity in Ihrer Anwendung zuordnen können.</span><span class="sxs-lookup"><span data-stu-id="2ef82-138">This means that users can sign in using existing authentication processes from providers like Microsoft, Google, Facebook, or Twitter and associate those identities with an ASP.NET Core identity in your application.</span></span>

<span data-ttu-id="2ef82-139">Für die Verwendung der externen Authentifizierung schließen Sie die entsprechende Authentifizierungsmiddleware in der HTTP-Pipeline zum Verarbeiten von Anforderungen ein.</span><span class="sxs-lookup"><span data-stu-id="2ef82-139">To use external authentication, you include the appropriate authentication middleware in your application’s HTTP request processing pipeline.</span></span> <span data-ttu-id="2ef82-140">Diese Middleware ist für die Verarbeitung von Anforderungen verantwortlich, um URI-Routen vom Authentifizierungsanbieter zurückzugeben, um Identitätsinformationen zu erfassen und diese über die SignInManager.GetExternalLoginInfo-Methode verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-140">This middleware is responsible for handling requests to return URI routes from the authentication provider, capturing identity information, and making it available via the SignInManager.GetExternalLoginInfo method.</span></span>

<span data-ttu-id="2ef82-141">Beliebte externe Authentifizierungsanbieter sowie deren zugeordnete NuGet-Pakete sind in der folgenden Tabelle dargestellt:</span><span class="sxs-lookup"><span data-stu-id="2ef82-141">Popular external authentication providers and their associated NuGet packages are shown in the following table:</span></span>

| <span data-ttu-id="2ef82-142">**Anbieter**</span><span class="sxs-lookup"><span data-stu-id="2ef82-142">**Provider**</span></span>  | <span data-ttu-id="2ef82-143">**Pakete**</span><span class="sxs-lookup"><span data-stu-id="2ef82-143">**Package**</span></span>                                          |
| ------------- | ---------------------------------------------------- |
| <span data-ttu-id="2ef82-144">**Microsoft**</span><span class="sxs-lookup"><span data-stu-id="2ef82-144">**Microsoft**</span></span> | <span data-ttu-id="2ef82-145">**Microsoft.AspNetCore.Authentication.MicrosoftAccount**</span><span class="sxs-lookup"><span data-stu-id="2ef82-145">**Microsoft.AspNetCore.Authentication.MicrosoftAccount**</span></span> |
| <span data-ttu-id="2ef82-146">**Google**</span><span class="sxs-lookup"><span data-stu-id="2ef82-146">**Google**</span></span>    | <span data-ttu-id="2ef82-147">**Microsoft.AspNetCore.Authentication.Google**</span><span class="sxs-lookup"><span data-stu-id="2ef82-147">**Microsoft.AspNetCore.Authentication.Google**</span></span>           |
| <span data-ttu-id="2ef82-148">**Facebook**</span><span class="sxs-lookup"><span data-stu-id="2ef82-148">**Facebook**</span></span>  | <span data-ttu-id="2ef82-149">**Microsoft.AspNetCore.Authentication.Facebook**</span><span class="sxs-lookup"><span data-stu-id="2ef82-149">**Microsoft.AspNetCore.Authentication.Facebook**</span></span>         |
| <span data-ttu-id="2ef82-150">**Twitter**</span><span class="sxs-lookup"><span data-stu-id="2ef82-150">**Twitter**</span></span>   | <span data-ttu-id="2ef82-151">**Microsoft.AspNetCore.Authentication.Twitter**</span><span class="sxs-lookup"><span data-stu-id="2ef82-151">**Microsoft.AspNetCore.Authentication.Twitter**</span></span>          |

<span data-ttu-id="2ef82-152">In allen Fällen wird die Middleware mithilfe eines Aufrufs einer Registrierungsmethode registriert, ähnlich wie `app.Use{ExternalProvider}Authentication` in `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="2ef82-152">In all cases, the middleware is registered with a call to a registration method similar to `app.Use{ExternalProvider}Authentication` in `Startup.Configure`.</span></span> <span data-ttu-id="2ef82-153">Diese Registrierungsmethoden nehmen ein Options-Objekt, das je nach Anbieter eine Anwendungs-ID sowie geheime Informationen (beispielsweise ein Kennwort) enthält.</span><span class="sxs-lookup"><span data-stu-id="2ef82-153">These registration methods take an options object that contains an application ID and secret information (a password, for instance), as needed by the provider.</span></span> <span data-ttu-id="2ef82-154">Externe Authentifizierungsanbieter erfordern, dass die Anwendung registriert ist (so wie in der [ASP.NET Core-Dokumentation beschrieben](/aspnet/core/security/authentication/social/)), sodass sie den Benutzer darüber informieren können, welche Anwendung Zugriff auf ihre Identität anfordert.</span><span class="sxs-lookup"><span data-stu-id="2ef82-154">External authentication providers require the application to be registered (as explained in [ASP.NET Core documentation](/aspnet/core/security/authentication/social/)) so that they can inform the user what application is requesting access to their identity.</span></span>

<span data-ttu-id="2ef82-155">Sobald die Middleware in `Startup.Configure` registriert ist, können Sie Benutzer auffordern, sich von einer beliebigen Controlleraktion aus anzumelden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-155">Once the middleware is registered in `Startup.Configure`, you can prompt users to sign in from any controller action.</span></span> <span data-ttu-id="2ef82-156">Um dies zu ermöglichen, erstellen Sie ein `AuthenticationProperties`-Objekt, das den Namen und die Umleitungs-URL des Authentifizierungsanbieters enthält.</span><span class="sxs-lookup"><span data-stu-id="2ef82-156">To do this, you create an `AuthenticationProperties` object that includes the authentication provider’s name and a redirect URL.</span></span> <span data-ttu-id="2ef82-157">Sie geben anschließend eine „Challenge“-Antwort zurück, die das `AuthenticationProperties`-Objekt übergibt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-157">You then return a Challenge response that passes the `AuthenticationProperties` object.</span></span> <span data-ttu-id="2ef82-158">Im folgenden Code ist ein Beispiel dafür dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-158">The following code shows an example of this.</span></span>

```csharp
var properties = _signInManager.ConfigureExternalAuthenticationProperties(provider,
    redirectUrl);
return Challenge(properties, provider);
```

<span data-ttu-id="2ef82-159">Der redirectUrl-Parameter enthält die URL, auf die der externe Anbieter umleiten soll, sobald sich der Benutzer authentifiziert hat.</span><span class="sxs-lookup"><span data-stu-id="2ef82-159">The redirectUrl parameter includes the URL that the external provider should redirect to once the user has authenticated.</span></span> <span data-ttu-id="2ef82-160">Die URL sollte eine Aktion darstellen, die den Benutzer, wie im folgenden vereinfachten Beispiel dargestellt, auf Grundlage externer Identitätsinformationen anmelden soll:</span><span class="sxs-lookup"><span data-stu-id="2ef82-160">The URL should represent an action that will sign the user in based on external identity information, as in the following simplified example:</span></span>

```csharp
// Sign in the user with this external login provider if the user
// already has a login.
var result = await _signInManager.ExternalLoginSignInAsync(info.LoginProvider, info.ProviderKey, isPersistent: false);

if (result.Succeeded)
{
    return RedirectToLocal(returnUrl);
}
else
{
    ApplicationUser newUser = new ApplicationUser
    {
        // The user object can be constructed with claims from the
        // external authentication provider, combined with information
        // supplied by the user after they have authenticated with
        // the external provider.
        UserName = info.Principal.FindFirstValue(ClaimTypes.Name),
        Email = info.Principal.FindFirstValue(ClaimTypes.Email)
    };
    var identityResult = await _userManager.CreateAsync(newUser);
    if (identityResult.Succeeded)
    {
        identityResult = await _userManager.AddLoginAsync(newUser, info);
        if (identityResult.Succeeded)
        {
            await _signInManager.SignInAsync(newUser, isPersistent: false);
        }
        return RedirectToLocal(returnUrl);
    }
}
```

<span data-ttu-id="2ef82-161">Wenn Sie die Authentifizierungsoption **Individual User Account** (Einzelbenutzerkonto) auswählen, wenn Sie das ASP.NET Code-Webanwendungsprojekt in Visual Studio erstellen, befindet sich der Code, der zur Anmeldung mit einem externen Anbieter benötigt wird, bereits im Projekt. Dies ist in Abbildung 9-3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-161">If you choose the **Individual User Account** authentication option when you create the ASP.NET Code web application project in Visual Studio, all the code necessary to sign in with an external provider is already in the project, as shown in Figure 9-3.</span></span>

![Dialogfeld für die neue ASP.NET Core-Webanwendung mit hervorgehobener Schaltfläche zum Ändern der Authentifizierung.](./media/image3.png)

<span data-ttu-id="2ef82-163">**Abbildung 9-3.**</span><span class="sxs-lookup"><span data-stu-id="2ef82-163">**Figure 9-3**.</span></span> <span data-ttu-id="2ef82-164">Auswählen einer Option zur Verwendung der externen Authentifizierung beim Erstellen eines Webanwendungsprojekts</span><span class="sxs-lookup"><span data-stu-id="2ef82-164">Selecting an option for using external authentication when creating a web application project</span></span>

<span data-ttu-id="2ef82-165">Zusätzlich zu den zuvor aufgeführten externen Authentifizierungsanbietern sind Pakete Dritter verfügbar, die Middleware zur Verwendung mehrerer externer Authentifizierungsanbieter bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-165">In addition to the external authentication providers listed previously, third-party packages are available that provide middleware for using many more external authentication providers.</span></span> <span data-ttu-id="2ef82-166">Eine Liste finden Sie im [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers/tree/dev/src)-Repository auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ef82-166">For a list, see the [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers/tree/dev/src) repo on GitHub.</span></span>

<span data-ttu-id="2ef82-167">Um besonderen Anforderungen gerecht zu werden, können Sie auch eigene Middleware zur externen Authentifizierung erstellen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-167">You can also create your own external authentication middleware to solve some special need.</span></span>

### <a name="authenticate-with-bearer-tokens"></a><span data-ttu-id="2ef82-168">Authentifizierung mit Bearertoken</span><span class="sxs-lookup"><span data-stu-id="2ef82-168">Authenticate with bearer tokens</span></span>

<span data-ttu-id="2ef82-169">Die Authentifizierung mit ASP.NET Core Identity (oder Identity plus externer Authentifizierunsanbieter) funktioniert für viele Webanwendungsszenarios einwandfrei, für die das Speichern von Benutzerinformationen in einem Cookie geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="2ef82-169">Authenticating with ASP.NET Core Identity (or Identity plus external authentication providers) works well for many web application scenarios in which storing user information in a cookie is appropriate.</span></span> <span data-ttu-id="2ef82-170">In anderen Szenarios sind Cookies jedoch kein natürlicher Vorgang zum Beibehalten und Übertragen von Daten.</span><span class="sxs-lookup"><span data-stu-id="2ef82-170">In other scenarios, though, cookies are not a natural means of persisting and transmitting data.</span></span>

<span data-ttu-id="2ef82-171">Beispielsweise verwenden Sie in einer ASP.NET Core-Web-API, die RESTful-Endpunkte verfügbar macht, auf die möglicherweise Einzelseitenanwendungen, native Clients oder auch andere Web-APIs zugreifen, stattdessen Bearertoken.</span><span class="sxs-lookup"><span data-stu-id="2ef82-171">For example, in an ASP.NET Core Web API that exposes RESTful endpoints that might be accessed by Single Page Applications (SPAs), by native clients, or even by other Web APIs, you typically want to use bearer token authentication instead.</span></span> <span data-ttu-id="2ef82-172">Diese Anwendungstypen funktionieren nicht mit Cookies, können jedoch einfach ein Bearertoken abrufen und dieses in den Autorisierungsheader nachfolgender Anforderungen einfügen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-172">These types of applications do not work with cookies, but can easily retrieve a bearer token and include it in the authorization header of subsequent requests.</span></span> <span data-ttu-id="2ef82-173">Für die Tokenauthentifizierung unterstützt ASP.NET Core mehrere Optionen zur Verwendung von [OAuth 2.0](https://oauth.net/2/) und [OpenID Connect](https://openid.net/connect/).</span><span class="sxs-lookup"><span data-stu-id="2ef82-173">To enable token authentication, ASP.NET Core supports several options for using [OAuth 2.0](https://oauth.net/2/) and [OpenID Connect](https://openid.net/connect/).</span></span>

### <a name="authenticate-with-an-openid-connect-or-oauth-20-identity-provider"></a><span data-ttu-id="2ef82-174">Authentifizierung mit einem OpenID Connect- und OAuth 2.0-Identitätsanbieter</span><span class="sxs-lookup"><span data-stu-id="2ef82-174">Authenticate with an OpenID Connect or OAuth 2.0 Identity provider</span></span>

<span data-ttu-id="2ef82-175">Wenn Benutzerinformationen in Azure Active Directory oder einer anderen Identitätslösung gespeichert werden, die OpenID Connect oder OAuth 2.0 verwendet, können Sie das Paket **Microsoft.AspNetCore.Authentication.OpenIdConnect** für die Authentifizierung mithilfe des OpenID Connect-Workflows verwenden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-175">If user information is stored in Azure Active Directory or another identity solution that supports OpenID Connect or OAuth 2.0, you can use the **Microsoft.AspNetCore.Authentication.OpenIdConnect** package to authenticate using the OpenID Connect workflow.</span></span> <span data-ttu-id="2ef82-176">Um sich z.B. beim Identity.Api-Microservice in eShopOnContainers zu authentifizieren, kann eine ASP.NET Core-Webanwendung, wie in folgendem vereinfachtem Beispiel in `Startup.cs` gezeigt, Middleware aus diesem Paket verwenden:</span><span class="sxs-lookup"><span data-stu-id="2ef82-176">For example, to authenticate to the Identity.Api microservice in eShopOnContainers, an ASP.NET Core web application can use middleware from that package as shown in the following simplified example in `Startup.cs`:</span></span>

```csharp
// Startup.cs

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    // Configure the pipeline to use authentication
    app.UseAuthentication();
    //…
    app.UseMvc();
}

public void ConfigureServices(IServiceCollection services)
{
    var identityUrl = Configuration.GetValue<string>("IdentityUrl");
    var callBackUrl = Configuration.GetValue<string>("CallBackUrl");

    // Add Authentication services

    services.AddAuthentication(options =>
    {
        options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
    })
    .AddCookie()
    .AddOpenIdConnect(options =>
    {
        options.SignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.Authority = identityUrl;
        options.SignedOutRedirectUri = callBackUrl;
        options.ClientSecret = "secret";
        options.SaveTokens = true;
        options.GetClaimsFromUserInfoEndpoint = true;
        options.RequireHttpsMetadata = false;
        options.Scope.Add("openid");
        options.Scope.Add("profile");
        options.Scope.Add("orders");
        options.Scope.Add("basket");
        options.Scope.Add("marketing");
        options.Scope.Add("locations");
        options.Scope.Add("webshoppingagg");
        options.Scope.Add("orders.signalrhub");
    });
}
```

<span data-ttu-id="2ef82-177">Beachten Sie, dass wenn Sie diesen Workflow verwenden, die ASP.NET Core Identity-Middleware nicht erforderlich ist, da der gesamte Speicher und die Authentifizierung der Benutzerinformationen vom Identitätsdienst behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-177">Note that when you use this workflow, the ASP.NET Core Identity middleware is not needed, because all user information storage and authentication is handled by the Identity service.</span></span>

### <a name="issue-security-tokens-from-an-aspnet-core-service"></a><span data-ttu-id="2ef82-178">Ausstellen von Sicherheitstoken von einem ASP.NET Core-Dienst</span><span class="sxs-lookup"><span data-stu-id="2ef82-178">Issue security tokens from an ASP.NET Core service</span></span>

<span data-ttu-id="2ef82-179">Wenn Sie lieber Sicherheitstoken für lokale ASP.NET Core Identity-Benutzer ausstellen möchten, anstatt einen externen Identitätsanbieter zu verwenden, können Sie von einigen guten Bibliotheken von Drittanbietern profitieren.</span><span class="sxs-lookup"><span data-stu-id="2ef82-179">If you prefer to issue security tokens for local ASP.NET Core Identity users rather than using an external identity provider, you can take advantage of some good third-party libraries.</span></span>

<span data-ttu-id="2ef82-180">[IdentityServer4](https://github.com/IdentityServer/IdentityServer4) und [OpenIddict](https://github.com/openiddict/openiddict-core) sind OpenID Connect-Anbieter, die sich einfach in ASP.NET Core Identity integrieren lassen, damit Sie Sicherheitstoken von einem ASP.NET Core-Dienst ausstellen können.</span><span class="sxs-lookup"><span data-stu-id="2ef82-180">[IdentityServer4](https://github.com/IdentityServer/IdentityServer4) and [OpenIddict](https://github.com/openiddict/openiddict-core) are OpenID Connect providers that integrate easily with ASP.NET Core Identity to let you issue security tokens from an ASP.NET Core service.</span></span> <span data-ttu-id="2ef82-181">Die [IdentityServer4-Dokumentation](https://identityserver4.readthedocs.io/en/latest/) bietet detaillierte Anweisungen zur Verwendung der Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="2ef82-181">The [IdentityServer4 documentation](https://identityserver4.readthedocs.io/en/latest/) has in-depth instructions for using the library.</span></span> <span data-ttu-id="2ef82-182">Jedoch sind die grundlegenden Schritte zur Verwendung von IdentityServer4 zur Ausstellung von Token wie folgt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-182">However, the basic steps to using IdentityServer4 to issue tokens are as follows.</span></span>

1. <span data-ttu-id="2ef82-183">Sie können UseIdentityServer in der Startup.Configure-Methode aufrufen, um IdentityServer4 der HTTP_Anforderungsverarbeitungspipeline hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-183">You call app.UseIdentityServer in the Startup.Configure method to add IdentityServer4 to the application’s HTTP request processing pipeline.</span></span> <span data-ttu-id="2ef82-184">Dadurch kann die Bibliothek Anforderungen an OpenID Connect und OAuth2-Endpunkte wie „/connect/token“ verarbeiten</span><span class="sxs-lookup"><span data-stu-id="2ef82-184">This lets the library serve requests to OpenID Connect and OAuth2 endpoints like /connect/token.</span></span>

2. <span data-ttu-id="2ef82-185">Sie konfigurieren IdentityServer4 in Startup.ConfigureServices, indem Sie services.AddIdentityServer aufrufen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-185">You configure IdentityServer4 in Startup.ConfigureServices by making a call to services.AddIdentityServer.</span></span>

3. <span data-ttu-id="2ef82-186">Sie konfigurieren Identitätsserver, indem Sie folgende Daten bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="2ef82-186">You configure identity server by setting the following data:</span></span>

   - <span data-ttu-id="2ef82-187">Die zu verwendenden [Anmeldeinformationen](https://identityserver4.readthedocs.io/en/latest/topics/crypto.html) für die Registrierung.</span><span class="sxs-lookup"><span data-stu-id="2ef82-187">The [credentials](https://identityserver4.readthedocs.io/en/latest/topics/crypto.html) to use for signing.</span></span>

   - <span data-ttu-id="2ef82-188">Die [Identitäts- und API-Ressourcen](https://identityserver4.readthedocs.io/en/latest/topics/resources.html), auf die Benutzer möglicherweise Zugriff anfordern:</span><span class="sxs-lookup"><span data-stu-id="2ef82-188">The [Identity and API resources](https://identityserver4.readthedocs.io/en/latest/topics/resources.html) that users might request access to:</span></span>

      - <span data-ttu-id="2ef82-189">API-Ressourcen stellen geschützte Daten oder Funktionen dar, auf die ein Benutzer mit einem Zugriffstoken zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="2ef82-189">API resources represent protected data or functionality that a user can access with an access token.</span></span> <span data-ttu-id="2ef82-190">Ein Beispiel einer API-Ressource wäre eine Web-API (oder ein Satz von APIs), für die die Autorisierung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="2ef82-190">An example of an API resource would be a web API (or set of APIs) that requires authorization.</span></span>

      - <span data-ttu-id="2ef82-191">Identitätsressourcen stellen Informationen (Ansprüche) dar, die einem Client zur Identifizierung eines Benutzers übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-191">Identity resources represent information (claims) that are given to a client to identify a user.</span></span> <span data-ttu-id="2ef82-192">Die Ansprüche können den Benutzernamen, die E-Mail-Adresse usw. beinhalten.</span><span class="sxs-lookup"><span data-stu-id="2ef82-192">The claims might include the user name, email address, and so on.</span></span>

   - <span data-ttu-id="2ef82-193">Die [Clients](https://identityserver4.readthedocs.io/en/latest/topics/clients.html), die eine Verbindung herstellen, um Token anzufordern.</span><span class="sxs-lookup"><span data-stu-id="2ef82-193">The [clients](https://identityserver4.readthedocs.io/en/latest/topics/clients.html) that will be connecting in order to request tokens.</span></span>

   - <span data-ttu-id="2ef82-194">Der Speichermechanismus für Benutzerinformationen, z.B. [ASP.NET Core Identity](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html) oder eine Alternative.</span><span class="sxs-lookup"><span data-stu-id="2ef82-194">The storage mechanism for user information, such as [ASP.NET Core Identity](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html) or an alternative.</span></span>

<span data-ttu-id="2ef82-195">Wenn Sie Clients und Ressourcen angeben, die IdentityServer4 verwenden sollen, können Sie eine <xref:System.Collections.Generic.IEnumerable%601>-Auflistung der geeigneten Typen an Methoden übergeben, die einen In-Memory-Client oder Ressourcenspeicher übernehmen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-195">When you specify clients and resources for IdentityServer4 to use, you can pass an <xref:System.Collections.Generic.IEnumerable%601> collection of the appropriate type to methods that take in-memory client or resource stores.</span></span> <span data-ttu-id="2ef82-196">Für komplexere Szenarios können Sie auch Client- oder Ressourcenanbietertypen über eine Abhängigkeitsinjektion nutzen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-196">Or for more complex scenarios, you can provide client or resource provider types via Dependency Injection.</span></span>

<span data-ttu-id="2ef82-197">Eine Beispielkonfiguration für IdentityServer4 zur Verwendung von In-Memory-Ressourcen und -Clients, die von einem benutzerdefinierten IClientStore-Typen bereitgestellt werden, könnten wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="2ef82-197">A sample configuration for IdentityServer4 to use in-memory resources and clients provided by a custom IClientStore type might look like the following example:</span></span>

```csharp
// Add IdentityServer services
services.AddSingleton<IClientStore, CustomClientStore>();
services.AddIdentityServer()
    .AddSigningCredential("CN=sts")
    .AddInMemoryApiResources(MyApiResourceProvider.GetAllResources())
    .AddAspNetIdentity<ApplicationUser>();
```

### <a name="consume-security-tokens"></a><span data-ttu-id="2ef82-198">Nutzen von Sicherheitstoken</span><span class="sxs-lookup"><span data-stu-id="2ef82-198">Consume security tokens</span></span>

<span data-ttu-id="2ef82-199">Die Authentifizierung bei einem OpenID Connect-Endpunkt oder die Ausstellung Ihrer eigenen Sicherheitstoken deckt einige Szenarios ab.</span><span class="sxs-lookup"><span data-stu-id="2ef82-199">Authenticating against an OpenID Connect endpoint or issuing your own security tokens covers some scenarios.</span></span> <span data-ttu-id="2ef82-200">Was ist jedoch mit dem Dienst, der einfach nur den Zugriff für jene Benutzer einschränken muss, die über gültige Sicherheitstoken verfügen, die von einem anderen Dienst bereitgestellt wurden?</span><span class="sxs-lookup"><span data-stu-id="2ef82-200">But what about a service that simply needs to limit access to those users who have valid security tokens that were provided by a different service?</span></span>

<span data-ttu-id="2ef82-201">Für dieses Szenario ist die Middleware zur Authentifizierung, die JWT-Token behandelt, im **Microsoft.AspNetCore.Authentication.JwtBearer**-Paket verfügbar.</span><span class="sxs-lookup"><span data-stu-id="2ef82-201">For that scenario, authentication middleware that handles JWT tokens is available in the **Microsoft.AspNetCore.Authentication.JwtBearer** package.</span></span> <span data-ttu-id="2ef82-202">JWT steht für „[JSON Web Token](https://tools.ietf.org/html/rfc7519)“ und ist ein allgemeines Sicherheitstokenformat (definiert von RFC 7519) zum Kommunizieren von Sicherheitsansprüchen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-202">JWT stands for "[JSON Web Token](https://tools.ietf.org/html/rfc7519)" and is a common security token format (defined by RFC 7519) for communicating security claims.</span></span> <span data-ttu-id="2ef82-203">Vereinfacht sieht ein Beispiel zur Verwendung von Middleware zur Nutzung solcher Token etwa wie dieses Codefragment aus, das dem Ordering.Api-Microservice von eShopOnContainers entnommen ist.</span><span class="sxs-lookup"><span data-stu-id="2ef82-203">A simplified example of how to use middleware to consume such tokens might look like this code fragment, taken from the Ordering.Api microservice of eShopOnContainers.</span></span>

```csharp
// Startup.cs

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    // Configure the pipeline to use authentication
    app.UseAuthentication();
    //…
    app.UseMvc();
}

public void ConfigureServices(IServiceCollection services)
{
    var identityUrl = Configuration.GetValue<string>("IdentityUrl");

    // Add Authentication services

    services.AddAuthentication(options =>
    {
        options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;

    }).AddJwtBearer(options =>
    {
        options.Authority = identityUrl;
        options.RequireHttpsMetadata = false;
        options.Audience = "orders";
    });
}
```

<span data-ttu-id="2ef82-204">Die Parameter hier sind:</span><span class="sxs-lookup"><span data-stu-id="2ef82-204">The parameters in this usage are:</span></span>

- <span data-ttu-id="2ef82-205">`Audience` stellt den Empfänger des eingehenden Tokens oder der Ressource dar, für die das Token den Zugriff erteilt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-205">`Audience` represents the receiver of the incoming token or the resource that the token grants access to.</span></span> <span data-ttu-id="2ef82-206">Wenn der in diesem Wert angegebene Parameter nicht mit dem Parameter im Token übereinstimmt, wird das Token abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-206">If the value specified in this parameter does not match the parameter in the token, the token will be rejected.</span></span>

- <span data-ttu-id="2ef82-207">`Authority` ist die Adresse des Authentifizierungsservers, der Token ausgibt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-207">`Authority` is the address of the token-issuing authentication server.</span></span> <span data-ttu-id="2ef82-208">Die Middleware zur JWT-Bearerauthentifizierung verwendet diesen URI, um den öffentlichen Schlüssel abzurufen, der zur Überprüfung der Tokensignatur verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="2ef82-208">The JWT bearer authentication middleware uses this URI to get the public key that can be used to validate the token's signature.</span></span> <span data-ttu-id="2ef82-209">Die Middleware bestätigt auch, dass der `iss`-Parameter im Token mit diesem URI übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="2ef82-209">The middleware also confirms that the `iss` parameter in the token matches this URI.</span></span>

<span data-ttu-id="2ef82-210">Ein weiterer Parameter, `RequireHttpsMetadata`, ist für Testzwecke nützlich: Sie legen diesen Parameter auf FALSE fest, damit Sie Tests in Umgebungen durchführen können, in denen Sie keine Zertifikate besitzen.</span><span class="sxs-lookup"><span data-stu-id="2ef82-210">Another parameter, `RequireHttpsMetadata`, is useful for testing purposes; you set this parameter to false so you can test in environments where you don't have certificates.</span></span> <span data-ttu-id="2ef82-211">In realen Bereitstellungen dürfen JWT-Bearertoken immer nur über HTTPS übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="2ef82-211">In real-world deployments, JWT bearer tokens should always be passed only over HTTPS.</span></span>

<span data-ttu-id="2ef82-212">Wenn diese Middleware vorhanden ist, werden JWT-Token automatisch aus Autorisierungsheadern extrahiert.</span><span class="sxs-lookup"><span data-stu-id="2ef82-212">With this middleware in place, JWT tokens are automatically extracted from authorization headers.</span></span> <span data-ttu-id="2ef82-213">Sie werden anschließend deserialisiert, überprüft (mithilfe der Werte in den Parametern `Audience` und `Authority`) und als Benutzerinformation gespeichert, auf die später durch MVC-Aktionen oder Autorisierungsfilter verwiesen werden soll.</span><span class="sxs-lookup"><span data-stu-id="2ef82-213">They are then deserialized, validated (using the values in the `Audience` and `Authority` parameters), and stored as user information to be referenced later by MVC actions or authorization filters.</span></span>

<span data-ttu-id="2ef82-214">Die Middleware für die JWT-Bearerauthentifizierung kann auch erweiterte Szenarios unterstützen, beispielsweise die Verwendung eines lokalen Zertifikats zur Überprüfung eines Tokens, wenn die Registrierungsstelle nicht verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="2ef82-214">The JWT bearer authentication middleware can also support more advanced scenarios, such as using a local certificate to validate a token if the authority is not available.</span></span> <span data-ttu-id="2ef82-215">Für dieses Szenario können Sie ein `TokenValidationParameters`-Objekt im `JwtBearerOptions`-Objekt angeben.</span><span class="sxs-lookup"><span data-stu-id="2ef82-215">For this scenario, you can specify a `TokenValidationParameters` object in the `JwtBearerOptions` object.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ef82-216">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2ef82-216">Additional resources</span></span>

- <span data-ttu-id="2ef82-217">**Gemeinsames Verwenden von Cookies in mehreren Anwendungen** </span><span class="sxs-lookup"><span data-stu-id="2ef82-217">**Sharing cookies between applications** </span></span>\
  [https://docs.microsoft.com/aspnet/core/security/cookie-sharing](/aspnet/core/security/cookie-sharing)

- <span data-ttu-id="2ef82-218">**Einführung in Identität** </span><span class="sxs-lookup"><span data-stu-id="2ef82-218">**Introduction to Identity** </span></span>\
  [https://docs.microsoft.com/aspnet/core/security/authentication/identity](/aspnet/core/security/authentication/identity)

- <span data-ttu-id="2ef82-219">**Rick Anderson. Zweistufige Authentifizierung mit SMS** </span><span class="sxs-lookup"><span data-stu-id="2ef82-219">**Rick Anderson. Two-factor authentication with SMS** </span></span>\
  [https://docs.microsoft.com/aspnet/core/security/authentication/2fa](/aspnet/core/security/authentication/2fa)

- <span data-ttu-id="2ef82-220">**Enabling authentication using Facebook, Google and other external providers (Ermöglichen der Authentifizierung mit Facebook, Google und anderen externen Anbietern)**  </span><span class="sxs-lookup"><span data-stu-id="2ef82-220">**Enabling authentication using Facebook, Google and other external providers** </span></span>\
  [https://docs.microsoft.com/aspnet/core/security/authentication/social/](/aspnet/core/security/authentication/social/)

- <span data-ttu-id="2ef82-221">**Michell Anicas. An Introduction to OAuth 2 (Einführung in OAuth 2)**  </span><span class="sxs-lookup"><span data-stu-id="2ef82-221">**Michell Anicas. An Introduction to OAuth 2** </span></span>\
  <https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2>

- <span data-ttu-id="2ef82-222">**AspNet.Security.OAuth.Providers** (GitHub repo for ASP.NET OAuth providers) </span><span class="sxs-lookup"><span data-stu-id="2ef82-222">**AspNet.Security.OAuth.Providers** (GitHub repo for ASP.NET OAuth providers) </span></span>\
  <https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers/tree/dev/src>

- <span data-ttu-id="2ef82-223">**Danny Strockis. Integrating Azure AD into an ASP.NET Core web app (Integration von Azure AD in eine ASP.NET-Web-App)**  </span><span class="sxs-lookup"><span data-stu-id="2ef82-223">**Danny Strockis. Integrating Azure AD into an ASP.NET Core web app** </span></span>\
  <https://azure.microsoft.com/resources/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/>

- <span data-ttu-id="2ef82-224">**IdentityServer4. Offizielle Dokumentation** </span><span class="sxs-lookup"><span data-stu-id="2ef82-224">**IdentityServer4. Official documentation** </span></span>\
  <https://identityserver4.readthedocs.io/en/latest/>

>[!div class="step-by-step"]
><span data-ttu-id="2ef82-225">[Zurück](../implement-resilient-applications/monitor-app-health.md)
>[Weiter](authorization-net-microservices-web-applications.md)</span><span class="sxs-lookup"><span data-stu-id="2ef82-225">[Previous](../implement-resilient-applications/monitor-app-health.md)
[Next](authorization-net-microservices-web-applications.md)</span></span>