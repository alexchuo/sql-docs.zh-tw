---
title: 在 Updategram (SQLXML 4.0) 中指定註解式的對應結構描述 |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ce7e9b90c034643ba31df7f34425ff8203956b9c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>在 Updategram 中指定註解式對應結構描述 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題說明 Updategram 中指定的對應結構描述 (XSD 或 XDR) 要如何用來處理更新。 在 updategram 中，您可以提供資料表和資料行中的對應的元素和屬性在 updategram 中使用註解式的對應結構描述名稱[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在 updategram 中指定對應結構描述時，此 updategram 中指定的元素和屬性名稱必須對應到對應結構描述內的元素和屬性。  
  
 若要指定對應結構描述，您使用**對應結構描述**屬性**\<同步 >** 項目。 下列範例會示範兩個 updategram：使用簡單對應結構描述的 updategram 以及使用更複雜之結構描述的 updategram。  
  
> [!NOTE]  
>  本文件集假設您非常熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的範本和對應結構描述支援。 如需詳細資訊，請參閱[簡介註解式 XSD 結構描述 & #40;SQLXML 4.0 & #41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). 如需使用 XDR 的舊版應用程式，請參閱[Annotated XDR Schemas &#40;SQLXML 4.0 中已被取代&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="dealing-with-data-types"></a>處理資料類型  
 如果結構描述指定**映像**，**二進位**，或**varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料類型 (使用**sql: datatype**) 並不是指定 XML 資料類型，updategram 會假設 XML 資料類型為**二進位 base 64**。 如果您的資料是**bin.base**類型，您必須明確指定型別 (**dt:type=bin.base**或**類型 ="xsd:hexBinary"**)。  
  
 如果結構描述指定**dateTime**，**日期**，或**時間**XSD 資料類型，您也必須指定對應[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所使用的資料型別**sql: datatype ="dateTime"**。  
  
 當處理參數的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **money**類型，您必須明確指定**sql: datatype ="money"** 對應結構描述中的適當節點上。  
  
## <a name="examples"></a>範例  
 若要建立工作範例使用下列範例，您必須符合指定的需求[執行 SQLXML 範例的需求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 使用簡單對應結構描述建立 updategram  
 下列 XSD 結構描述 (SampleSchema.xml) 是對應的對應結構描述**\<客戶 >** 到 Sales.Customer 資料表的項目：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 下列 updategram 會將一筆記錄插入 Sales.Customer 資料表，並依賴之前的對應結構描述，適當地將此資料對應至資料表。 請注意，updategram 會使用相同的項目名稱， **\<客戶 >**、 結構描述中定義。 這是強制性的作法，因為 updategram 會指定特定的結構描述。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
2.  複製底下的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. 使用對應結構描述內指定的父子式關聯性插入記錄  
 結構描述元素可以產生關聯。 **\<Sql: relationship >** 項目會指定結構描述項目之間的父子式關聯性。 這項資訊是用來更新具有主索引鍵與外部索引鍵關聯性的對應資料表。  
  
 下列的對應結構描述 (SampleSchema.xml) 包含兩個項目， **\<順序 >** 和 **\<OD >**:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 下列 updategram 會使用這個 XSD 結構描述加入新的訂單詳細資料記錄 (  **\<OD >** 中的項目**\<之後 >** 區塊) 針對訂單 43860。 **對應結構描述**屬性用來在 updategram 中指定對應結構描述。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
2.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. 使用 XSD 結構描述內指定的父子式關聯性和反向註解來插入記錄  
 此範例說明如何 updategram 邏輯會使用 XSD 中指定的父子式關聯性來處理更新，以及如何**反向**註解。 如需有關**反向**註解，請參閱[sql: relationship 指定 sql: inverse 屬性&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)。  
  
 這個範例假設下列資料表處於**tempdb**資料庫：  
  
-   `Cust (CustomerID, CompanyName)`，其中 `CustomerID` 是主索引鍵  
  
-   `Ord (OrderID, CustomerID)`，其中 `CustomerID` 是參考 `CustomerID` 資料表內之 `Cust` 主索引鍵的外部索引鍵。  
  
 updategram 會使用以下 XSD 結構描述，將記錄插入 Cust 和 Ord 資料表中：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 在此範例中，XSD 結構描述具有**\<客戶 >** 和**\<順序 >** 項目，而且它會指定兩個項目之間的父子式關聯性。 它會識別**\<順序 >** 與父項目和**\<客戶 >** 為子元素。  
  
 此 updategram 處理邏輯會使用有關父子式關聯性的資訊來判斷哪些記錄會插入資料表中。 在此範例中，updategram 邏輯第一次嘗試將記錄插入 Ord 資料表 (因為**\<順序 >** 父系)，然後嘗試將記錄插入 Cust 資料表 (因為 **\<客戶 >** 是子系)。 但是，由於包含在資料庫資料表結構描述內之主索引鍵/外部索引鍵資訊的緣故，這項插入作業會造成資料庫中的外部索引鍵違規，而使得插入失敗。  
  
 若要指示要在更新作業期間反轉父子式關聯性的 updategram 邏輯**反向**上指定註解**\<關聯性 >** 項目。 因此，記錄會先加入到 Cust 資料表，然後再加入到 Ord 資料表，作業就會成功。  
  
 下列 updategram 會使用指定的 XSD 結構描述，將訂單 (OrderID=2) 插入到 Ord 資料表，並將客戶 (CustomerID='AAAAA') 插入到 Cust 資料表：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  建立這些資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
3.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
