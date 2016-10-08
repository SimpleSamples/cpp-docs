---
title: "Virtual List Controls"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 319f841f-e426-423a-8276-d93f965b0b45
caps.latest.revision: 11
manager: ghogen
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# Virtual List Controls
A virtual list control is a list view control that has the **LVS_OWNERDATA** style. This style enables the control to support an item count up to a `DWORD` (the default item count only extends to an `int`). However, the biggest advantage provided by this style is the ability to only have a subset of data items in memory at any one time. This allows the virtual list view control to lend itself for use with large databases of information, where specific methods of accessing data are already in place.  
  
> [!NOTE]
>  In addition to providing virtual list functionality in `CListCtrl`, MFC also provides the same functionality in the [CListView](../VS_visualcpp/CListView-Class.md) class.  
  
 There are some compatibility issues you should be aware of when developing virtual list controls. For more information, see the Compatibility Issues section of the List-View Controls topic in the Windows SDK.  
  
## Handling the LVN_GETDISPINFO Notification  
 Virtual list controls maintain very little item information. Except for the item selection and focus information, all item information is managed by the owner of the control. Information is requested by the framework via a **LVN_GETDISPINFO** notification message. To provide the requested information, the owner of the virtual list control (or the control itself) must handle this notification. This can easily be done using the Properties window (see [Mapping Messages to Functions](../VS_visualcpp/Mapping-Messages-to-Functions.md)). The resultant code should look something like the following example (where `CMyDialog` owns the virtual list control object and the dialog is handling the notification):  
  
 [!CODE [NVC_MFCControlLadenDialog#23](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCControlLadenDialog#23)]  
  
 In the handler for the **LVN_GETDISPINFO** notification message, you must check to see what type of information is being requested. The possible values are:  
  
-   `LVIF_TEXT` The `pszText` member must be filled in.  
  
-   `LVIF_IMAGE` The `iImage` member must be filled in.  
  
-   **LVIF_INDENT** The *iIndent* member must be filled in.  
  
-   `LVIF_PARAM` The *lParam* member must be filled in. (Not present for sub-items.)  
  
-   `LVIF_STATE` The *state* member must be filled in.  
  
 You should then supply whatever information is requested back to the framework.  
  
 The following example (taken from the body of the notification handler for the list control object) demonstrates one possible method by supplying information for the text buffers and image of an item:  
  
 [!CODE [NVC_MFCControlLadenDialog#24](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCControlLadenDialog#24)]  
  
## Caching and Virtual List Controls  
 Because this type of list control is intended for large data sets, it is recommended that you cache requested item data to improve retrieval performance. The framework provides a cache-hinting mechanism to assist in optimizing the cache by sending an **LVN_ODCACHEHINT** notification message.  
  
 The following example updates the cache with the range passed to the handler function.  
  
 [!CODE [NVC_MFCControlLadenDialog#25](../CodeSnippet/VS_Snippets_Cpp/NVC_MFCControlLadenDialog#25)]  
  
 For more information on preparing and maintaining a cache, see the Cache Management section of the List-View Controls topic in the Windows SDK.  
  
## Finding Specific Items  
 The **LVN_ODFINDITEM** notification message is sent by the virtual list control when a particular list control item needs to be found. The notification message is sent when the list view control receives quick key access or when it receives an **LVM_FINDITEM** message. Search information is sent in the form of an **LVFINDINFO** structure, which is a member of the **NMLVFINDITEM** structure. Handle this message by overriding the `OnChildNotify` function of your list control object and inside the body of the handler, check for the **LVN_ODFINDITEM** message. If found, perform the appropriate action.  
  
 You should be prepared to search for an item that matches the information given by the list view control. You should return the index of the item if successful, or -1 if no matching item is found.  
  
## See Also  
 [Using CListCtrl](../VS_visualcpp/Using-CListCtrl.md)   
 [Controls](../VS_visualcpp/Controls--MFC-.md)