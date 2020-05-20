---
title: '.NET Core-Projekt-SDKs: Übersicht'
description: Erfahren Sie mehr über .NET Core-Projekt-SDKs.
ms.date: 02/02/2020
ms.topic: conceptual
ms.openlocfilehash: d0ac01dca31dffea482745126e00c34b1da20774
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389668"
---
# <a name="net-core-project-sdks"></a><span data-ttu-id="b1ce5-103">.NET Core-Projekt-SDKs</span><span class="sxs-lookup"><span data-stu-id="b1ce5-103">.NET Core project SDKs</span></span>

<span data-ttu-id="b1ce5-104">.NET Core-Projekten ist ein SDK (Software Development Kit) zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-104">.NET Core projects are associated with a software development kit (SDK).</span></span> <span data-ttu-id="b1ce5-105">Jedes *Projekt-SDK* besteht aus einer Reihe von MSBuild-[Zielen](/visualstudio/msbuild/msbuild-targets) und zugehörigen [Tasks](/visualstudio/msbuild/msbuild-tasks), mit denen Code kompiliert, paketiert und veröffentlicht wird.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-105">Each *project SDK* is a set of MSBuild [targets](/visualstudio/msbuild/msbuild-targets) and associated [tasks](/visualstudio/msbuild/msbuild-tasks) that are responsible for compiling, packing, and publishing code.</span></span> <span data-ttu-id="b1ce5-106">Ein Projekt, das auf ein Projekt-SDK verweist, wird zuweilen auch als *Projekt im SDK-Stil* bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-106">A project that references a project SDK is sometimes referred to as an *SDK-style project*.</span></span>

## <a name="available-sdks"></a><span data-ttu-id="b1ce5-107">Verfügbare SDKs</span><span class="sxs-lookup"><span data-stu-id="b1ce5-107">Available SDKs</span></span>

<span data-ttu-id="b1ce5-108">Für .NET Core sind die folgenden SDKs verfügbar:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-108">The following SDKs are available for .NET Core:</span></span>

| <span data-ttu-id="b1ce5-109">Id</span><span class="sxs-lookup"><span data-stu-id="b1ce5-109">ID</span></span> | <span data-ttu-id="b1ce5-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b1ce5-110">Description</span></span> | <span data-ttu-id="b1ce5-111">Repository</span><span class="sxs-lookup"><span data-stu-id="b1ce5-111">Repo</span></span>|
| - | - | - |
| `Microsoft.NET.Sdk` | <span data-ttu-id="b1ce5-112">Das .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="b1ce5-112">The .NET Core SDK</span></span> | https://github.com/dotnet/sdk |
| `Microsoft.NET.Sdk.Web` | <span data-ttu-id="b1ce5-113">Das .NET Core [Web SDK](/aspnet/core/razor-pages/web-sdk)</span><span class="sxs-lookup"><span data-stu-id="b1ce5-113">The .NET Core [Web SDK](/aspnet/core/razor-pages/web-sdk)</span></span> | https://github.com/aspnet/websdk |
| `Microsoft.NET.Sdk.Razor` | <span data-ttu-id="b1ce5-114">Das .NET Core [Razor SDK](/aspnet/core/razor-pages/sdk)</span><span class="sxs-lookup"><span data-stu-id="b1ce5-114">The .NET Core [Razor SDK](/aspnet/core/razor-pages/sdk)</span></span> |
| `Microsoft.NET.Sdk.Worker` | <span data-ttu-id="b1ce5-115">Das .NET Core Worker Service SDK</span><span class="sxs-lookup"><span data-stu-id="b1ce5-115">The .NET Core Worker Service SDK</span></span> |
| `Microsoft.NET.Sdk.WindowsDesktop` | <span data-ttu-id="b1ce5-116">Das .NET Core WinForms and WPF SDK</span><span class="sxs-lookup"><span data-stu-id="b1ce5-116">The .NET Core WinForms and WPF SDK</span></span> |

<span data-ttu-id="b1ce5-117">Das .NET Core SDK ist das Basis-SDK für .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-117">The .NET Core SDK is the base SDK for .NET Core.</span></span> <span data-ttu-id="b1ce5-118">Die anderen SDKs verweisen auf das .NET Core SDK, und Projekten, die den anderen SDKs zugeordnet sind, stehen alle .NET Core SDK-Eigenschaften zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-118">The other SDKs reference the .NET Core SDK, and projects that are associated with the other SDKs have all the .NET Core SDK properties available to them.</span></span> <span data-ttu-id="b1ce5-119">Das Web SDK hängt z. B. sowohl vom .NET Core SDK als auch vom Razor SDK ab.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-119">The Web SDK, for example, depends on both the .NET Core SDK and the Razor SDK.</span></span>

