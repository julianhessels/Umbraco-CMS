# Umbraco CMS Architecture

The Umbraco CMS application is composed of multiple projects organized around core functionality, web UI, APIs, and persistence layers. The diagram below highlights the main components and how they relate to each other at a high level.

```mermaid
flowchart TD
    subgraph Web
        U_Web_UI["Umbraco.Web.UI<br/>(ASP.NET Core app)"]
        U_Web_Common["Umbraco.Web.Common"]
    end

    subgraph Core
        U_Core["Umbraco.Core"]
        U_Infrastructure["Umbraco.Infrastructure"]
        U_Cms["Umbraco.Cms"]
        U_PublishedCache["Umbraco.PublishedCache.HybridCache"]
    end

    subgraph APIs
        U_Api_Common["Umbraco.Cms.Api.Common"]
        U_Api_Delivery["Umbraco.Cms.Api.Delivery"]
        U_Api_Management["Umbraco.Cms.Api.Management"]
    end

    subgraph Persistence
        U_Persistence_EFCore["Umbraco.Cms.Persistence.EFCore"]
        U_Persistence_SQL["Umbraco.Cms.Persistence.SqlServer / Sqlite"]
    end

    subgraph Imaging
        U_ImageSharp["Umbraco.Cms.Imaging.ImageSharp"]
    end

    U_Web_UI --> U_Web_Common
    U_Web_Common --> U_Cms
    U_Cms --> U_Core
    U_Cms --> U_Infrastructure
    U_Cms --> U_PublishedCache
    U_Web_UI --> U_Api_Common
    U_Api_Common --> U_Api_Delivery
    U_Api_Common --> U_Api_Management
    U_Infrastructure --> U_Persistence_EFCore
    U_Infrastructure --> U_Persistence_SQL
    U_Infrastructure --> U_ImageSharp
```

This diagram presents a simplified overview. The `Umbraco.Web.UI` project hosts the ASP.NET Core application and depends on web-specific components in `Umbraco.Web.Common`. The CMS core functionality is provided by `Umbraco.Cms`, `Umbraco.Core`, `Umbraco.Infrastructure`, and caching implementations in `Umbraco.PublishedCache.HybridCache`. API projects provide REST endpoints for management and delivery scenarios, while persistence projects implement data storage via Entity Framework Core and database-specific providers. Imaging support is handled by projects such as `Umbraco.Cms.Imaging.ImageSharp`.

