---
title: Wann sollte .NET Framework für Docker-Container verwendet werden?
description: .NET Microservicesarchitektur für .NET-Containeranwendungen | Wann sollte .NET Framework für Docker-Container verwendet werden?
ms.date: 01/07/2019
ms.openlocfilehash: 53164654710775320f023df9fb56a78506bd3a1a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675737"
---
# <a name="when-to-choose-net-framework-for-docker-containers"></a><span data-ttu-id="f2ed7-103">Wann sollte .NET Framework für Docker-Container verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="f2ed7-103">When to choose .NET Framework for Docker containers</span></span>

<span data-ttu-id="f2ed7-104">Während .NET Core erhebliche Vorteile für neue Anwendungen und Anwendungsmuster bietet, ist .NET Framework nach wie vor eine gute Wahl für viele vorhandene Szenarios.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-104">While .NET Core offers significant benefits for new applications and application patterns, .NET Framework will continue to be a good choice for many existing scenarios.</span></span>

## <a name="migrating-existing-applications-directly-to-a-windows-server-container"></a><span data-ttu-id="f2ed7-105">Direktes Migrieren vorhandener Anwendungen zu einem Windows Server-Container</span><span class="sxs-lookup"><span data-stu-id="f2ed7-105">Migrating existing applications directly to a Windows Server container</span></span>

<span data-ttu-id="f2ed7-106">Mithilfe von Docker-Containern können Sie die Bereitstellung vereinfachen, auch wenn Sie keine Microservices erstellen.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-106">You might want to use Docker containers just to simplify deployment, even if you are not creating microservices.</span></span> <span data-ttu-id="f2ed7-107">Wenn Sie beispielsweise den DevOps-Workflow mit Docker verbessern möchten, bieten Container besser isolierte Testumgebungen und können Bereitstellungsprobleme lösen, die durch fehlende Abhängigkeiten verursacht werden, wenn Sie in eine Produktionsumgebung wechseln.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-107">For example, perhaps you want to improve your DevOps workflow with Docker—containers can give you better isolated test environments and can also eliminate deployment issues caused by missing dependencies when you move to a production environment.</span></span> <span data-ttu-id="f2ed7-108">Wenn Sie eine monolithische Anwendung bereitstellen, ist es in solchen Fällen sinnvoll, Docker- und Windows-Container für die aktuellen .NET Framework-Anwendungen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-108">In cases like these, even if you are deploying a monolithic application, it makes sense to use Docker and Windows Containers for your current .NET Framework applications.</span></span>

<span data-ttu-id="f2ed7-109">In diesem Szenario müssen Sie Ihre vorhandenen Anwendungen in den meisten Fällen nicht zu .NET Core migrieren, sondern können einfach Docker-Container verwenden, die das traditionelle .NET Framework enthalten.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-109">In most cases for this scenario, you will not need to migrate your existing applications to .NET Core; you can use Docker containers that include the traditional .NET Framework.</span></span> <span data-ttu-id="f2ed7-110">Empfohlen wird jedoch, .NET Core zu verwenden, wenn Sie eine vorhandene Anwendung erweitern möchten, z.B. durch Schreiben eines neuen Diensts in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-110">However, a recommended approach is to use .NET Core as you extend an existing application, such as writing a new service in ASP.NET Core.</span></span>

## <a name="using-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a><span data-ttu-id="f2ed7-111">Verwenden von .NET-Bibliotheken von Drittanbietern oder NuGet-Paketen, die für .NET Core nicht verfügbar sind</span><span class="sxs-lookup"><span data-stu-id="f2ed7-111">Using third-party .NET libraries or NuGet packages not available for .NET Core</span></span>