<span data-ttu-id="b1ce5-120">Sie können auch selbst ein SDK erstellen, das über NuGet verteilt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-120">You can also author your own SDK that can be distributed via NuGet.</span></span>

## <a name="project-files"></a><span data-ttu-id="b1ce5-121">Projektdateien</span><span class="sxs-lookup"><span data-stu-id="b1ce5-121">Project files</span></span>

<span data-ttu-id="b1ce5-122">.NET Core-Projekte basieren auf dem [MSBuild](/visualstudio/msbuild/msbuild)-Format.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-122">.NET Core projects are based on the [MSBuild](/visualstudio/msbuild/msbuild) format.</span></span> <span data-ttu-id="b1ce5-123">Projektdateien mit der Erweiterung *.csproj* für C#-Projekte und *.fsproj* für F#-Projekte, weisen das XML-Format auf.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-123">Project files, which have extensions like *.csproj* for C# projects and *.fsproj* for F# projects, are in XML format.</span></span> <span data-ttu-id="b1ce5-124">Das Stammelement einer MSBuild-Projektdatei ist das Element [Project](/visualstudio/msbuild/project-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="b1ce5-124">The root element of an MSBuild project file is the [Project](/visualstudio/msbuild/project-element-msbuild) element.</span></span> <span data-ttu-id="b1ce5-125">Das `Project`-Element besitzt ein optionales `Sdk`-Attribut, das angibt, welches SDK (und welche Version) verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-125">The `Project` element has an optional `Sdk` attribute that specifies which SDK (and version) to use.</span></span> <span data-ttu-id="b1ce5-126">Um die .NET Core-Tools zu verwenden und Ihren Code zu erstellen, legen Sie das `Sdk`-Attribut auf eine der IDs in der Tabelle [Verfügbare SDKs](#available-sdks) fest.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-126">To use the .NET Core tools and build your code, set the `Sdk` attribute to one of the IDs in the [Available SDKs](#available-sdks) table.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  ...
</Project>
```

<span data-ttu-id="b1ce5-127">Um ein aus NuGet stammendes SDK anzugeben, schließen Sie die Version am Ende des Namens ein, oder geben Sie den Namen und die Version in der Datei *global.json* an.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-127">To specify an SDK that comes from NuGet, include the version at the end of the name, or specify the name and version in the *global.json* file.</span></span>

```xml
<Project Sdk="MSBuild.Sdk.Extras/2.0.54">
  ...
</Project>
```

<span data-ttu-id="b1ce5-128">Das [Sdk](/visualstudio/msbuild/sdk-element-msbuild)-Element auf der obersten Ebene ist eine weitere Möglichkeit, das SDK anzugeben:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-128">Another way to specify the SDK is with the top-level [Sdk](/visualstudio/msbuild/sdk-element-msbuild) element:</span></span>

```xml
<Project>
  <Sdk Name="Microsoft.NET.Sdk" />
  ...
</Project>
```

<span data-ttu-id="b1ce5-129">Indem mit einer dieser Möglichkeiten auf ein SDK verwiesen wird, werden Projektdateien für .NET Core erheblich vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-129">Referencing an SDK in one of these ways greatly simplifies project files for .NET Core.</span></span> <span data-ttu-id="b1ce5-130">Während der Auswertung des Projekts fügt MSBuild implizite Importe in der Projektdatei hinzu: im oberen Bereich für `Sdk.props`, im unteren Bereich für `Sdk.targets`.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-130">While evaluating the project, MSBuild adds implicit imports for `Sdk.props` at the top of the project file and `Sdk.targets` at the bottom.</span></span>

```xml
<Project>
  <!-- Implicit top import -->
  <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />
  ...
  <!-- Implicit bottom import -->
  <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />
