---
title: Erstellen eines Vorlagenpakets für „dotnet new“
description: Hier erfahren Sie, wie Sie eine CSPROJ-Datei zum Erstellen eines Vorlagenpakets für den Befehl „dotnet new“ erstellen.
author: thraka
ms.date: 06/25/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: df8c33856195ba7feacd32203e4a885997b50ad2
ms.sourcegitcommit: 6472349821dbe202d01182bc2cfe9d7176eaaa6c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67870629"
---
# <a name="tutorial-create-a-template-pack"></a><span data-ttu-id="643c7-103">Tutorial: Erstellen eines Vorlagenpakets</span><span class="sxs-lookup"><span data-stu-id="643c7-103">Tutorial: Create a template pack</span></span>

<span data-ttu-id="643c7-104">Mit .NET Core können Sie Vorlagen erstellen und bereitstellen, die Projekte, Dateien und sogar Ressourcen generieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-104">With .NET Core, you can create and deploy templates that generate projects, files, even resources.</span></span> <span data-ttu-id="643c7-105">Dieses Tutorial ist der dritte Teil einer Reihe, die zeigt, wie Sie Vorlagen für die Verwendung mit dem Befehl `dotnet new` erstellen, installieren und deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-105">This tutorial is part three of a series that teaches you how to create, install, and uninstall, templates for use with the `dotnet new` command.</span></span>

<span data-ttu-id="643c7-106">In diesem Teil der Reihe wird Folgendes vermittelt:</span><span class="sxs-lookup"><span data-stu-id="643c7-106">In this part of the series you'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="643c7-107">Erstellen eines CSPROJ-Projekts zur Erstellung eines Vorlagenpakets</span><span class="sxs-lookup"><span data-stu-id="643c7-107">Create a _.csproj\* project to build a template pack</span></span>
> * <span data-ttu-id="643c7-108">Konfigurieren der Projektdatei zum Ausführen eines Packvorgangs</span><span class="sxs-lookup"><span data-stu-id="643c7-108">Configure the project file for packing</span></span>
> * <span data-ttu-id="643c7-109">Installieren einer Vorlage aus einer NuGet-Paketdatei</span><span class="sxs-lookup"><span data-stu-id="643c7-109">Install a template from a NuGet package file</span></span>
> * <span data-ttu-id="643c7-110">Deinstallieren einer Vorlage anhand der Paket-ID</span><span class="sxs-lookup"><span data-stu-id="643c7-110">Uninstall a template by package ID</span></span>

## <a name="prerequisites"></a><span data-ttu-id="643c7-111">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="643c7-111">Prerequisites</span></span>

* <span data-ttu-id="643c7-112">Absolvieren Sie [Teil 1](cli-templates-create-item-template.md) und [Teil 2](cli-templates-create-project-template.md) dieser Tutorialreihe.</span><span class="sxs-lookup"><span data-stu-id="643c7-112">Complete [part 1](cli-templates-create-item-template.md) and [part 2](cli-templates-create-project-template.md) of this tutorial series.</span></span>

  <span data-ttu-id="643c7-113">In diesem Tutorial werden die beiden Vorlagen verwendet, die in den ersten beiden Teilen dieses Tutorials erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="643c7-113">This tutorial uses the two templates created in the first two parts of this tutorial.</span></span> <span data-ttu-id="643c7-114">Gegebenenfalls kann auch eine andere Vorlage verwendet werden, solange diese als Ordner in den Ordner _working\templates\\_ kopiert wird.</span><span class="sxs-lookup"><span data-stu-id="643c7-114">It's possible you can use a different template as long as you copy the template as a folder into the _working\templates\\_ folder.</span></span>

* <span data-ttu-id="643c7-115">Öffnen Sie ein Terminal, und navigieren Sie zum Ordner _working\templates\\_ .</span><span class="sxs-lookup"><span data-stu-id="643c7-115">Open a terminal and navigate to the _working\templates\\_ folder.</span></span>

## <a name="create-a-template-pack-project"></a><span data-ttu-id="643c7-116">Erstellen eines Vorlagenpaketprojekts</span><span class="sxs-lookup"><span data-stu-id="643c7-116">Create a template pack project</span></span>