<span data-ttu-id="f2ed7-112">[.NET Standard](../../../standard/net-standard.md) kommt in Drittanbieterbibliotheken immer häufiger zum Einsatz und ermöglicht die Codefreigabe in allen .NET-Varianten, einschließlich .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-112">Third-party libraries are quickly embracing the [.NET Standard](../../../standard/net-standard.md), which enables code sharing across all .NET flavors, including .NET Core.</span></span> <span data-ttu-id="f2ed7-113">In .NET Standard 2.0 und höher wurde die API-Oberflächenkompatibilität frameworkübergreifend deutlich erhöht, und Anwendungen können in .NET Core 2.x auch direkt auf vorhandene .NET Framework-Bibliotheken verweisen (siehe [.NET Framework 4.6.1 supporting .NET Standard 2.0](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#net-framework-461-supporting-net-standard-20), .NET Framework 4.6.1 mit Unterstützung für .NET Standard 2.0).</span><span class="sxs-lookup"><span data-stu-id="f2ed7-113">With the .NET Standard Library 2.0 and beyond the API surface compatibility across different frameworks has become significantly larger and in .NET Core 2.x applications can also directly reference existing .NET Framework libraries (see [.NET Framework 4.6.1 supporting .NET Standard 2.0](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#net-framework-461-supporting-net-standard-20)).</span></span>

<span data-ttu-id="f2ed7-114">Darüber hinaus wurde das [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md) im November 2017 veröffentlicht, um die für .NET Standard 2.0 unter Windows verfügbare API-Oberfläche zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-114">In addition, the [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md) was released on NOV-2017 to extend the API surface available for .NET Standard 2.0 on Windows.</span></span> <span data-ttu-id="f2ed7-115">Mit diesem Paket kann der größte Teil des vorhandenen Codes mit nur geringen oder ganz ohne Änderungen für .NET Standard 2.x neu kompiliert und unter Windows ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-115">This pack allows recompiling most existing code to .NET Standard 2.x with little or no modification, to run on Windows.</span></span>

<span data-ttu-id="f2ed7-116">Selbst bei diesen außergewöhnlichen Fortschritten seit .NET Standard 2.0 und .NET Core 2.1 können jedoch weiterhin Fälle auftreten, in denen bestimmte NuGet-Pakete nicht ohne Windows ausgeführt werden können und .NET Core nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-116">However, even with that exceptional progression since .NET Standard 2.0 and .NET Core 2.1, there might be cases where certain NuGet packages need Windows to run and might not support .NET Core.</span></span> <span data-ttu-id="f2ed7-117">Wenn diese Pakete von entscheidender Bedeutung für die Anwendung sind, müssen Sie .NET Framework in Windows-Containern verwenden.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-117">If those packages are critical for your application, then you will need to use .NET Framework on Windows Containers.</span></span>

## <a name="using-net-technologies-not-available-for-net-core"></a><span data-ttu-id="f2ed7-118">Verwenden von .NET-Technologien, die für .NET Core nicht verfügbar sind</span><span class="sxs-lookup"><span data-stu-id="f2ed7-118">Using .NET technologies not available for .NET Core</span></span> 

<span data-ttu-id="f2ed7-119">Einige .NET Framework-Technologien sind nicht in der aktuellen Version von .NET Core verfügbar (Version 2.2 bei Redaktionsschluss).</span><span class="sxs-lookup"><span data-stu-id="f2ed7-119">Some .NET Framework technologies are not available in the current version of .NET Core (version 2.2 as of this writing).</span></span> <span data-ttu-id="f2ed7-120">Einige werden in höheren .NET Core-Versionen verfügbar sein (.NET Core 2.x). Andere können jedoch nicht für die neuen Anwendungsmuster verwendet werden, auf die .NET Core ausgelegt ist, und werden möglicherweise nie verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-120">Some of them will be available in later .NET Core releases (.NET Core 2.x), but others do not apply to the new application patterns targeted by .NET Core and might never be available.</span></span>

<span data-ttu-id="f2ed7-121">In der folgenden Liste wird der Großteil der Technologien aufgezählt, die in .NET Core 2.x nicht verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="f2ed7-121">The following list shows most of the technologies that are not available in .NET Core 2.x:</span></span>

- <span data-ttu-id="f2ed7-122">ASP.NET Web Forms:</span><span class="sxs-lookup"><span data-stu-id="f2ed7-122">ASP.NET Web Forms.</span></span> <span data-ttu-id="f2ed7-123">Diese Technologie ist nur in .NET Framework verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-123">This technology is only available on .NET Framework.</span></span> <span data-ttu-id="f2ed7-124">Eine Integration von ASP.NET Web Forms in .NET Core ist zurzeit nicht geplant.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-124">Currently there are no plans to bring ASP.NET Web Forms to .NET Core.</span></span>