</Project>
```

> [!TIP]
> <span data-ttu-id="b1ce5-131">Auf einem Windows-Computer befinden sich die Dateien *Sdk.props* und *Sdk.targets* im Ordner *%ProgramFiles%\dotnet\sdk\\[version]\Sdks\Microsoft.NET.Sdk\Sdk*.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-131">On a Windows machine, the *Sdk.props* and *Sdk.targets* files can be found in the *%ProgramFiles%\dotnet\sdk\\[version]\Sdks\Microsoft.NET.Sdk\Sdk* folder.</span></span>

### <a name="preprocess-the-project-file"></a><span data-ttu-id="b1ce5-132">Vorverarbeiten der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="b1ce5-132">Preprocess the project file</span></span>

<span data-ttu-id="b1ce5-133">Mithilfe des Befehls `dotnet msbuild -preprocess` können Sie ein vollständig erweitertes Projekt so anzeigen, wie es für MSBuild dargestellt wird, nachdem das SDK und die zugehörigen Ziele angegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-133">You can see the fully expanded project as MSBuild sees it after the SDK and its targets are included by using the `dotnet msbuild -preprocess` command.</span></span> <span data-ttu-id="b1ce5-134">Die Option [preprocess](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) des Befehls [`dotnet msbuild`](../tools/dotnet-msbuild.md) zeigt die importierten Dateien, ihre Quellen und ihren Beitrag zum Build, ohne das Projekt tatsächlich zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-134">The [preprocess](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) switch of the [`dotnet msbuild`](../tools/dotnet-msbuild.md) command shows which files are imported, their sources, and their contributions to the build without actually building the project.</span></span>

<span data-ttu-id="b1ce5-135">Wenn das Projekt mehrere Zielframeworks umfasst, geben Sie die Ergebnisse des Befehls nur für ein Framework aus, indem Sie dieses als MSBuild-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-135">If the project has multiple target frameworks, focus the results of the command on only one framework by specifying it as an MSBuild property.</span></span> <span data-ttu-id="b1ce5-136">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-136">For example:</span></span>

`dotnet msbuild -property:TargetFramework=netcoreapp2.0 -preprocess:output.xml`

### <a name="default-compilation-includes"></a><span data-ttu-id="b1ce5-137">Standardmäßige Includedateien für die Kompilierung</span><span class="sxs-lookup"><span data-stu-id="b1ce5-137">Default compilation includes</span></span>

<span data-ttu-id="b1ce5-138">Die standardmäßigen Include- und Excludedateien für Compile-Elemente und eingebettete Ressourcen sind im SDK definiert.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-138">The default includes and excludes for compile items and embedded resources are defined in the SDK.</span></span> <span data-ttu-id="b1ce5-139">Im Gegensatz zu SDK-Projekten, die nicht das .NET Framework als Ziel verwenden, müssen Sie diese Elemente nicht in Ihrer Projektdatei angeben, da die Standardwerte die meisten gängigen Anwendungsfälle abdecken.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-139">Unlike non-SDK .NET Framework projects, you don't need to specify these items in your project file, because the defaults cover most common use cases.</span></span> <span data-ttu-id="b1ce5-140">Dies führt zu kleineren Projektdateien, die einfacher zu verstehen und bei Bedarf auch manuell zu bearbeiten sind.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-140">This leads to smaller project files that are easier to understand as well as edit by hand, if needed.</span></span>

<span data-ttu-id="b1ce5-141">Die folgende Tabelle zeigt, welche Elemente und welche [Globs](https://en.wikipedia.org/wiki/Glob_(programming)) im .NET Core SDK enthalten und ausgeschlossen sind:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-141">The following table shows which element and which [globs](https://en.wikipedia.org/wiki/Glob_(programming)) are included and excluded in the .NET Core SDK:</span></span>

| <span data-ttu-id="b1ce5-142">Element</span><span class="sxs-lookup"><span data-stu-id="b1ce5-142">Element</span></span>           | <span data-ttu-id="b1ce5-143">Glob einschließen</span><span class="sxs-lookup"><span data-stu-id="b1ce5-143">Include glob</span></span>                              | <span data-ttu-id="b1ce5-144">Glob ausschließen</span><span class="sxs-lookup"><span data-stu-id="b1ce5-144">Exclude glob</span></span>                                                  | <span data-ttu-id="b1ce5-145">Glob entfernen</span><span class="sxs-lookup"><span data-stu-id="b1ce5-145">Remove glob</span></span>              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|--------------------------|
| <span data-ttu-id="b1ce5-146">Compile</span><span class="sxs-lookup"><span data-stu-id="b1ce5-146">Compile</span></span>           | <span data-ttu-id="b1ce5-147">\*\*/\*.cs (oder andere Spracherweiterungen)</span><span class="sxs-lookup"><span data-stu-id="b1ce5-147">\*\*/\*.cs (or other language extensions)</span></span> | <span data-ttu-id="b1ce5-148">\*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="b1ce5-148">\*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc</span></span>  | <span data-ttu-id="b1ce5-149">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="b1ce5-149">N/A</span></span>                      |
| <span data-ttu-id="b1ce5-150">EmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="b1ce5-150">EmbeddedResource</span></span>  | <span data-ttu-id="b1ce5-151">\*\*/\*.resx</span><span class="sxs-lookup"><span data-stu-id="b1ce5-151">\*\*/\*.resx</span></span>                              | <span data-ttu-id="b1ce5-152">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="b1ce5-152">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="b1ce5-153">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="b1ce5-153">N/A</span></span>                      |
| <span data-ttu-id="b1ce5-154">Keine</span><span class="sxs-lookup"><span data-stu-id="b1ce5-154">None</span></span>              | \*\*/\*                                   | <span data-ttu-id="b1ce5-155">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="b1ce5-155">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="b1ce5-156">\*\*/\*.cs; \*\*/\*.resx</span><span class="sxs-lookup"><span data-stu-id="b1ce5-156">\*\*/\*.cs; \*\*/\*.resx</span></span> |

> [!NOTE]
> <span data-ttu-id="b1ce5-157">Die Ordner `./bin` und `./obj` aus, die von den MSBuild-Eigenschaften `$(BaseOutputPath)` und `$(BaseIntermediateOutputPath)` dargestellt werden, sind standardmäßig von den Globs ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-157">The `./bin` and `./obj` folders, which are represented by the `$(BaseOutputPath)` and `$(BaseIntermediateOutputPath)` MSBuild properties, are excluded from the globs by default.</span></span> <span data-ttu-id="b1ce5-158">Excludedateien werden durch die Eigenschaft `$(DefaultItemExcludes)` dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-158">Excludes are represented by the property `$(DefaultItemExcludes)`.</span></span>

<span data-ttu-id="b1ce5-159">Wenn Sie diese Elemente explizit in Ihrer Projektdatei definieren, erhalten Sie wahrscheinlich folgenden Fehler:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-159">If you explicitly define these items in your project file, you're likely to get the following error:</span></span>

<span data-ttu-id="b1ce5-160">**Doppelte Compile-Elemente waren enthalten. .NET SDK enthält Compile-Elemente aus Ihrem Projektverzeichnis in der Standardeinstellung. Sie können diese Elemente aus Ihrer Projektdatei entfernen oder die Eigenschaft „EnableDefaultCompileItems“ auf FALSE festlegen, wenn Sie sie explizit in Ihrer Projektdatei einschließen möchten.**</span><span class="sxs-lookup"><span data-stu-id="b1ce5-160">**Duplicate Compile items were included. The .NET SDK includes Compile items from your project directory by default. You can either remove these items from your project file, or set the 'EnableDefaultCompileItems' property to 'false' if you want to explicitly include them in your project file.**</span></span>

<span data-ttu-id="b1ce5-161">Um diesen Fehler zu beheben, entfernen Sie entweder die expliziten `Compile`-Elemente, die den in der obigen Tabelle aufgeführten impliziten Elementen entsprechen, oder legen Sie die `EnableDefaultCompileItems`-Eigenschaft auf `false` fest, wodurch der implizite Einschluss deaktiviert wird:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-161">To resolve the error, either remove the explicit `Compile` items that match the implicit ones listed on the previous table, or set the `EnableDefaultCompileItems` property to `false`, which disables implicit inclusion:</span></span>

```xml
<PropertyGroup>
  <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```

<span data-ttu-id="b1ce5-162">Wenn Sie z. B. einige Dateien angeben möchten, die mit Ihrer Anwendung veröffentlicht werden sollen, können Sie weiterhin die bekannten MSBuild-Mechanismen dafür verwenden, wie etwa das `Content`-Element.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-162">If you want to specify, for example, some files to get published with your app, you can still use the known MSBuild mechanisms for that, for example, the `Content` element.</span></span>

<span data-ttu-id="b1ce5-163">`EnableDefaultCompileItems` deaktiviert nur `Compile`-Globs, wirkt sich jedoch nicht auf andere Globs wie das implizite `None`-Glob aus, das ebenfalls für \*.cs-Elemente gilt.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-163">`EnableDefaultCompileItems` only disables `Compile` globs but doesn't affect other globs, like the implicit `None` glob that also applies to \*.cs items.</span></span> <span data-ttu-id="b1ce5-164">Aus diesem Grund zeigt der Projektmappen-Explorer in Visual Studio die \*.cs-Elemente weiterhin als Teil des Projekts an, eingeschlossen als `None`-Elemente.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-164">Because of that, Solution Explorer in Visual Studio shows \*.cs items as part of the project, included as `None` items.</span></span> <span data-ttu-id="b1ce5-165">Um das implizite `None`-Glob zu deaktivieren, legen Sie `EnableDefaultNoneItems` auf `false` fest:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-165">To disable the implicit `None` glob, set `EnableDefaultNoneItems` to `false`:</span></span>

```xml
<PropertyGroup>
  <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