<span data-ttu-id="643c7-117">Bei einem Vorlagenpaket handelt es sich um eine Datei, in die mindestens eine Vorlage gepackt wurde.</span><span class="sxs-lookup"><span data-stu-id="643c7-117">A template pack is one or more templates packaged into a file.</span></span> <span data-ttu-id="643c7-118">Wenn Sie ein Paket installieren oder deinstallieren, werden alle darin enthaltenen Vorlagen hinzugefügt bzw. entfernt.</span><span class="sxs-lookup"><span data-stu-id="643c7-118">When you install or uninstall a pack, all templates contained in the pack are added or removed, respectively.</span></span> <span data-ttu-id="643c7-119">In den vorherigen Teilen dieser Tutorialreihe wurden jeweils nur einzelne Vorlagen verwendet.</span><span class="sxs-lookup"><span data-stu-id="643c7-119">The previous parts of this tutorial series only worked with individual templates.</span></span> <span data-ttu-id="643c7-120">Wenn Sie eine nicht gepackte Vorlage weitergeben möchten, müssen Sie den Vorlagenordner kopieren und die Installation unter Verwendung dieses Ordners durchführen.</span><span class="sxs-lookup"><span data-stu-id="643c7-120">To share a non-packed template, you have to copy the template folder and install via that folder.</span></span> <span data-ttu-id="643c7-121">Ein Vorlagenpaket ist eine einzelne Datei, die mehrere Vorlagen enthalten kann, was die Weitergabe vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="643c7-121">Because a template pack can have more than one template in it, and is a single file, sharing is easier.</span></span>

<span data-ttu-id="643c7-122">Bei Vorlagenpaketen handelt es sich um NuGet-Paketdateien ( _.nupkg_).</span><span class="sxs-lookup"><span data-stu-id="643c7-122">Template packs are represented by a NuGet package (_.nupkg_) file.</span></span> <span data-ttu-id="643c7-123">Das bedeutet, sie können wie jedes andere NuGet-Paket in einen NuGet-Feed hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="643c7-123">And, like any NuGet package, you can upload the template pack to a NuGet feed.</span></span> <span data-ttu-id="643c7-124">Der Befehl `dotnet new -i` unterstützt die Installation von Vorlagenpaketen aus einem NuGet-Paketfeed.</span><span class="sxs-lookup"><span data-stu-id="643c7-124">The `dotnet new -i` command supports installing template pack from a NuGet package feed.</span></span> <span data-ttu-id="643c7-125">Darüber hinaus kann ein Vorlagenpaket auch direkt über eine __ NUPKG-Datei installiert werden.</span><span class="sxs-lookup"><span data-stu-id="643c7-125">Additionally, you can install a template pack from a _.nupkg_ file directly.</span></span>

<span data-ttu-id="643c7-126">Üblicherweise wird eine C#-Projektdatei verwendet, um Code zu kompilieren und eine Binärdatei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="643c7-126">Normally you use a C# project file to compile code and produce a binary.</span></span> <span data-ttu-id="643c7-127">Das Projekt kann jedoch auch verwendet werden, um ein Vorlagenpaket zu generieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-127">However, the project can also be used to generate a template pack.</span></span> <span data-ttu-id="643c7-128">Durch Ändern der Einstellungen der __ CSPROJ-Datei können Sie sicherstellen, dass kein Code kompiliert wird, und stattdessen alle Ressourcen ihrer Vorlagen als Ressourcen einschließen.</span><span class="sxs-lookup"><span data-stu-id="643c7-128">By changing the settings of the _.csproj_, you can prevent it from compiling any code and instead include all the assets of your templates as resources.</span></span> <span data-ttu-id="643c7-129">Wenn dieses Projekt erstellt wird, wird ein Vorlagenpaket in Form eines NuGet-Pakets erzeugt.</span><span class="sxs-lookup"><span data-stu-id="643c7-129">When this project is built, it produces a template pack NuGet package.</span></span>

<span data-ttu-id="643c7-130">Das erstellte Paket enthält die zuvor erstellte [Elementvorlage](cli-templates-create-item-template.md) und [Paketvorlage](cli-templates-create-project-template.md).</span><span class="sxs-lookup"><span data-stu-id="643c7-130">The pack you'll create will include the [item template](cli-templates-create-item-template.md) and [package template](cli-templates-create-project-template.md) previously created.</span></span> <span data-ttu-id="643c7-131">Da wir die beiden Vorlagen im Ordner _working\templates\\_ zusammengefasst haben, können wir den Ordner _working_ für die __ CSPROJ-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="643c7-131">Because we grouped the two templates into the _working\templates\\_ folder, we can use the _working_ folder for the _.csproj_ file.</span></span>

