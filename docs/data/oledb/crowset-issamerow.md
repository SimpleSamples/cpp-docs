---
title: "CRowset::IsSameRow | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: ["cpp-windows"]
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: ["CRowset::IsSameRow", "CRowset.IsSameRow", "IsSameRow", "ATL::CRowset::IsSameRow", "ATL.CRowset.IsSameRow", "CRowset<TAccessor>::IsSameRow", "ATL.CRowset<TAccessor>.IsSameRow", "CRowset<TAccessor>.IsSameRow", "ATL::CRowset<TAccessor>::IsSameRow"]
dev_langs: ["C++"]
helpviewer_keywords: ["IsSameRow method"]
ms.assetid: 53cba847-52f5-4dd9-973f-bbe7454c425c
caps.latest.revision: 10
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
ms.workload: ["cplusplus", "data-storage"]
---
# CRowset::IsSameRow
Compares the specified row with the current row.  
  
## Syntax  
  
```  
  
      HRESULT IsSameRow(   
   HROW hRow    
) const throw( );  
```  
  
#### Parameters  
 `hRow`  
 [in] A handle to the row to compare to the current row.  
  
## Return Value  
 A standard `HRESULT`. `S_OK` indicates the rows are the same. For other values, see [IRowsetIndentity::IsSameRow](https://msdn.microsoft.com/en-us/library/ms719629.aspx) in the *OLE DB Programmer's Reference* in the Windows SDK.  
  
## Requirements  
 **Header:** atldbcli.h  
  
## See Also  
 [CRowset Class](../../data/oledb/crowset-class.md)