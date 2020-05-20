---
title: MSBuild-Eigenschaften für Microsoft.NET.Sdk
description: Referenz für MSBuild-Eigenschaften, die vom .NET Core SDK verstanden werden.
ms.date: 02/14/2020
ms.topic: reference
ms.openlocfilehash: 800ff59310d8437d7f770bf20a5bdf37714f8515
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795572"
---
# <a name="msbuild-properties-for-net-core-sdk-projects"></a><span data-ttu-id="ef949-103">MSBuild-Eigenschaften für .NET Core SDK-Projekte</span><span class="sxs-lookup"><span data-stu-id="ef949-103">MSBuild properties for .NET Core SDK projects</span></span>

<span data-ttu-id="ef949-104">Auf dieser Seite werden die MSBuild-Eigenschaften für das Konfigurieren von .NET Core-Projekten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="ef949-104">This page describes MSBuild properties for configuring .NET Core projects.</span></span> <span data-ttu-id="ef949-105">Sie können *Metadaten* für jede Eigenschaft als untergeordnete Elemente der Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-105">You can specify *metadata* for each property as child elements of the property.</span></span>

> [!NOTE]
> <span data-ttu-id="ef949-106">Diese Seite befindet sich noch in Bearbeitung und führt nicht sämtlich nützlichen MSBuild-Eigenschaften für das .NET Core SDK auf.</span><span class="sxs-lookup"><span data-stu-id="ef949-106">This page is a work in progress and does not list all of the useful MSBuild properties for the .NET Core SDK.</span></span> <span data-ttu-id="ef949-107">Eine Liste der gängigen MSBuild-Eigenschaften finden Sie unter [Gemeinsame MSBuild-Projekteigenschaften](/visualstudio/msbuild/common-msbuild-project-properties).</span><span class="sxs-lookup"><span data-stu-id="ef949-107">For a list of common MSBuild properties, see [Common MSBuild properties](/visualstudio/msbuild/common-msbuild-project-properties).</span></span>

## <a name="framework-properties"></a><span data-ttu-id="ef949-108">Frameworkeigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-108">Framework properties</span></span>

