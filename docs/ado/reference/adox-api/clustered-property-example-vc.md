---
title: 叢集屬性範例 （VC + +） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Clustered property [ADOX], VC++ example
ms.assetid: b993e357-3e2e-48a7-a627-76909160c97f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c8fcc028770a7d2d2b0c64b1f9f0630c4679071
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="clustered-property-example-vc"></a>Clustered 的屬性範例 （VC + +）
這個範例會示範[Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)屬性[索引](../../../ado/reference/adox-api/index-object-adox.md)。 請注意，Microsoft Jet 資料庫不支援叢集的索引，因此這個範例會傳回**False**如**Clustered**屬性中的所有索引*Northwind*資料庫。  
  
```  
// BeginClusteredCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ClusteredX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   ClusteredX();  
   ::CoUninitialize();  
}  
  
void ClusteredX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _IndexPtr m_pIndex = NULL;  
  
   // Define other variables here  
   _variant_t vIndex;  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      // Connect to the catalog.  
      m_pCatalog->PutActiveConnection("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
      // Enumerate Tables.  
      for (short iTable = 0 ; iTable < m_pCatalog->Tables->Count ; iTable++ ) {  
         vIndex = iTable;  
         m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
         // Enumerate Indexes.  
         for (short iIndex = 0 ; iIndex < m_pTable->Indexes->Count ; iIndex++) {  
            vIndex = iIndex;  
            m_pIndex = m_pTable->Indexes->GetItem(vIndex);  
            cout << m_pTable->Name << "   " ;  
            cout << m_pIndex->Name << "   " << (m_pIndex->GetClustered() ? "True" : "False") << endl;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in ClusteredX...."<< endl;  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [Clustered 的屬性 (ADOX)](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