<span data-ttu-id="643c7-132">Navigieren Sie in Ihrem Terminal zum Ordner _working_.</span><span class="sxs-lookup"><span data-stu-id="643c7-132">In your terminal, navigate to the _working_ folder.</span></span> <span data-ttu-id="643c7-133">Erstellen Sie ein neues Projekt, und legen Sie den Namen auf `templatepack` und den Ausgabeordner auf den aktuellen Ordner fest.</span><span class="sxs-lookup"><span data-stu-id="643c7-133">Create a new project and set the name to `templatepack` and the output folder to the current folder.</span></span>

```console
dotnet new console -n templatepack -o .
```

<span data-ttu-id="643c7-134">Der Parameter `-n` legt den Dateinamen der __ CSPROJ-Datei auf _templatepack.csproj_ fest, und der Parameter `-o` erstellt die Dateien im aktuellen Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="643c7-134">The `-n` parameter sets the _.csproj_ filename to _templatepack.csproj_ and the `-o` parameters creates the files in the current directory.</span></span> <span data-ttu-id="643c7-135">Das Ergebnis sollte in etwa wie in der folgenden Ausgabe aussehen:</span><span class="sxs-lookup"><span data-stu-id="643c7-135">You should see a result similar to the following output.</span></span>

```console
C:\working> dotnet new console -n templatepack -o .
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

<span data-ttu-id="643c7-136">Öffnen Sie als Nächstes die Datei _templatepack.csproj_ in Ihrem bevorzugten Editor, und ersetzen Sie den Inhalt durch den folgenden XML-Code:</span><span class="sxs-lookup"><span data-stu-id="643c7-136">Next, open the _templatepack.csproj_ file in your favorite editor and replace the content with the following XML:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="643c7-137">Die Einstellungen vom Typ `<PropertyGroup>` im obigen XML-Code sind in drei Gruppen unterteilt:</span><span class="sxs-lookup"><span data-stu-id="643c7-137">The `<PropertyGroup>` settings in the XML above is broken into three groups.</span></span> <span data-ttu-id="643c7-138">Die erste Gruppe enthält erforderliche Eigenschaften für ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="643c7-138">The first group deals with properties required for a NuGet package.</span></span> <span data-ttu-id="643c7-139">Die drei Einstellungen vom Typ `<Package` haben mit den NuGet-Paketeigenschaften zu tun, die Ihr Paket in einem NuGet-Feed identifizieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-139">The three `<Package` settings have to do with the NuGet package properties to identify your package on a NuGet feed.</span></span> <span data-ttu-id="643c7-140">Der Wert von `<PacakgeId>` dient insbesondere dazu, das Vorlagenpaket mit einem einzelnen Namen zu deinstallieren (anstatt mit einem Verzeichnispfad).</span><span class="sxs-lookup"><span data-stu-id="643c7-140">Specifically the `<PacakgeId>` value is used to uninstall the template pack with a single name instead of a directory path.</span></span> <span data-ttu-id="643c7-141">Er kann aber auch verwendet werden, um das Vorlagenpaket aus einem NuGet-Feed zu installieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-141">It can also be used to install the template pack from a NuGet feed.</span></span> <span data-ttu-id="643c7-142">Die übrigen Einstellungen (etwa `<Title>` und `<Tags>`) hängen mit den im NuGet-Feed angezeigten Metadaten zusammen.</span><span class="sxs-lookup"><span data-stu-id="643c7-142">The remaining settings such as `<Title>` and `<Tags>` have to do with metadata displayed on the NuGet feed.</span></span> <span data-ttu-id="643c7-143">Weitere Informationen zu NuGet-Einstellungen finden Sie unter [NuGet pack and restore as MSBuild targets](/nuget/reference/msbuild-targets) (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele).</span><span class="sxs-lookup"><span data-stu-id="643c7-143">For more information about NuGet settings, see [NuGet and MSBuild properties](/nuget/reference/msbuild-targets).</span></span>

<span data-ttu-id="643c7-144">Die Einstellung `<TargetFramework>` muss festgelegt werden, damit MSBuild ordnungsgemäß ausgeführt wird, wenn Sie das Projekt mithilfe des Befehls „pack“ kompilieren und packen.</span><span class="sxs-lookup"><span data-stu-id="643c7-144">The `<TargetFramework>` setting must be set so that MSBuild will run properly when you run the pack command to compile and pack the project.</span></span>

<span data-ttu-id="643c7-145">Die letzten drei Einstellungen dienen zur korrekten Konfiguration des Projekts, damit bei der Erstellung die Vorlagen im entsprechenden Ordner in das NuGet-Paket eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="643c7-145">The last three settings have to do with configuring the project correctly to include the templates in the appropriate folder in the NuGet pack when it's created.</span></span>

<span data-ttu-id="643c7-146">`<ItemGroup>` enthält zwei Einstellungen:</span><span class="sxs-lookup"><span data-stu-id="643c7-146">The `<ItemGroup>` contains two settings.</span></span> <span data-ttu-id="643c7-147">Die erste Einstellung (`<Content>`) schließt alles aus dem Ordner _templates_ als Inhalt ein.</span><span class="sxs-lookup"><span data-stu-id="643c7-147">First, the `<Content>` setting includes everything in the _templates_ folder as content.</span></span> <span data-ttu-id="643c7-148">Außerdem werden alle Ordner vom Typ _bin_ oder _obj_ ausgeschlossen, um zu verhindern, dass kompilierter Code eingeschlossen wird (falls Sie Ihre Vorlagen getestet und kompiliert haben).</span><span class="sxs-lookup"><span data-stu-id="643c7-148">It's also set to exclude any _bin_ folder or _obj_ folder to prevent any compiled code (if you tested and compiled your templates) from being included.</span></span> <span data-ttu-id="643c7-149">Die zweite Einstellung (`<Compile>`) schließt alle Codedateien von der Kompilierung aus – unabhängig davon, wo sie sich befinden.</span><span class="sxs-lookup"><span data-stu-id="643c7-149">Second, the `<Compile>` setting excludes all code files from compiling no matter where they're located.</span></span> <span data-ttu-id="643c7-150">Diese Einstellung verhindert, dass das für die Vorlagenpaketerstellung verwendete Projekt versucht, den Code in der Ordnerhierarchie _templates_ zu kompilieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-150">This setting prevents the project being used to create a template pack from trying to compile the code in the _templates_ folder hierarchy.</span></span>

## <a name="build-and-install"></a><span data-ttu-id="643c7-151">Erstellen und Installieren</span><span class="sxs-lookup"><span data-stu-id="643c7-151">Build and install</span></span>

<span data-ttu-id="643c7-152">Speichern Sie die Datei, und führen Sie anschließend den Befehl „pack“ aus.</span><span class="sxs-lookup"><span data-stu-id="643c7-152">Save this file and then run the pack command</span></span>

```console
dotnet pack
```

<span data-ttu-id="643c7-153">Dieser Befehl erstellt sowohl Ihr Projekt als auch ein NuGet-Paket im Ordner _working\bin\Debug_.</span><span class="sxs-lookup"><span data-stu-id="643c7-153">This command will build your project and create a NuGet package in This should be the _working\bin\Debug_ folder.</span></span>

```console
C:\working> dotnet pack
Microsoft (R) Build Engine version 16.2.0-preview-19278-01+d635043bd for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