</PropertyGroup>
```

<span data-ttu-id="b1ce5-166">Um *alle* impliziten Globs zu deaktivieren, legen Sie die `EnableDefaultItems`-Eigenschaft auf `false` fest:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-166">To disable *all* implicit globs, set the `EnableDefaultItems` property to `false`:</span></span>

```xml
<PropertyGroup>
  <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

## <a name="customize-the-build"></a><span data-ttu-id="b1ce5-167">Anpassen des Builds</span><span class="sxs-lookup"><span data-stu-id="b1ce5-167">Customize the build</span></span>

<span data-ttu-id="b1ce5-168">Es gibt verschiedene Möglichkeiten, [einen Build anzupassen](/visualstudio/msbuild/customize-your-build).</span><span class="sxs-lookup"><span data-stu-id="b1ce5-168">There are various ways to [customize a build](/visualstudio/msbuild/customize-your-build).</span></span> <span data-ttu-id="b1ce5-169">Sie können eine Eigenschaft überschreiben, indem Sie sie als Argument an einen [msbuild](/visualstudio/msbuild/msbuild-command-line-reference)- oder [dotnet](../tools/index.md)-Befehl übergeben.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-169">You may want to override a property by passing it as an argument to an [msbuild](/visualstudio/msbuild/msbuild-command-line-reference) or [dotnet](../tools/index.md) command.</span></span> <span data-ttu-id="b1ce5-170">Sie können die Eigenschaft auch zur Projektdatei oder zu einer *Directory.Build.props*-Datei hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-170">You can also add the property to the project file or to a *Directory.Build.props* file.</span></span> <span data-ttu-id="b1ce5-171">Eine Liste mit nützlichen Eigenschaften für .NET Core-Projekte finden Sie unter [MSBuild-Eigenschaften für .NET Core SDK-Projekte](msbuild-props.md).</span><span class="sxs-lookup"><span data-stu-id="b1ce5-171">For a list of useful properties for .NET Core projects, see [MSBuild properties for .NET Core SDK projects](msbuild-props.md).</span></span>