- [<span data-ttu-id="ef949-109">TargetFramework</span><span class="sxs-lookup"><span data-stu-id="ef949-109">TargetFramework</span></span>](#targetframework)
- [<span data-ttu-id="ef949-110">TargetFrameworks</span><span class="sxs-lookup"><span data-stu-id="ef949-110">TargetFrameworks</span></span>](#targetframeworks)
- [<span data-ttu-id="ef949-111">NetStandardImplicitPackageVersion</span><span class="sxs-lookup"><span data-stu-id="ef949-111">NetStandardImplicitPackageVersion</span></span>](#netstandardimplicitpackageversion)

### <a name="targetframework"></a><span data-ttu-id="ef949-112">TargetFramework</span><span class="sxs-lookup"><span data-stu-id="ef949-112">TargetFramework</span></span>

<span data-ttu-id="ef949-113">Die Eigenschaft `TargetFramework` gibt die Zielframeworkversion für die App an, die implizit auf ein [Metapaket](../packages.md#metapackages) verweist.</span><span class="sxs-lookup"><span data-stu-id="ef949-113">The `TargetFramework` property specifies the target framework version for the app, which implicitly references a [metapackage](../packages.md#metapackages).</span></span> <span data-ttu-id="ef949-114">Eine Liste gültiger Zielframeworkmoniker finden Sie unter [Zielframeworks in Projekten im SDK-Format](../../standard/frameworks.md#supported-target-framework-versions).</span><span class="sxs-lookup"><span data-stu-id="ef949-114">For a list of valid target framework monikers, see [Target frameworks in SDK-style projects](../../standard/frameworks.md#supported-target-framework-versions).</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

<span data-ttu-id="ef949-115">Weitere Informationen finden Sie unter [Zielframeworks in Projekten im SDK-Format](../../standard/frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ef949-115">For more information, see [Target frameworks in SDK-style projects](../../standard/frameworks.md).</span></span>

### <a name="targetframeworks"></a><span data-ttu-id="ef949-116">TargetFrameworks</span><span class="sxs-lookup"><span data-stu-id="ef949-116">TargetFrameworks</span></span>

<span data-ttu-id="ef949-117">Verwenden Sie die Eigenschaft `TargetFrameworks`, wenn Sie Ihre App für mehrere Zielplattformen entwickeln möchten.</span><span class="sxs-lookup"><span data-stu-id="ef949-117">Use the `TargetFrameworks` property when you want your app to target multiple platforms.</span></span> <span data-ttu-id="ef949-118">Eine Liste gültiger Zielframeworkmoniker finden Sie unter [Zielframeworks in Projekten im SDK-Format](../../standard/frameworks.md#supported-target-framework-versions).</span><span class="sxs-lookup"><span data-stu-id="ef949-118">For a list of valid target framework monikers, see [Target frameworks in SDK-style projects](../../standard/frameworks.md#supported-target-framework-versions).</span></span>

> [!NOTE]
> <span data-ttu-id="ef949-119">Diese Eigenschaft wird ignoriert, wenn `TargetFramework` (Singular) angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="ef949-119">This property is ignored if `TargetFramework` (singular) is specified.</span></span>

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

<span data-ttu-id="ef949-120">Weitere Informationen finden Sie unter [Zielframeworks in Projekten im SDK-Format](../../standard/frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ef949-120">For more information, see [Target frameworks in SDK-style projects](../../standard/frameworks.md).</span></span>

### <a name="netstandardimplicitpackageversion"></a><span data-ttu-id="ef949-121">NetStandardImplicitPackageVersion</span><span class="sxs-lookup"><span data-stu-id="ef949-121">NetStandardImplicitPackageVersion</span></span>

> [!NOTE]
> <span data-ttu-id="ef949-122">Diese Eigenschaft gilt nur für Projekte, die `netstandard1.x` verwenden.</span><span class="sxs-lookup"><span data-stu-id="ef949-122">This property only applies to projects using `netstandard1.x`.</span></span> <span data-ttu-id="ef949-123">Sie gilt nicht für Projekte, die `netstandard2.x` verwenden.</span><span class="sxs-lookup"><span data-stu-id="ef949-123">It doesn't apply to projects that use `netstandard2.x`.</span></span>

<span data-ttu-id="ef949-124">Verwenden Sie die Eigenschaft `NetStandardImplicitPackageVersion`, wenn Sie eine Frameworkversion angeben möchten, die niedriger ist als die [Metapaketversion](../packages.md#metapackages).</span><span class="sxs-lookup"><span data-stu-id="ef949-124">Use the `NetStandardImplicitPackageVersion` property when you want to specify a framework version that's lower than the [metapackage](../packages.md#metapackages) version.</span></span> <span data-ttu-id="ef949-125">Die Projektdatei im folgenden Beispiel gilt für `netstandard1.3`, verwendet aber Version 1.6.0 von `NETStandard.Library`.</span><span class="sxs-lookup"><span data-stu-id="ef949-125">The project file in the following example targets `netstandard1.3` but uses the 1.6.0 version of `NETStandard.Library`.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a><span data-ttu-id="ef949-126">Paketeigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-126">Package properties</span></span>

<span data-ttu-id="ef949-127">Sie können Eigenschaften wie `PackageId`, `PackageVersion`, `PackageIcon`, `Title` und `Description` angeben, um das Paket zu beschreiben, das aus Ihrem Projekt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="ef949-127">You can specify properties such as `PackageId`, `PackageVersion`, `PackageIcon`, `Title`, and `Description` to describe the package that gets created from your project.</span></span> <span data-ttu-id="ef949-128">Informationen zu diesen und anderen Eigenschaften finden Sie unter [Paketziel](/nuget/reference/msbuild-targets#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ef949-128">For information about these and other properties, see [pack target](/nuget/reference/msbuild-targets#pack-target).</span></span>

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties"></a><span data-ttu-id="ef949-129">Eigenschaften veröffentlichen</span><span class="sxs-lookup"><span data-stu-id="ef949-129">Publish properties</span></span>

- [<span data-ttu-id="ef949-130">RuntimeIdentifier</span><span class="sxs-lookup"><span data-stu-id="ef949-130">RuntimeIdentifier</span></span>](#runtimeidentifier)
- [<span data-ttu-id="ef949-131">RuntimeIdentifiers</span><span class="sxs-lookup"><span data-stu-id="ef949-131">RuntimeIdentifiers</span></span>](#runtimeidentifiers)
- [<span data-ttu-id="ef949-132">TrimmerRootAssembly</span><span class="sxs-lookup"><span data-stu-id="ef949-132">TrimmerRootAssembly</span></span>](#trimmerrootassembly)
- [<span data-ttu-id="ef949-133">UseAppHost</span><span class="sxs-lookup"><span data-stu-id="ef949-133">UseAppHost</span></span>](#useapphost)

### <a name="runtimeidentifier"></a><span data-ttu-id="ef949-134">RuntimeIdentifier</span><span class="sxs-lookup"><span data-stu-id="ef949-134">RuntimeIdentifier</span></span>

<span data-ttu-id="ef949-135">Mit der Eigenschaft `RuntimeIdentifier` können Sie eine einzelne [Runtime-ID (RID)](../rid-catalog.md) für das Projekt angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-135">The `RuntimeIdentifier` property lets you specify a single [runtime identifier (RID)](../rid-catalog.md) for the project.</span></span> <span data-ttu-id="ef949-136">RIDs ermöglichen das Veröffentlichen einer eigenständigen Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="ef949-136">The RID enables publishing a self-contained deployment.</span></span>

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a><span data-ttu-id="ef949-137">RuntimeIdentifiers</span><span class="sxs-lookup"><span data-stu-id="ef949-137">RuntimeIdentifiers</span></span>

<span data-ttu-id="ef949-138">Mit der Eigenschaft `RuntimeIdentifiers` können Sie eine durch Semikolons getrennte Liste von [Runtime-IDs (RIDs)](../rid-catalog.md) für das Projekt angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-138">The `RuntimeIdentifiers` property lets you specify a semicolon-delimited list of [runtime identifiers (RIDs)](../rid-catalog.md) for the project.</span></span> <span data-ttu-id="ef949-139">Verwenden Sie diese Eigenschaft, wenn die Veröffentlichung für mehrere Runtimes erfolgen muss.</span><span class="sxs-lookup"><span data-stu-id="ef949-139">Use this property if you need to publish for multiple runtimes.</span></span> <span data-ttu-id="ef949-140">`RuntimeIdentifiers` wird zur Wiederherstellungszeit verwendet, um sicherzustellen, dass sich die richtigen Assets im Graph befinden.</span><span class="sxs-lookup"><span data-stu-id="ef949-140">`RuntimeIdentifiers` is used at restore time to ensure the right assets are in the graph.</span></span>

> [!TIP]
> <span data-ttu-id="ef949-141">`RuntimeIdentifier` (Singular) kann schnellere Builds bereitstellen, wenn nur eine einzige Runtime erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="ef949-141">`RuntimeIdentifier` (singular) can provide faster builds when only a single runtime is required.</span></span>

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a><span data-ttu-id="ef949-142">TrimmerRootAssembly</span><span class="sxs-lookup"><span data-stu-id="ef949-142">TrimmerRootAssembly</span></span>

<span data-ttu-id="ef949-143">Mit dem `TrimmerRootAssembly`-Element können Sie eine Assembly aus der [*Kürzung*](../deploying/trim-self-contained.md) ausschließen.</span><span class="sxs-lookup"><span data-stu-id="ef949-143">The `TrimmerRootAssembly` item lets you exclude an assembly from [*trimming*](../deploying/trim-self-contained.md).</span></span> <span data-ttu-id="ef949-144">Die Kürzung ist der Prozess, bei dem nicht verwendete Teile der Runtime aus einer gepackten Anwendung entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="ef949-144">Trimming is the process of removing unused parts of the runtime from a packaged application.</span></span> <span data-ttu-id="ef949-145">In einigen Fällen können die erforderlichen Verweise durch eine Kürzung fälschlicherweise entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="ef949-145">In some cases, trimming might incorrectly remove required references.</span></span>

<span data-ttu-id="ef949-146">Der folgende XML-Code schließt die `System.Security`-Assembly aus der Kürzung aus.</span><span class="sxs-lookup"><span data-stu-id="ef949-146">The following XML excludes the `System.Security` assembly from trimming.</span></span>

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a><span data-ttu-id="ef949-147">UseAppHost</span><span class="sxs-lookup"><span data-stu-id="ef949-147">UseAppHost</span></span>

<span data-ttu-id="ef949-148">Die Eigenschaft `UseAppHost` wurde in Version 2.1.400 des .NET Core SDK eingeführt.</span><span class="sxs-lookup"><span data-stu-id="ef949-148">The `UseAppHost` property was introduced in the 2.1.400 version of the .NET Core SDK.</span></span> <span data-ttu-id="ef949-149">Sie steuert, ob eine native ausführbare Datei für eine Bereitstellung erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="ef949-149">It controls whether or not a native executable is created for a deployment.</span></span> <span data-ttu-id="ef949-150">Eine native ausführbare Datei ist für eigenständige Bereitstellungen erforderlich.</span><span class="sxs-lookup"><span data-stu-id="ef949-150">A native executable is required for self-contained deployments.</span></span>

<span data-ttu-id="ef949-151">In .NET Core 3.0 und höheren Versionen wird standardmäßig eine frameworkabhängige ausführbare Datei erstellt.</span><span class="sxs-lookup"><span data-stu-id="ef949-151">In .NET Core 3.0 and later versions, a framework-dependent executable is created by default.</span></span> <span data-ttu-id="ef949-152">Legen Sie die Eigenschaft `UseAppHost` auf `false` fest, um die Erzeugung der ausführbaren Datei zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-152">Set the `UseAppHost` property to `false` to disable generation of the executable.</span></span>

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

<span data-ttu-id="ef949-153">Weitere Informationen zur Bereitstellung finden Sie unter [.NET Core-Anwendungsbereitstellung](../deploying/index.md).</span><span class="sxs-lookup"><span data-stu-id="ef949-153">For more information about deployment, see [.NET Core application deployment](../deploying/index.md).</span></span>

## <a name="compile-properties"></a><span data-ttu-id="ef949-154">Kompilierungseigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-154">Compile properties</span></span>

- [<span data-ttu-id="ef949-155">LangVersion</span><span class="sxs-lookup"><span data-stu-id="ef949-155">LangVersion</span></span>](#langversion)

### <a name="langversion"></a><span data-ttu-id="ef949-156">LangVersion</span><span class="sxs-lookup"><span data-stu-id="ef949-156">LangVersion</span></span>

<span data-ttu-id="ef949-157">Mit der Eigenschaft `LangVersion` können Sie eine bestimmte Version der Programmiersprache angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-157">The `LangVersion` property lets you specify a specific programming language version.</span></span> <span data-ttu-id="ef949-158">Wenn Sie beispielsweise auf C#-Vorschaufeatures zugreifen möchten, legen Sie `LangVersion` auf `preview` fest.</span><span class="sxs-lookup"><span data-stu-id="ef949-158">For example, if you want access to C# preview features, set `LangVersion` to `preview`.</span></span>

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

<span data-ttu-id="ef949-159">Weitere Informationen finden Sie unter [C#-Sprachversionsverwaltung](../../csharp/language-reference/configure-language-version.md#override-a-default).</span><span class="sxs-lookup"><span data-stu-id="ef949-159">For more information, see [C# language versioning](../../csharp/language-reference/configure-language-version.md#override-a-default).</span></span>

## <a name="run-time-configuration-properties"></a><span data-ttu-id="ef949-160">Runtimekonfigurationseigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-160">Run-time configuration properties</span></span>

<span data-ttu-id="ef949-161">Sie können manche Verhaltensweisen der Runtime konfigurieren, indem Sie die MSBuild-Eigenschaften in der Projektdatei der App angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-161">You can configure some run-time behaviors by specifying MSBuild properties in the project file of the app.</span></span> <span data-ttu-id="ef949-162">Informationen zu anderen Konfigurationsmöglichkeiten für das Runtimeverhalten finden Sie unter [Konfigurationseinstellungen für die .NET Core-Runtime](../run-time-config/index.md).</span><span class="sxs-lookup"><span data-stu-id="ef949-162">For information about other ways of configuring run-time behavior, see [.NET Core run-time configuration settings](../run-time-config/index.md).</span></span>

- [<span data-ttu-id="ef949-163">ConcurrentGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-163">ConcurrentGarbageCollection</span></span>](#concurrentgarbagecollection)
- [<span data-ttu-id="ef949-164">InvariantGlobalization</span><span class="sxs-lookup"><span data-stu-id="ef949-164">InvariantGlobalization</span></span>](#invariantglobalization)
- [<span data-ttu-id="ef949-165">RetainVMGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-165">RetainVMGarbageCollection</span></span>](#retainvmgarbagecollection)
- [<span data-ttu-id="ef949-166">ServerGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-166">ServerGarbageCollection</span></span>](#servergarbagecollection)
- [<span data-ttu-id="ef949-167">ThreadPoolMaxThreads</span><span class="sxs-lookup"><span data-stu-id="ef949-167">ThreadPoolMaxThreads</span></span>](#threadpoolmaxthreads)
- [<span data-ttu-id="ef949-168">ThreadPoolMinThreads</span><span class="sxs-lookup"><span data-stu-id="ef949-168">ThreadPoolMinThreads</span></span>](#threadpoolminthreads)
- [<span data-ttu-id="ef949-169">TieredCompilation</span><span class="sxs-lookup"><span data-stu-id="ef949-169">TieredCompilation</span></span>](#tieredcompilation)
- [<span data-ttu-id="ef949-170">TieredCompilationQuickJit</span><span class="sxs-lookup"><span data-stu-id="ef949-170">TieredCompilationQuickJit</span></span>](#tieredcompilationquickjit)
- [<span data-ttu-id="ef949-171">TieredCompilationQuickJitForLoops</span><span class="sxs-lookup"><span data-stu-id="ef949-171">TieredCompilationQuickJitForLoops</span></span>](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a><span data-ttu-id="ef949-172">ConcurrentGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-172">ConcurrentGarbageCollection</span></span>

<span data-ttu-id="ef949-173">Mit der `ConcurrentGarbageCollection`-Eigenschaft wird konfiguriert, ob [die Garbage Collection im Hintergrund (parallele GC)](../../standard/garbage-collection/background-gc.md) aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="ef949-173">The `ConcurrentGarbageCollection` property configures whether [background (concurrent) garbage collection](../../standard/garbage-collection/background-gc.md) is enabled.</span></span> <span data-ttu-id="ef949-174">Legen Sie den Wert auf `false` fest, um die Garbage Collection im Hintergrund zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-174">Set the value to `false` to disable background garbage collection.</span></span> <span data-ttu-id="ef949-175">Weitere Informationen finden Sie unter [System.GC.Concurrent/COMPlus_gcConcurrent](../run-time-config/garbage-collector.md#systemgcconcurrentcomplus_gcconcurrent).</span><span class="sxs-lookup"><span data-stu-id="ef949-175">For more information, see [System.GC.Concurrent/COMPlus_gcConcurrent](../run-time-config/garbage-collector.md#systemgcconcurrentcomplus_gcconcurrent).</span></span>

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a><span data-ttu-id="ef949-176">InvariantGlobalization</span><span class="sxs-lookup"><span data-stu-id="ef949-176">InvariantGlobalization</span></span>

<span data-ttu-id="ef949-177">Mit der `InvariantGlobalization`-Eigenschaft wird konfiguriert, ob die App im *globalisierungsinvarianten Modus* ausgeführt wird, was bedeutet, dass sie keinen Zugriff auf kulturspezifische Daten hat.</span><span class="sxs-lookup"><span data-stu-id="ef949-177">The `InvariantGlobalization` property configures whether the app runs in *globalization-invariant* mode, which means it doesn't have access to culture-specific data.</span></span> <span data-ttu-id="ef949-178">Legen Sie den Wert auf `true` fest, um die Ausführung im globalisierungsinvarianten Modus zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-178">Set the value to `true` to run in globalization-invariant mode.</span></span> <span data-ttu-id="ef949-179">Weitere Informationen finden Sie unter [Invarianter Modus](../run-time-config/globalization.md#invariant-mode).</span><span class="sxs-lookup"><span data-stu-id="ef949-179">For more information, see [Invariant mode](../run-time-config/globalization.md#invariant-mode).</span></span>

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a><span data-ttu-id="ef949-180">RetainVMGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-180">RetainVMGarbageCollection</span></span>

<span data-ttu-id="ef949-181">Mit der `RetainVMGarbageCollection`-Eigenschaft wird der Garbage Collector so konfiguriert, dass gelöschte Speichersegmente in eine Standbyliste eingefügt werden, damit Sie diese zukünftig verwenden oder freigeben können.</span><span class="sxs-lookup"><span data-stu-id="ef949-181">The `RetainVMGarbageCollection` property configures the garbage collector to put deleted memory segments on a standby list for future use or release them.</span></span> <span data-ttu-id="ef949-182">Wenn der Wert auf `true` festgelegt wird, wird der Garbage Collector angewiesen, die Segmente in eine Standbyliste einzufügen.</span><span class="sxs-lookup"><span data-stu-id="ef949-182">Setting the value to `true` tells the garbage collector to put the segments on a standby list.</span></span> <span data-ttu-id="ef949-183">Weitere Informationen finden Sie unter [System.GC.RetainVM/COMPlus_GCRetainVM](../run-time-config/garbage-collector.md#systemgcretainvmcomplus_gcretainvm).</span><span class="sxs-lookup"><span data-stu-id="ef949-183">For more information, see [System.GC.RetainVM/COMPlus_GCRetainVM](../run-time-config/garbage-collector.md#systemgcretainvmcomplus_gcretainvm).</span></span>

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a><span data-ttu-id="ef949-184">ServerGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="ef949-184">ServerGarbageCollection</span></span>

<span data-ttu-id="ef949-185">Mit der `ServerGarbageCollection`-Eigenschaft wird konfiguriert, ob die Anwendung die [Garbage Collection für Arbeitsstationen oder für Server](../../standard/garbage-collection/workstation-server-gc.md) verwendet.</span><span class="sxs-lookup"><span data-stu-id="ef949-185">The `ServerGarbageCollection` property configures whether the application uses [workstation garbage collection or server garbage collection](../../standard/garbage-collection/workstation-server-gc.md).</span></span> <span data-ttu-id="ef949-186">Legen Sie den Wert auf `true` fest, um die Garbage Collection für Server zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ef949-186">Set the value to `true` to use server garbage collection.</span></span> <span data-ttu-id="ef949-187">Weitere Informationen finden Sie unter [System.GC.Server/COMPlus_gcServer](../run-time-config/garbage-collector.md#systemgcservercomplus_gcserver).</span><span class="sxs-lookup"><span data-stu-id="ef949-187">For more information, see [System.GC.Server/COMPlus_gcServer](../run-time-config/garbage-collector.md#systemgcservercomplus_gcserver).</span></span>

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a><span data-ttu-id="ef949-188">ThreadPoolMaxThreads</span><span class="sxs-lookup"><span data-stu-id="ef949-188">ThreadPoolMaxThreads</span></span>

<span data-ttu-id="ef949-189">Mit der `ThreadPoolMaxThreads`-Eigenschaft wird die maximale Threadanzahl für den Arbeitsthreadpool konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="ef949-189">The `ThreadPoolMaxThreads` property configures the maximum number of threads for the worker thread pool.</span></span> <span data-ttu-id="ef949-190">Weitere Informationen finden Sie unter [Maximale Threadanzahl](../run-time-config/threading.md#maximum-threads).</span><span class="sxs-lookup"><span data-stu-id="ef949-190">For more information, see [Maximum threads](../run-time-config/threading.md#maximum-threads).</span></span>

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a><span data-ttu-id="ef949-191">ThreadPoolMinThreads</span><span class="sxs-lookup"><span data-stu-id="ef949-191">ThreadPoolMinThreads</span></span>

<span data-ttu-id="ef949-192">Mit der `ThreadPoolMinThreads`-Eigenschaft wird die minimale Threadanzahl für den Arbeitsthreadpool konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="ef949-192">The `ThreadPoolMinThreads` property configures the minimum number of threads for the worker thread pool.</span></span> <span data-ttu-id="ef949-193">Weitere Informationen finden Sie unter [Minimale Threadanzahl](../run-time-config/threading.md#minimum-threads).</span><span class="sxs-lookup"><span data-stu-id="ef949-193">For more information, see [Minimum threads](../run-time-config/threading.md#minimum-threads).</span></span>

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a><span data-ttu-id="ef949-194">TieredCompilation</span><span class="sxs-lookup"><span data-stu-id="ef949-194">TieredCompilation</span></span>

<span data-ttu-id="ef949-195">Mit der `TieredCompilation`-Eigenschaft wird konfiguriert, ob der JIT-Compiler (Just-in-Time) die [mehrstufige Kompilierung](../whats-new/dotnet-core-3-0.md#tiered-compilation) verwendet.</span><span class="sxs-lookup"><span data-stu-id="ef949-195">The `TieredCompilation` property configures whether the just-in-time (JIT) compiler uses [tiered compilation](../whats-new/dotnet-core-3-0.md#tiered-compilation).</span></span> <span data-ttu-id="ef949-196">Legen Sie den Wert auf `false` fest, um die mehrstufige Kompilierung zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-196">Set the value to `false` to disable tiered compilation.</span></span> <span data-ttu-id="ef949-197">Weitere Informationen finden Sie unter [Mehrstufige Kompilierung](../run-time-config/compilation.md#tiered-compilation).</span><span class="sxs-lookup"><span data-stu-id="ef949-197">For more information, see [Tiered compilation](../run-time-config/compilation.md#tiered-compilation).</span></span>

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a><span data-ttu-id="ef949-198">TieredCompilationQuickJit</span><span class="sxs-lookup"><span data-stu-id="ef949-198">TieredCompilationQuickJit</span></span>

<span data-ttu-id="ef949-199">Mit der `TieredCompilationQuickJit`-Eigenschaft wird konfiguriert, ob der JIT-Compiler Quick JIT verwendet.</span><span class="sxs-lookup"><span data-stu-id="ef949-199">The `TieredCompilationQuickJit` property configures whether the JIT compiler uses quick JIT.</span></span> <span data-ttu-id="ef949-200">Legen Sie den Wert auf `false` fest, um Quick JIT zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-200">Set the value to `false` to disable quick JIT.</span></span> <span data-ttu-id="ef949-201">Weitere Informationen finden Sie unter [Quick JIT](../run-time-config/compilation.md#quick-jit).</span><span class="sxs-lookup"><span data-stu-id="ef949-201">For more information, see [Quick JIT](../run-time-config/compilation.md#quick-jit).</span></span>

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a><span data-ttu-id="ef949-202">TieredCompilationQuickJitForLoops</span><span class="sxs-lookup"><span data-stu-id="ef949-202">TieredCompilationQuickJitForLoops</span></span>

<span data-ttu-id="ef949-203">Mit der `TieredCompilationQuickJitForLoops`-Eigenschaft wird konfiguriert, ob der JIT-Compiler Quick JIT für Methoden mit Schleifen verwendet.</span><span class="sxs-lookup"><span data-stu-id="ef949-203">The `TieredCompilationQuickJitForLoops` property configures whether the JIT compiler uses quick JIT on methods that contain loops.</span></span> <span data-ttu-id="ef949-204">Legen Sie den Wert auf `true` fest, um Quick JIT für Methoden mit Schleifen zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef949-204">Set the value to `true` to enable quick JIT on methods that contain loops.</span></span> <span data-ttu-id="ef949-205">Weitere Informationen finden Sie unter [Quick JIT für Schleifen](../run-time-config/compilation.md#quick-jit-for-loops).</span><span class="sxs-lookup"><span data-stu-id="ef949-205">For more information, see [Quick JIT for loops](../run-time-config/compilation.md#quick-jit-for-loops).</span></span>

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties"></a><span data-ttu-id="ef949-206">Verweiseigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-206">Reference properties</span></span>

- [<span data-ttu-id="ef949-207">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ef949-207">AssetTargetFallback</span></span>](#assettargetfallback)
- [<span data-ttu-id="ef949-208">PackageReference</span><span class="sxs-lookup"><span data-stu-id="ef949-208">PackageReference</span></span>](#packagereference)
- [<span data-ttu-id="ef949-209">ProjectReference</span><span class="sxs-lookup"><span data-stu-id="ef949-209">ProjectReference</span></span>](#projectreference)
- [<span data-ttu-id="ef949-210">Verweis</span><span class="sxs-lookup"><span data-stu-id="ef949-210">Reference</span></span>](#reference)
- [<span data-ttu-id="ef949-211">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-211">Restore properties</span></span>](#restore-properties)

### <a name="assettargetfallback"></a><span data-ttu-id="ef949-212">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ef949-212">AssetTargetFallback</span></span>

<span data-ttu-id="ef949-213">Mit der Eigenschaft `AssetTargetFallback` können Sie zusätzliche kompatible Frameworkversionen für Projektverweise und NuGet-Pakete angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-213">The `AssetTargetFallback` property lets you specify additional compatible framework versions for project references and NuGet packages.</span></span> <span data-ttu-id="ef949-214">Wenn Sie z. B. mit `PackageReference` eine Paketabhängigkeit angeben, aber das entsprechende Paket keine Assets enthält, die mit dem `TargetFramework` Ihres Projekts kompatibel sind, kommt die Eigenschaft `AssetTargetFallback` ins Spiel.</span><span class="sxs-lookup"><span data-stu-id="ef949-214">For example, if you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's `TargetFramework`, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="ef949-215">Die Kompatibilität des referenzierten Pakets wird erneut anhand jedes Zielframeworks überprüft, das in `AssetTargetFallback` angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="ef949-215">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>

<span data-ttu-id="ef949-216">Sie können die Eigenschaft `AssetTargetFallback` auf eine oder mehrere [Zielframeworkversionen](../../standard/frameworks.md#supported-target-framework-versions) festlegen.</span><span class="sxs-lookup"><span data-stu-id="ef949-216">You can set the `AssetTargetFallback` property to one or more [target framework versions](../../standard/frameworks.md#supported-target-framework-versions).</span></span>

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="packagereference"></a><span data-ttu-id="ef949-217">PackageReference</span><span class="sxs-lookup"><span data-stu-id="ef949-217">PackageReference</span></span>

<span data-ttu-id="ef949-218">`PackageReference` definiert einen Verweis auf ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="ef949-218">The `PackageReference` defines a reference to a NuGet package.</span></span> <span data-ttu-id="ef949-219">Beispiel: Sie möchten auf ein einzelnes Paket verweisen statt auf ein [Metapaket](../packages.md#metapackages).</span><span class="sxs-lookup"><span data-stu-id="ef949-219">For example, you may want to reference a single package instead of a [metapackage](../packages.md#metapackages).</span></span>

<span data-ttu-id="ef949-220">Das `Include`-Attribut gibt die Paket-ID an.</span><span class="sxs-lookup"><span data-stu-id="ef949-220">The `Include` attribute specifies the package ID.</span></span> <span data-ttu-id="ef949-221">Das `Version`-Attribut gibt die Version oder den Versionsbereich an.</span><span class="sxs-lookup"><span data-stu-id="ef949-221">The `Version` attribute specifies the version or version range.</span></span> <span data-ttu-id="ef949-222">Informationen, wie Sie eine Mindestversion, Maximalversion, einen Versionsbereich oder eine exakte Versionsübereinstimmung angeben, finden Sie unter [Versionsbereiche](/nuget/concepts/package-versioning#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="ef949-222">For information about how to specify a minimum version, maximum version, range, or exact match, see [Version ranges](/nuget/concepts/package-versioning#version-ranges).</span></span> <span data-ttu-id="ef949-223">Sie können auch die folgenden Metadaten zu einem Projektverweis hinzufügen: `IncludeAssets`, `ExcludeAssets` und `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="ef949-223">You can also add the following metadata to a project reference: `IncludeAssets`, `ExcludeAssets`, and `PrivateAssets`.</span></span>

<span data-ttu-id="ef949-224">Der Codeausschnitt für die Projektdatei im folgenden Beispiel verweist auf das Paket [System.Runtime](https://www.nuget.org/packages/System.Runtime/).</span><span class="sxs-lookup"><span data-stu-id="ef949-224">The project file snippet in the following example references the [System.Runtime](https://www.nuget.org/packages/System.Runtime/) package.</span></span>

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

<span data-ttu-id="ef949-225">Weitere Informationen finden Sie unter [Paketverweis in Projektdateien](/nuget/consume-packages/package-references-in-project-files).</span><span class="sxs-lookup"><span data-stu-id="ef949-225">For more information, see [Package references in project files](/nuget/consume-packages/package-references-in-project-files).</span></span>

### <a name="projectreference"></a><span data-ttu-id="ef949-226">ProjectReference</span><span class="sxs-lookup"><span data-stu-id="ef949-226">ProjectReference</span></span>

<span data-ttu-id="ef949-227">Das `ProjectReference`-Element definiert einen Verweis auf ein anderes Projekt.</span><span class="sxs-lookup"><span data-stu-id="ef949-227">The `ProjectReference` item defines a reference to another project.</span></span> <span data-ttu-id="ef949-228">Das referenzierte Projekt wird als NuGet-Paketabhängigkeit hinzugefügt, d. h., es wird genauso wie eine `PackageReference` behandelt.</span><span class="sxs-lookup"><span data-stu-id="ef949-228">The referenced project is added as a NuGet package dependency, that is, it's treated the same as a `PackageReference`.</span></span>

<span data-ttu-id="ef949-229">Das Attribut `Include` gibt den Pfad zu dem Projekt an.</span><span class="sxs-lookup"><span data-stu-id="ef949-229">The `Include` attribute specifies the path to the project.</span></span> <span data-ttu-id="ef949-230">Sie können auch die folgenden Metadaten zu einem Projektverweis hinzufügen: `IncludeAssets`, `ExcludeAssets` und `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="ef949-230">You can also add the following metadata to a project reference: `IncludeAssets`, `ExcludeAssets`, and `PrivateAssets`.</span></span>

<span data-ttu-id="ef949-231">Der Codeausschnitt für die Projektdatei im folgenden Beispiel verweist auf ein Projekt namens `Project2`.</span><span class="sxs-lookup"><span data-stu-id="ef949-231">The project file snippet in the following example references a project named `Project2`.</span></span>

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a><span data-ttu-id="ef949-232">Referenz</span><span class="sxs-lookup"><span data-stu-id="ef949-232">Reference</span></span>

<span data-ttu-id="ef949-233">Das `Reference`-Element definiert einen Verweis auf eine Assemblydatei.</span><span class="sxs-lookup"><span data-stu-id="ef949-233">The `Reference` item defines a reference to an assembly file.</span></span>

<span data-ttu-id="ef949-234">Das `Include`-Attribut gibt den Namen der Datei an, und das untergeordnete `HintPath`-Element gibt den Pfad zu der Assembly an.</span><span class="sxs-lookup"><span data-stu-id="ef949-234">The `Include` attribute specifies the name of the file, and the `HintPath` child element specifies the path to the assembly.</span></span>

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-properties"></a><span data-ttu-id="ef949-235">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-235">Restore properties</span></span>

<span data-ttu-id="ef949-236">Durch das Wiederherstellen eines referenzierten Pakets werden alle seine direkten Abhängigkeiten sowie alle Abhängigkeiten dieser Abhängigkeiten installiert.</span><span class="sxs-lookup"><span data-stu-id="ef949-236">Restoring a referenced package installs all of its direct dependencies and all the dependencies of those dependencies.</span></span> <span data-ttu-id="ef949-237">Sie können die Paketwiederherstellung anpassen, indem Sie Eigenschaften wie `RestorePackagesPath` und `RestoreIgnoreFailedSources` angeben.</span><span class="sxs-lookup"><span data-stu-id="ef949-237">You can customize package restoration by specifying properties such as `RestorePackagesPath` and `RestoreIgnoreFailedSources`.</span></span> <span data-ttu-id="ef949-238">Weitere Informationen zu diesen und anderen Eigenschaften finden Sie unter [Wiederherstellungsziel](/nuget/reference/msbuild-targets#restore-target).</span><span class="sxs-lookup"><span data-stu-id="ef949-238">For more information about these and other properties, see [restore target](/nuget/reference/msbuild-targets#restore-target).</span></span>

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="see-also"></a><span data-ttu-id="ef949-239">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ef949-239">See also</span></span>

- [<span data-ttu-id="ef949-240">MSBuild-Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="ef949-240">MSBuild schema reference</span></span>](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [<span data-ttu-id="ef949-241">Gemeinsame MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="ef949-241">Common MSBuild properties</span></span>](/visualstudio/msbuild/common-msbuild-project-properties)
- [<span data-ttu-id="ef949-242">MSBuild-Eigenschaften für NuGet-Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="ef949-242">MSBuild properties for NuGet pack</span></span>](/nuget/reference/msbuild-targets#pack-target)
- [<span data-ttu-id="ef949-243">MSBuild-Eigenschaften für NuGet-Ziel „restore“</span><span class="sxs-lookup"><span data-stu-id="ef949-243">MSBuild properties for NuGet restore</span></span>](/nuget/reference/msbuild-targets#restore-properties)
- [<span data-ttu-id="ef949-244">Anpassen eines Builds</span><span class="sxs-lookup"><span data-stu-id="ef949-244">Customize a build</span></span>](/visualstudio/msbuild/customize-your-build)