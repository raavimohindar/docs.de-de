---
ms.openlocfilehash: fb78e1439a680a8dbb9fc0eb8afdeee3efef7ead
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768395"
---

<span data-ttu-id="6a4dc-101">Die [dotnet-install-Skripts](../../tools/dotnet-install-script.md) werden für die Automatisierung sowie für Installationen von **SDK** und **Runtime** durch Benutzer ohne Administratorrechte verwendet.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-101">The [dotnet-install scripts](../../tools/dotnet-install-script.md) are used for automation and non-admin installs of the **SDK** and **Runtime**.</span></span> <span data-ttu-id="6a4dc-102">Sie können das Skript unter <https://dot.net/v1/dotnet-install.sh> herunterladen.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-102">You can download the script from <https://dot.net/v1/dotnet-install.sh>.</span></span>

<span data-ttu-id="6a4dc-103">Das Skript installiert standardmäßig die neueste [LTS](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)-SDK-Version (Long-Term Support), die derzeit .NET Core 3.1 entspricht.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-103">The script defaults to installing the latest SDK [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 3.1.</span></span> <span data-ttu-id="6a4dc-104">Um die aktuelle Version zu installieren, bei der es sich möglicherweise nicht um eine LTS-Version handelt, nutzen Sie den Parameter `-c Current`.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-104">To install the current release, which may not be an (LTS) version, use the `-c Current` parameter.</span></span>

```bash
./dotnet-install.sh -c Current
```

<span data-ttu-id="6a4dc-105">Um die .NET Core-Runtime anstelle des SDK zu installieren, geben Sie den Parameter `--runtime` an.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-105">To install .NET Core Runtime instead of the SDK, use the `--runtime` parameter.</span></span>

```bash
./dotnet-install.sh -c Current --runtime aspnetcore
```

<span data-ttu-id="6a4dc-106">Sie können eine bestimmte Version installieren, indem Sie mit dem Parameter `-c` die gewünschte Version angeben.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-106">You can install a specific version by altering the `-c` parameter to indicate the specific version.</span></span> <span data-ttu-id="6a4dc-107">Mit dem folgenden Befehl wird .NET Core SDK 3.1 installiert.</span><span class="sxs-lookup"><span data-stu-id="6a4dc-107">The following command installs .NET Core SDK 3.1.</span></span>

```bash
./dotnet-install.sh -c 3.1
```

<span data-ttu-id="6a4dc-108">Weitere Informationen finden Sie in der [ Referenz zu dotnet-install-Skripts](../../tools/dotnet-install-script.md).</span><span class="sxs-lookup"><span data-stu-id="6a4dc-108">For more information, see [dotnet-install scripts reference](../../tools/dotnet-install-script.md).</span></span>