### <a name="custom-targets"></a><span data-ttu-id="b1ce5-172">Benutzerdefinierte Ziele</span><span class="sxs-lookup"><span data-stu-id="b1ce5-172">Custom targets</span></span>

<span data-ttu-id="b1ce5-173">.NET Core-Projekte können benutzerdefinierte MSBuild-Ziele und -Eigenschaften für Projekte paketieren, die das Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-173">.NET Core projects can package custom MSBuild targets and properties for use by projects that consume the package.</span></span> <span data-ttu-id="b1ce5-174">Verwenden Sie diese Art der Erweiterbarkeit, wenn Sie Folgendes vorhaben:</span><span class="sxs-lookup"><span data-stu-id="b1ce5-174">Use this type of extensibility when you want to:</span></span>

- <span data-ttu-id="b1ce5-175">Erweitern des Buildprozesses</span><span class="sxs-lookup"><span data-stu-id="b1ce5-175">Extend the build process.</span></span>
- <span data-ttu-id="b1ce5-176">Zugreifen auf Artefakte des Buildprozesses, z. B. generierte Dateien</span><span class="sxs-lookup"><span data-stu-id="b1ce5-176">Access artifacts of the build process, such as generated files.</span></span>
- <span data-ttu-id="b1ce5-177">Untersuchen einer Konfiguration, in der der Build aufgerufen wird</span><span class="sxs-lookup"><span data-stu-id="b1ce5-177">Inspect the configuration under which the build is invoked.</span></span>

<span data-ttu-id="b1ce5-178">Sie fügen benutzerdefinierte Buildziele oder -eigenschaften hinzu, indem Sie Dateien im Format `<package_id>.targets` oder `<package_id>.props` (z. B.`Contoso.Utility.UsefulStuff.targets`) im *build*-Ordner des Projekts platzieren.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-178">You add custom build targets or properties by placing files in the form `<package_id>.targets` or `<package_id>.props` (for example, `Contoso.Utility.UsefulStuff.targets`) in the *build* folder of the project.</span></span>