- <span data-ttu-id="f2ed7-125">WCF-Dienste:</span><span class="sxs-lookup"><span data-stu-id="f2ed7-125">WCF services.</span></span> <span data-ttu-id="f2ed7-126">Auch wenn eine [WCF-Clientbibliothek](https://github.com/dotnet/wcf) für die Nutzung durch WCF-Dienste von .NET Core verfügbar ist, ist die WCF-Serverimplementierung seit Mitte 2017 nur in .NET Framework verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-126">Even when a [WCF-Client library](https://github.com/dotnet/wcf) is available to consume WCF services from .NET Core, as of mid-2017, the WCF server implementation is only available on .NET Framework.</span></span> <span data-ttu-id="f2ed7-127">Dieses Szenario kann für zukünftige Versionen von .NET Core eine Rolle spielen, es gibt sogar Erwägungen, bestimmte APIs in das [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md) aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-127">This scenario might be considered for future releases of .NET Core, there are even some APIs considered for inclusion in the [Windows Compatibility Pack](../../../core/porting/windows-compat-pack.md).</span></span>

- <span data-ttu-id="f2ed7-128">Workflow-bezogene Dienste:</span><span class="sxs-lookup"><span data-stu-id="f2ed7-128">Workflow-related services.</span></span> <span data-ttu-id="f2ed7-129">Windows Workflow Foundation (WF), die Workflow-Dienste (WCF + WF in einem einzigen Dienst) und WCF Data Services (früher ADO.NET Data Services) sind nur in .NET Framework verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-129">Windows Workflow Foundation (WF), Workflow Services (WCF + WF in a single service), and WCF Data Services (formerly known as ADO.NET Data Services) are only available on .NET Framework.</span></span> <span data-ttu-id="f2ed7-130">Es ist zurzeit nicht vorgesehen, sie in .NET Core zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-130">There are currently no plans to bring them to .NET Core.</span></span>

<span data-ttu-id="f2ed7-131">Zusätzlich zu den in der offiziellen [Roadmap für .NET Core](https://github.com/aspnet/Home/wiki/Roadmap) aufgeführten Technologien werden möglicherweise andere Features zu .NET Core portiert.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-131">In addition to the technologies listed in the official [.NET Core roadmap](https://github.com/aspnet/Home/wiki/Roadmap), other features might be ported to .NET Core.</span></span> <span data-ttu-id="f2ed7-132">Eine vollständige Liste finden Sie auf der GitHub-CoreFX-Website. Die Elemente sind jeweils mit dem Tag [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core) versehen.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-132">For a full list, look at the items tagged as [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core) on the CoreFX GitHub site.</span></span> <span data-ttu-id="f2ed7-133">Beachten Sie, dass diese Liste keine Zusage von Microsoft darstellt, dass diese Komponenten in .NET Core integriert werden. In dieser Liste werden lediglich Anregungen der Community erfasst.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-133">Note that this list does not represent a commitment from Microsoft to bring those components to .NET Core — the items simply capture requests from the community.</span></span> <span data-ttu-id="f2ed7-134">Wenn Sie sich für eine der oben aufgeführten Komponenten interessieren, können Sie sich gern auf GitHub an den Diskussionen beteiligen.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-134">If you care about any of the components listed above, consider participating in the discussions on GitHub so that your voice can be heard.</span></span> <span data-ttu-id="f2ed7-135">Wenn Ihrer Ansicht nach noch etwas fehlt, [eröffnen Sie im CoreFX Repository ein neues „Issue“](https://github.com/dotnet/corefx/issues/new).</span><span class="sxs-lookup"><span data-stu-id="f2ed7-135">And if you think something is missing, please [file a new issue in the CoreFX repository](https://github.com/dotnet/corefx/issues/new).</span></span>

<span data-ttu-id="f2ed7-136">Zwar wird .NET Core 3 (zum Zeitpunkt der Erstellung dieses Texts in Arbeit) Unterstützung für eine große Zahl vorhandener .NET Framework-APIs beinhalten, diese sind aber desktoporientiert und bieten daher zurzeit keinen Nutzen in der Welt der Container.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-136">Even though .NET Core 3 (at the time of this writing this is in the works) will include support for a lot of existing .NET Framework APIs, these are desktop oriented so, currently, they are of no use in the container world.</span></span>

## <a name="using-a-platform-or-api-that-does-not-support-net-core"></a><span data-ttu-id="f2ed7-137">Verwenden einer Plattform oder API, die .NET Core nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="f2ed7-137">Using a platform or API that does not support .NET Core</span></span>

<span data-ttu-id="f2ed7-138">Einige Plattformen von Microsoft oder Drittanbietern unterstützen .NET Core nicht.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-138">Some Microsoft or third-party platforms do not support .NET Core.</span></span> <span data-ttu-id="f2ed7-139">Einige Azure-Dienste stellen beispielsweise ein SDK bereit, das noch nicht für die Nutzung in .NET Core verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-139">For example, some Azure services provide an SDK that is not yet available for consumption on .NET Core.</span></span> <span data-ttu-id="f2ed7-140">Dieses Problem ist jedoch nur vorübergehend, da alle Azure-Dienste letztendlich .NET Core verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-140">This is temporary, because all Azure services will eventually use .NET Core.</span></span> <span data-ttu-id="f2ed7-141">Das [Azure DocumentDB SDK für .NET Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/1.2.1) wurde z.B. als Vorschauversion am 16. November 2016 veröffentlicht und ist jetzt als stabile Version allgemein verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-141">For example, the [Azure DocumentDB SDK for .NET Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/1.2.1) was released as a preview on November 16, 2016, but it is now generally available (GA) as a stable version.</span></span>

<span data-ttu-id="f2ed7-142">Wenn eine der Plattformen oder einer der Dienste in Azure .NET Core weiterhin nicht mit der Client-API unterstützt, können Sie in der Zwischenzeit die entsprechende REST-API aus dem Azure-Dienst oder das Client SDK in .NET Framework verwenden.</span><span class="sxs-lookup"><span data-stu-id="f2ed7-142">In the meantime, if any platform or service in Azure still doesn't support .NET Core with its client API, you can use the equivalent REST API from the Azure service or the client SDK on .NET Framework.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="f2ed7-143">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f2ed7-143">Additional resources</span></span>

- <span data-ttu-id="f2ed7-144">**Leitfaden für .NET Core**</span><span class="sxs-lookup"><span data-stu-id="f2ed7-144">**.NET Core Guide**</span></span>  
    [https://docs.microsoft.com/dotnet/core/index](../../../core/index.md)

- <span data-ttu-id="f2ed7-145">**Portieren von .NET Framework zu .NET Core**</span><span class="sxs-lookup"><span data-stu-id="f2ed7-145">**Porting from .NET Framework to .NET Core**</span></span>  
    [https://docs.microsoft.com/dotnet/core/porting/index](../../../core/porting/index.md)

- <span data-ttu-id="f2ed7-146">**Einführung zu .NET und Docker** [https://docs.microsoft.com/dotnet/core/docker/intro-net-docker](../../../core/docker/intro-net-docker.md)</span><span class="sxs-lookup"><span data-stu-id="f2ed7-146">**.NET Core on Docker Guide** [https://docs.microsoft.com/dotnet/core/docker/intro-net-docker](../../../core/docker/intro-net-docker.md)</span></span>

- <span data-ttu-id="f2ed7-147">**.NET-Komponenten – Übersicht**</span><span class="sxs-lookup"><span data-stu-id="f2ed7-147">**.NET Components Overview**</span></span>  
    [https://docs.microsoft.com/dotnet/standard/components](../../../standard/components.md)

>[!div class="step-by-step"]
><span data-ttu-id="f2ed7-148">[Zurück](net-core-container-scenarios.md)
>[Weiter](container-framework-choice-factors.md)</span><span class="sxs-lookup"><span data-stu-id="f2ed7-148">[Previous](net-core-container-scenarios.md)
[Next](container-framework-choice-factors.md)</span></span>