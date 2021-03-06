---
title: "Designing a Business Data Connectivity Model | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "office-development"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "BDC [SharePoint development in Visual Studio], designing a model"
  - "Business Data Connectivity service [SharePoint development in Visual Studio], designing a model"
ms.assetid: 19cad8cf-8a82-4000-84cf-1e5aff54e5af
caps.latest.revision: 41
author: "gewarren"
ms.author: "gewarren"
manager: "ghogen"
---
# Designing a Business Data Connectivity Model
  You can develop a model for the Business Data Connectivity (BDC) service by adding entities and methods to a model file. An entity describes a collection of data fields. For example, an entity can represent a table in a database. A method performs a task such as adding, deleting, or updating data represented by the entities. For more information, see [Integrating Business Data into SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md).  
  
## Adding Entities  
 You can add an entity by dragging or copying an **Entity** from the Visual Studio **Toolbox** onto the BDC Designer. For more information, see [How to: Add an Entity to a Model](../sharepoint/how-to-add-an-entity-to-a-model.md).  
  
 Define the fields of the entity in a class. For example, you might add a field named `Address` to a `Customer` class. You can either add a new class to the project or use an existing class created by using other tools such as the Object Relational Designer (O/R Designer). The name of the entity and the name of the class that represents the entity do not have to match. You relate the class to the entity when you define the methods in your model.  
  
## Adding Methods  
 The BDC service calls methods in your model when users view, add, update, or delete information in a list or Web Part that is based on your model. You must add a method to the model for each task that the user can perform. Create methods by selecting any of the five basic method types from the **BDC Method Details** window. The following table describes the five basic methods of a BDC model.  
  
|Method|Description|  
|------------|-----------------|  
|Finder|Returns a collection of entity instances. Called when the user opens the list or Web Part. For more information, see [How to: Add a Finder Method](../sharepoint/how-to-add-a-finder-method.md).|  
|Specific Finder|Returns a specific entity instance. Called when a user views the details of a specific item in a list. For more information, see [How to: Add a Specific Finder Method](../sharepoint/how-to-add-a-specific-finder-method.md).|  
|Creator|Adds new data to the data source of an entity. Called when users choose the **New Item** button on the Ribbon of a list that is based on the model. For more information, see [How to: Add a Creator Method](../sharepoint/how-to-add-a-creator-method.md).|  
|Updater|Modifies the data in a list. Called when users update information in a list. For more information, see [How to: Add an Updater Method](../sharepoint/how-to-add-an-updater-method.md).|  
|Deleter|Removes data. Called when users delete an item from the list. For more information, see [How to: Add a Deleter Method](../sharepoint/how-to-add-a-deleter-method.md).|  
  