<span data-ttu-id="b1ce5-179">Der XML-Code ist ein Codeausschnitt aus einer *.csproj*-Datei, die den Befehl [`dotnet pack`](../tools/dotnet-pack.md) anweist, was paketiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-179">The following XML is a snippet from a *.csproj* file that instructs the [`dotnet pack`](../tools/dotnet-pack.md) command what to package.</span></span> <span data-ttu-id="b1ce5-180">Das Element `<ItemGroup Label="dotnet pack instructions">` platziert die Zieledateien innerhalb des Pakets in den Ordner *build*.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-180">The `<ItemGroup Label="dotnet pack instructions">` element places the targets files into the *build* folder inside the package.</span></span> <span data-ttu-id="b1ce5-181">Das Element `<Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">` platziert die Assemblys und *.json*-Dateien in den Ordner *build*.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-181">The `<Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">` element places the assemblies and *.json* files into the *build* folder.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  ...
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  ...
  
</Project>
```

<span data-ttu-id="b1ce5-182">Damit ein benutzerdefiniertes Ziel in Ihrem Projekt genutzt werden kann, fügen Sie ein `PackageReference`-Element hinzu, das auf das Paket und dessen Version zeigt.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-182">To consume a custom target in your project, add a `PackageReference` element that points to the package and its version.</span></span> <span data-ttu-id="b1ce5-183">Im Gegensatz zu den Tools wird das benutzerdefinierte Zielpaket in die Abhängigkeiten des nutzenden Projekts eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-183">Unlike the tools, the custom targets package is included in the consuming project's dependency closure.</span></span>

<span data-ttu-id="b1ce5-184">Sie können konfigurieren, wie das benutzerdefinierte Ziel genutzt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-184">You can configure how to use the custom target.</span></span> <span data-ttu-id="b1ce5-185">Da es sich um ein MSBuild-Ziel handelt, kann es von einem angegebenen Ziel abhängig sein, nach einem anderen Ziel ausgeführt werden oder mit dem Befehl `dotnet msbuild -t:<target-name>` manuell aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-185">Since it's an MSBuild target, it can depend on a given target, run after another target, or be manually invoked by using the `dotnet msbuild -t:<target-name>` command.</span></span> <span data-ttu-id="b1ce5-186">Wenn Sie jedoch ein besseres Benutzererlebnis bieten möchten, können Sie projektbezogene Tools und benutzerdefinierte Ziele kombinieren.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-186">However, to provide a better user experience, you can combine per-project tools and custom targets.</span></span> <span data-ttu-id="b1ce5-187">In diesem Szenario akzeptiert das projektbezogene Tool alle erforderlichen Parameter und übersetzt diese in den erforderlichen [`dotnet msbuild`](../tools/dotnet-msbuild.md)-Aufruf, der das Ziel ausführt.</span><span class="sxs-lookup"><span data-stu-id="b1ce5-187">In this scenario, the per-project tool accepts whatever parameters are needed and translates that into the required [`dotnet msbuild`](../tools/dotnet-msbuild.md) invocation that executes the target.</span></span> <span data-ttu-id="b1ce5-188">Sie sehen ein Beispiel dieser Art von Synergie im Repository mit den [MVP Summit 2016 Hackathon-Beispielen](https://github.com/dotnet/MVPSummitHackathon2016) im Projekt [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer).</span><span class="sxs-lookup"><span data-stu-id="b1ce5-188">You can see a sample of this kind of synergy on the [MVP Summit 2016 Hackathon samples](https://github.com/dotnet/MVPSummitHackathon2016) repo in the [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) project.</span></span>

## <a name="see-also"></a><span data-ttu-id="b1ce5-189">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b1ce5-189">See also</span></span>

- [<span data-ttu-id="b1ce5-190">Installieren von .NET Core</span><span class="sxs-lookup"><span data-stu-id="b1ce5-190">Install .NET Core</span></span>](../install/index.md)
- [<span data-ttu-id="b1ce5-191">Vorgehensweise: Verwenden von MSBuild-Projekt-SDKs</span><span class="sxs-lookup"><span data-stu-id="b1ce5-191">How to use MSBuild project SDKs</span></span>](/visualstudio/msbuild/how-to-use-project-sdk)
- [<span data-ttu-id="b1ce5-192">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="b1ce5-192">Package custom MSBuild targets and props with NuGet</span></span>](/nuget/create-packages/creating-a-package#include-msbuild-props-and-targets-in-a-package)