<span data-ttu-id="643c7-154">Installieren Sie als Nächstes mithilfe des Befehls `dotnet new -i PATH_TO_NUPKG_FILE` die Vorlagenpaketdatei.</span><span class="sxs-lookup"><span data-stu-id="643c7-154">Next, install the template pack file with the `dotnet new -i PATH_TO_NUPKG_FILE` command.</span></span>

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Example templates: string extensions              stringext             [C#]              Common/Code
Console Application                               console               [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync          [C#]              Common/Console/C#8
Class library                                     classlib              [C#], F#, VB      Common/Library
```

<span data-ttu-id="643c7-155">Wenn Sie das NuGet-Paket in einen NuGet-Feed hochgeladen haben, können Sie den Befehl `dotnet new -i PACKAGEID` verwenden. `PACKAGEID` entspricht dabei der Einstellung `<PackageId>` aus der __ CSPROJ-Datei.</span><span class="sxs-lookup"><span data-stu-id="643c7-155">If you uploaded the NuGet package to a NuGet feed, you can use the `dotnet new -i PACKAGEID` command where `PACKAGEID` is the same as the `<PackageId>` setting from the _.csproj_ file.</span></span> <span data-ttu-id="643c7-156">Diese Paket-ID ist mit der NuGet-Paket-ID identisch.</span><span class="sxs-lookup"><span data-stu-id="643c7-156">This package ID is the same as the NuGet package identifier.</span></span>

## <a name="uninstall-the-template-pack"></a><span data-ttu-id="643c7-157">Deinstallieren des Vorlagenpakets</span><span class="sxs-lookup"><span data-stu-id="643c7-157">Uninstall the template pack</span></span>

<span data-ttu-id="643c7-158">Beim Entfernen eines Vorlagenpakets spielt es keine Rolle, ob Sie das Vorlagenpaket direkt über die __ NUPKG-Datei oder per NuGet-Feed installiert haben.</span><span class="sxs-lookup"><span data-stu-id="643c7-158">No matter how you installed the template pack, either with the _.nupkg_ file directly or by NuGet feed, removing a template pack is the same.</span></span> <span data-ttu-id="643c7-159">Verwenden Sie die Paket-ID (`<PackageId>`) der Vorlage, die Sie deinstallieren möchten.</span><span class="sxs-lookup"><span data-stu-id="643c7-159">Use the `<PackageId>` of the template you want to uninstall.</span></span> <span data-ttu-id="643c7-160">Mithilfe des Befehls `dotnet new -u` können Sie eine Liste der installierten Vorlagen abrufen.</span><span class="sxs-lookup"><span data-stu-id="643c7-160">You can get a list of templates that are installed by running the `dotnet new -u` command.</span></span>

```console
C:\working> dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      dotnet gitignore file (gitignore)
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)

... cut to save space ...

  NUnit3.DotNetNew.Template
    Templates:
      NUnit 3 Test Project (nunit) C#
      NUnit 3 Test Item (nunit-test) C#
      NUnit 3 Test Project (nunit) F#
      NUnit 3 Test Item (nunit-test) F#
      NUnit 3 Test Project (nunit) VB
      NUnit 3 Test Item (nunit-test) VB
  AdatumCorporation.Utility.Templates
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
```

<span data-ttu-id="643c7-161">Führen Sie `dotnet new -u AdatumCorporation.Utility.Templates` aus, um die Vorlage zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="643c7-161">Run `dotnet new -u AdatumCorporation.Utility.Templates` to uninstall the template.</span></span> <span data-ttu-id="643c7-162">Der Befehl `dotnet new` gibt Hilfeinformationen aus, in denen Ihre zuvor installierten Vorlagen nicht mehr enthalten sein sollten.</span><span class="sxs-lookup"><span data-stu-id="643c7-162">The `dotnet new` command will output help information that should omit the templates you previously installed.</span></span>

<span data-ttu-id="643c7-163">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="643c7-163">Congratulations!</span></span> <span data-ttu-id="643c7-164">Sie haben ein Vorlagenpaket installiert und deinstalliert.</span><span class="sxs-lookup"><span data-stu-id="643c7-164">you've installed and uninstalled a template pack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="643c7-165">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="643c7-165">Next steps</span></span>

<span data-ttu-id="643c7-166">Weitere Informationen zu Vorlagen (die Ihnen größtenteils bereits bekannt sein dürften) finden Sie im Artikel [Benutzerdefinierte Vorlagen für dotnet new](../tools/custom-templates.md).</span><span class="sxs-lookup"><span data-stu-id="643c7-166">To learn more about templates, most of which you've already learned, see the [Custom templates for dotnet new](../tools/custom-templates.md) article.</span></span>

* [<span data-ttu-id="643c7-167">dotnet/templating GitHub repo Wiki (GitHub-Repositorywiki dotnet/templating)</span><span class="sxs-lookup"><span data-stu-id="643c7-167">dotnet/templating GitHub repo Wiki</span></span>](https://github.com/dotnet/templating/wiki)
* [<span data-ttu-id="643c7-168">dotnet/dotnet-template-samples-GitHub-Repository</span><span class="sxs-lookup"><span data-stu-id="643c7-168">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
* [<span data-ttu-id="643c7-169">*template.json*-Schema im JSON-Schemaspeicher</span><span class="sxs-lookup"><span data-stu-id="643c7-169">*template.json* schema at the JSON Schema Store</span></span>](http://json.schemastore.org/template)