---
ms.openlocfilehash: 959f3959c28c7d0159be7a213986345e2865b9a2
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394437"
---
### <a name="shared-framework-removed-microsoftaspnetcoreall"></a><span data-ttu-id="ea18a-101">Freigegebenes Framework: Microsoft.AspNetCore.All wurde entfernt</span><span class="sxs-lookup"><span data-stu-id="ea18a-101">Shared framework: Removed Microsoft.AspNetCore.All</span></span>

<span data-ttu-id="ea18a-102">Ab ASP.NET Core 3.0 werden das Metapaket `Microsoft.AspNetCore.All` und das entsprechende freigegebene Framework `Microsoft.AspNetCore.All` nicht mehr erstellt.</span><span class="sxs-lookup"><span data-stu-id="ea18a-102">Starting in ASP.NET Core 3.0, the `Microsoft.AspNetCore.All` metapackage and the matching `Microsoft.AspNetCore.All` shared framework are no longer produced.</span></span> <span data-ttu-id="ea18a-103">Dieses Paket ist in ASP.NET Core 2.2 verfügbar und wird auch weiterhin mit Wartungsupdates in ASP.NET Core 2.1 versorgt.</span><span class="sxs-lookup"><span data-stu-id="ea18a-103">This package is available in ASP.NET Core 2.2 and will continue to receive servicing updates in ASP.NET Core 2.1.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="ea18a-104">Eingeführt in Version</span><span class="sxs-lookup"><span data-stu-id="ea18a-104">Version introduced</span></span>

<span data-ttu-id="ea18a-105">3.0</span><span class="sxs-lookup"><span data-stu-id="ea18a-105">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="ea18a-106">Altes Verhalten</span><span class="sxs-lookup"><span data-stu-id="ea18a-106">Old behavior</span></span>

<span data-ttu-id="ea18a-107">Apps konnten das Metapaket `Microsoft.AspNetCore.All` verwenden, um das freigegebene Framework `Microsoft.AspNetCore.All` als Ziel in .NET Core zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ea18a-107">Apps could use the `Microsoft.AspNetCore.All` metapackage to target the `Microsoft.AspNetCore.All` shared framework on .NET Core.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="ea18a-108">Neues Verhalten</span><span class="sxs-lookup"><span data-stu-id="ea18a-108">New behavior</span></span>

<span data-ttu-id="ea18a-109">.NET Core 3.0 enthält das freigegebene Framework `Microsoft.AspNetCore.All` nicht mehr.</span><span class="sxs-lookup"><span data-stu-id="ea18a-109">.NET Core 3.0 doesn't include a `Microsoft.AspNetCore.All` shared framework.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="ea18a-110">Grund für die Änderung</span><span class="sxs-lookup"><span data-stu-id="ea18a-110">Reason for change</span></span>

<span data-ttu-id="ea18a-111">Das Metapaket `Microsoft.AspNetCore.All` enthielt eine große Anzahl externer Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="ea18a-111">The `Microsoft.AspNetCore.All` metapackage included a large number of external dependencies.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="ea18a-112">Empfohlene Maßnahme</span><span class="sxs-lookup"><span data-stu-id="ea18a-112">Recommended action</span></span>

<span data-ttu-id="ea18a-113">Stellen Sie Ihr Projekt auf die Verwendung des Frameworks `Microsoft.AspNetCore.App` um.</span><span class="sxs-lookup"><span data-stu-id="ea18a-113">Migrate your project to use the `Microsoft.AspNetCore.App` framework.</span></span> <span data-ttu-id="ea18a-114">Komponenten, die zuvor in `Microsoft.AspNetCore.All` verfügbar waren, sind weiterhin in NuGet verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ea18a-114">Components that were previously available in `Microsoft.AspNetCore.All` are still available on NuGet.</span></span> <span data-ttu-id="ea18a-115">Diese Komponenten werden nun mit Ihrer App bereitgestellt, anstatt in das freigegebene Framework eingefügt zu werden.</span><span class="sxs-lookup"><span data-stu-id="ea18a-115">Those components are now deployed with your app instead of being included in the shared framework.</span></span>

#### <a name="category"></a><span data-ttu-id="ea18a-116">Kategorie</span><span class="sxs-lookup"><span data-stu-id="ea18a-116">Category</span></span>

<span data-ttu-id="ea18a-117">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ea18a-117">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="ea18a-118">Betroffene APIs</span><span class="sxs-lookup"><span data-stu-id="ea18a-118">Affected APIs</span></span>

<span data-ttu-id="ea18a-119">Keine</span><span class="sxs-lookup"><span data-stu-id="ea18a-119">None</span></span>

<!-- 

#### Affected APIs

Not detectable via API analysis

-->