## Defining Method Parameters  
 When you create a method, Visual Studio adds the input and output parameters that are appropriate for the method type. These parameters are just placeholders. In most cases, you must modify the parameters so that they pass in or return the correct type of data. For example, by default, a Finder method returns a string. In most cases, you want to modify the return parameter of the Finder method so that it returns a collection of entities. You can accomplish that by modifying the type descriptor of the parameter. A type descriptor is a collection of attributes that describes the data type of a parameter. For more information, see [How to: Define the Type Descriptor of a Parameter](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
 Visual Studio enables you to copy type descriptors between parameters in the model. For example, you might define a type descriptor named `CustomerTD` for the return parameter of the `GetCustomer` method. You can copy the `CustomerTD` type descriptor in the **BDC Explorer**, and then paste that type descriptor to the input parameter of the `CreateCustomer` method. This prevents you from having to define the same type descriptor more than once.  
  
##  <a name="MethodInstances"></a> Method Instances  
 When you create a method, Visual Studio adds a default method instance. A method instance is a reference to a method, plus the default values for the parameters. A single method can have multiple method instances. Each instance is a combination of the method signature and a set of default values. For more information, see [How to: Define the Type Descriptor of a Parameter](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
 When you run the project, method instances appear in a drop-down list above the SharePoint list. Users can choose method instances to view the data.  
  
 To add default values to the method instance, you have to modify the XML of the model directly. For more information, see [DefaultValue](http://go.microsoft.com/fwlink/?LinkID=169279).  
  
## Adding Filter Descriptors  
 Consumers of the model might want to retrieve instances of an entity that match some criteria. To enable this functionality, you can add a filter descriptor to a method. Filter descriptors enable model consumers to filter method result sets by passing values to methods before they execute. For more information, see [How to: Add Filter Parameters to Operations to Limit Instances from the External System](http://go.microsoft.com/fwlink/?LinkID=169267).  
  
 SharePoint provides several features that enable users to provide filter values. For example, Business Data Web Parts provide a filter text box. Users can limit the data in a list by entering a value in the text box. For more information about how to add a filter descriptor to a method, see [How to: Add a Filter Descriptor to a Finder Method](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md).  
  
### Filter Descriptor Properties  
 You must set the value of the **Associated Type Descriptor**, **Name**, and **Type** properties of a filter descriptor. All other properties are optional.  
  
 The **Associated Type Descriptor** property relates the filter descriptor to an input parameter. When a user provides a filter value, the BDC service passes that value into the method by using the input parameter.  
  
 The **Type** property describes the filtering pattern that you want to use. In SharePoint, the filtering pattern you select affects the text that appears in the User Interface (UI). For example, for a Comparator filtering pattern, the text **is equal to** appears as a control above a Business Data Web Part. For more information about each filtering pattern, see [Types of Filters Supported by the BDC](http://go.microsoft.com/fwlink/?LinkId=169287).  
  
 For more information about the properties of a filter descriptor, see [FilterDescriptor](http://go.microsoft.com/fwlink/?LinkID=169280).  
  
### Providing Default Values  
 In some cases, the user might not provide a filter value. You can provide a default value by adding a default value to the method instance, or by setting the default value in the code of your method. For more information about how to add a default value to the method instance, see [MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282). For an example of how to set the default value of an input parameter in the code of your method, see [How to: Add a Filter Descriptor to a Finder Method](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md).  
  
## Validating the Model  
 You can validate your model during development. Visual Studio identifies issues that can prevent your model from behaving as expected. These issues appear in the Visual Studio **Error List**.  
  
 You can validate a model by opening the shortcut menu for the BDC Designer and then choosing **Validate**. If the model contains any errors, they appear in the **Error List**. You can quickly move the cursor to the code that contains an error by double-clicking the error in the list. As an alternative, you can choose the F8 or Shift+F8 keys repeatedly to step forward or backward through the errors in the list.  
  
 Validation errors can occur when the rules of the model are violated in some way. For example, if the **IsCollection** property of a type descriptor is set to **true**, but no child type descriptors exist, a validation error will appear. You might have to refer to the rules of a BDC model to understand some errors that appear in the Visual Studio **Error List**. For more information about the rules of a BDC model, see [BDCMetadata Schema](http://go.microsoft.com/fwlink/?LinkID=169275).  
  
## Debugging the Solution that Contains the Model  
 You can debug your code as you would debug any code in Visual Studio. To debug your code, set breakpoints anywhere in your code and then start the debugger. Visual Studio opens the SharePoint site. In SharePoint, create a list or Web Part that uses your business data. Then, you can step through your code. For more information about debugging SharePoint projects, see [Troubleshooting SharePoint Solutions](../sharepoint/troubleshooting-sharepoint-solutions.md).  
  
 You can also debug code in custom assemblies that you add to the project. However, to debug code in a custom assembly, you must add the assembly to the solution package. For more information, see [How to: Add and Remove Additional Assemblies](../sharepoint/how-to-add-and-remove-additional-assemblies.md).  
  
 For more information about adding a custom assembly to your project, see [How to: Include a Custom Assembly in a BDC Feature](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md).  
  
### Configuring BDC Security  
 You might have to modify your security settings in SharePoint before you can debug your solution. To modify these settings, open the Business Data Connectivity Service Application in the SharePoint 2010 Central Administration Web site. In the **Set Metadata Store Permissions** dialog box, add your user account, and then select any of the following options:  
  
|Task|Option|  
|----------|------------|  
|To deploy models to the BDC service.|Edit|  
|To create lists and Web Parts by using external content types (entities) in your model.|Selectable in Clients|  
|To create, read, update, and delete entity data.|Execute|  
  
 For more information about these settings, see [Business Data Connectivity service management](http://go.microsoft.com/fwlink/?LinkID=178883).  
  
 You can also set security permissions for individual models or external content types. For more information about how to set the security permissions of a model, see [BDC model management](http://go.microsoft.com/fwlink/?LinkID=178884). For more information about how to set the security permissions of an external content type, see [External content type management](http://go.microsoft.com/fwlink/?LinkID=178885).  
  
> [!NOTE]  
>  Use these settings to debug a solution on your local SharePoint Server. For more information about how to configure BDC-related security settings on production SharePoint server, see [Business Data Connectivity Services security overview](http://go.microsoft.com/fwlink/?LinkID=178886).  
  
### Retracting Models That Become Corrupt  
 The first time that you start the debugger, Visual Studio deploys the entire model to SharePoint. For each time thereafter, Visual Studio updates the model in SharePoint with any changes that you make between deployments.  
  
 There might be situations where you want Visual Studio to retract the model from SharePoint completely. For example, a model might become corrupt.  To redeploy your model to SharePoint, set the **Incremental Update** property of the model to **False**, and then start the debugger. The **Incremental Update** property appears in the **Properties** window when you select the node that represents the model in the **BDC Explorer**. By default, the name of the model is **BdcModel1**.  
  
### Changing Identifier Names of Entities in the Model  
 If you change the name of an identifier after you deploy the model, you might receive a deployment error. You cannot resolve this error by setting the **Incremental Update** property of the model to **False**. You must retract the model manually, and then deploy the solution again. For more information, see [Troubleshooting SharePoint Solutions](../sharepoint/troubleshooting-sharepoint-solutions.md). You can avoid this error by setting the **Incremental Update** property to **False** before you initially deploy the model.  
  
## Locating Documentation for BDC Model Elements  
 Visual Studio adds an XML element to the model for each entity, method, or other item that you create. Element attributes appear as properties in the **Properties** window. For information about the elements and attributes that Visual Studio generates as you design the model, see [BDCMetadata Schema](http://go.microsoft.com/fwlink/?LinkID=169275).  
  
## Related Topics  
  
|Title|Description|  
|-----------|-----------------|  
|[BDC Model Design Tools Overview](../sharepoint/bdc-model-design-tools-overview.md)|Describes the tools that you can use to visually design a model for the BDC.|  
|[How to: Add an Entity to a Model](../sharepoint/how-to-add-an-entity-to-a-model.md)|Shows you how to add external content types, or entities, to the model.|  
|[How to: Add a Finder Method](../sharepoint/how-to-add-a-finder-method.md)|Shows you how to add a method that enables users to view a list of entities in a list or Web Part.|  
|[How to: Add a Specific Finder Method](../sharepoint/how-to-add-a-specific-finder-method.md)|Shows you how to add a method that enables users to view the details of a specific entity.|  
|[How to: Add a Creator Method](../sharepoint/how-to-add-a-creator-method.md)|Shows you how to add a method that enables users to add records to a data source directly from a list or Web Part.|  
|[How to: Add a Deleter Method](../sharepoint/how-to-add-a-deleter-method.md)|Shows you how to add a method that enables users to remove data from a data source by using options in the User Interface (UI) of a list or Web Part.|  
|[How to: Add an Updater Method](../sharepoint/how-to-add-an-updater-method.md)|Shows you how to add a method that enables users to change data records in a data source directly from a list or Web Part.|  
|[How to: Add a Parameter to a Method](../sharepoint/how-to-add-a-parameter-to-a-method.md)|Shows you how to use the Method Details Window in Visual Studio to add input and return parameters to a method.|  
|[How to: Define the Type Descriptor of a Parameter](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|Shows you how to define parameter data types in the model.|  
|[How to: Define a Method Instance](../sharepoint/how-to-define-a-method-instance.md)|Shows you how to create an instance of a method that the BDC executes.|  
|[How to: Add a Filter Descriptor to a Finder Method](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|Shows you how to enable users to limit the number of instances returned by a Finder method.|  
|[Creating an Association Between Entities](../sharepoint/creating-an-association-between-entities.md)|Describes how you can define relationships between entities in the model. Business Data Web Parts, External Lists, and custom applications can display these data relationships in a user interface (UI).|  
|[How to: Create an Association between Entities](../sharepoint/how-to-create-an-association-between-entities.md)|Shows you how to define relationships between entities in the model.|  
|[Walkthrough: Creating an External List in SharePoint by Using Business Data](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|Provides step-by-step instructions that show you how to create and test a model that displays contacts in a SharePoint external list.|  
|[Integrating Business Data into SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)|Provides an overview of creating and designing models for the BDC service.|  
  
  