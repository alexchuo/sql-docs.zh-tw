---
title: "與 common_table_expression (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITH common_table_expression
- WITH_TSQL
- WITH
- common table expression
dev_langs:
- TSQL
helpviewer_keywords:
- WITH common_table_expression clause
- CTEs
- hierarchical queries [SQL Server], WITH common_table_expression
- recursive CTEs [SQL Server]
- recursive queries [SQL Server]
- common table expressions
- MAXRECURSION hint
- clauses [SQL Server], WITH common_table_expression
ms.assetid: 27cfb819-3e8d-4274-8bbe-cbbe4d9c2e23
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a065ef1f5c21d0fb5a458d55108acd8a9fd0678e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="with-commontableexpression-transact-sql"></a>WITH common_table_expression (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定稱為通用資料表運算式 (CTE) 的暫存具名結果集。 這是從簡單查詢衍生而來，定義在單一 SELECT、INSERT、UPDATE 或 DELETE 陳述式的執行範圍內。 您也可以在 CREATE VIEW 陳述式中使用這個子句，作為用來定義 SELECT 陳述式的一部分。 通用資料表運算式可以包括指向本身的參考。 這稱為遞迴通用資料表運算式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
  
<common_table_expression>::=  
    expression_name [ ( column_name [ ,...n ] ) ]  
    AS  
    ( CTE_query_definition )  
```  
  
## <a name="arguments"></a>引數  
 *expression_name*  
是通用資料表運算式的有效識別項。 *expression_name*都必須使用不同的名稱的任何其他通用資料表運算式定義中相同 WITH \<common_table_expression > 子句，但*expression_name*可以是相同的名稱基底資料表或檢視表。 所有參考*expression_name*查詢中使用通用資料表運算式並不是基底物件。
  
 *column_name*  
 在一般資料表運算式中，指定資料行名稱。 在單一 CTE 定義內，名稱不能重複。 指定資料行名稱的數目必須符合的結果集中的資料行數目*個 CTE_query_definition*。 只有在查詢定義提供了所有結果資料行的個別名稱時，資料行名稱清單才是選擇性的。  
  
 *個 CTE_query_definition*  
 指定其結果集擴展一般資料表運算式的 SELECT 陳述式。 SELECT 陳述式*個 CTE_query_definition*必須符合建立檢視時，除了 CTE 不能定義另一個 CTE 的相同需求。 如需詳細資訊，請參閱 < 備註 > 一節和[CREATE VIEW &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 如果有一個以上*個 CTE_query_definition*是定義，聯結查詢定義必須由下列其中一種設定運算子： UNION ALL、 UNION、 EXCEPT 或 INTERSECT。  
  
## <a name="remarks"></a>備註  
  
## <a name="guidelines-for-creating-and-using-common-table-expressions"></a>建立和使用通用資料表運算式的方針  
 下列方針適用於非遞迴的通用資料表運算式。 如需適用於遞迴通用資料表運算式的方針，請參閱下面的「定義和使用遞迴通用資料表運算式的方針」。  
  
-   CTE 之後必須接著參考部分或所有 CTE 資料行的單一 INSERT、UPDATE 或 DELETE 陳述式。 您也可以在 CREATE VIEW 陳述式中，將 CTE 指定為用來定義檢視的 SELECT 陳述式的一部分。  
  
-   您可以在非遞迴的 CTE 中，定義多個 CTE 查詢定義。 這些定義必須由下列其中一個設定運算子所組合：UNION ALL、UNION、INTERSECT 或 EXCEPT。  
  
-   CTE 可以參考它本身，以及先前在相同 WITH 子句中所定義的 CTE。 不允許向前參考。  
  
-   不允許在 CTE 中指定多個 WITH 子句。 例如，如果*個 CTE_query_definition*包含子查詢，以定義另一個 CTE 的子句，這個子查詢不能包含巢狀。  
  
-   下列子句不能在*個 CTE_query_definition*:  
  
    -   ORDER BY (除非指定了 TOP 子句)  
  
    -   INTO  
  
    -   含有查詢提示的 OPTION 子句  
  
    -   FOR BROWSE  
  
-   當批次中的陳述式使用 CTE 時，在 CTE 之前的陳述式，後面必須接著分號。  
  
-   參考 CTE 的查詢可用來定義資料指標。  
  
-   在 CTE 中，可以參考遠端伺服器的資料表。  
  
-   當執行 CTE 時，任何參考 CTE 的提示都可能如同在查詢中參考檢視表的提示，與 CTE 存取基礎資料表時所發現的其他提示衝突。 當這種情況發生時，查詢會傳回錯誤：  
  
## <a name="guidelines-for-defining-and-using-recursive-common-table-expressions"></a>定義和使用遞迴通用資料表運算式的方針  
 下列方針適用於定義遞迴通用資料表運算式：  
  
-   遞迴 CTE 定義必須包含至少兩個 CTE 查詢定義，錨點成員和遞迴成員各一個。 您可以定義多個錨點成員和遞迴成員；不過，所有錨點成員查詢定義都必須放在第一個遞迴成員定義的前面。 除非 CTE 查詢定義參考 CTE 本身，否則，它們都是錨點成員。  
  
-   錨點成員必須由下列其中一個設定運算子所組合：UNION ALL、UNION、INTERSECT 或 EXCEPT。 在最後一個錨點成員和第一個遞迴成員之間，以及在組合多個成員時，UNION ALL 是唯一允許使用的設定運算子。  
  
-   錨點和遞迴成員中的資料行數目必須相同。  
  
-   遞迴成員資料行的資料類型必須與錨點成員中對應資料行的資料類型相同。  
  
-   遞迴成員的 FROM 子句必須一次只能參考 CTE *expression_name*。  
  
-   中不允許下列項目*個 CTE_query_definition*的遞迴成員：  
  
    -   SELECT DISTINCT  
  
    -   GROUP BY  
  
    -   PIVOT (當資料庫相容性層級為 110 以上時。 請參閱[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。)  
  
    -   HAVING  
  
    -   純量彙總  
  
    -   頂端  
  
    -   LEFT、RIGHT、OUTER JOIN (允許 INNER JOIN)  
  
    -   子查詢  
  
    -   套用至內 CTE 之遞迴參考的提示*個 CTE_query_definition*。  
  
 下列方針適用於使用遞迴通用資料表運算式：  
  
-   遞迴 CTE 能夠傳回的所有資料行都可為 Null，不論參與的 SELECT 陳述式所傳回之資料行的 Null 屬性為何，都是如此。  
  
-   組合不正確的遞迴 CTE 可能會造成無限迴圈。 例如，若遞迴成員查詢定義對父資料行與子資料行傳回相同的值，就會建立無限迴圈。 若要防止無限迴圈，您可以在 INSERT、UPDATE、DELETE 或 SELECT 陳述式的 OPTION 子句中使用 MAXRECURSION 提示以及 0 和 32,767 之間的值，來限制特定陳述式所能使用的遞迴層級數目。 這可讓您控制陳述式的執行，直到產生迴圈的程式碼問題解決為止。 伺服器範圍的預設值是 100。 當指定 0 時，不會套用任何限制。 每個陳述式只能指定一個 MAXRECURSION 值。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
-   您不能利用包含遞迴通用資料表運算式的檢視來更新資料。  
  
-   資料指標可以利用 CTE 在查詢中定義。 CTE 是*select_statement*定義資料指標的結果集的引數。 遞迴 CTE 只能使用僅限向前快轉和靜態 (快照集) 資料指標。 如果在遞迴 CTE 中指定了另一種資料指標類型，就會將資料指標類型轉換成靜態。  
  
-   在 CTE 中，可以參考遠端伺服器的資料表。 如果在 CTE 遞迴成員參考遠端伺服器，便會為每個遠端資料表各建立一項多工緩衝處理，以便在本機重複存取資料表。 如果它是 CTE 查詢，索引多工緩衝處理/延遲多工緩衝處理會顯示在查詢計劃中，而且將會有額外的 WITH STACK 述詞。 這是確認適當遞迴的一種方式。  
  
-   CTE 遞迴部分中的分析和彙總函式會套用至目前遞迴層級的集合，而不會套用至 CTE 的集合。 ROW_NUMBER 之類的函數只會針對目前遞迴層級傳遞給它們的資料子集運作，而不會針對傳遞給 CTE 遞迴部分的整個資料集運作。 如需詳細資訊，請參閱 < 範例 k。 使用分析函數在遞迴 CTE 所示。  
  
## <a name="features-and-limitations-of-common-table-expressions-in-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>常見的功能和限制資料表中的運算式[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 在 Cte 的目前實作[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]具有下列功能和限制：  
  
-   CTE 可以指定在**選取**陳述式。  
  
-   CTE 可以指定在**CREATE VIEW**陳述式。  
  
-   CTE 可以指定在**CREATE TABLE AS SELECT** (CTAS) 陳述式。  
  
-   CTE 可以指定在**建立遠端 TABLE AS SELECT** (CRTAS) 陳述式。  
  
-   CTE 可以指定在**CREATE EXTERNAL TABLE AS SELECT** (CETAS) 陳述式。  
  
-   從 CTE 可以參考遠端資料表。  
  
-   從 CTE 可以參考外部資料表。  
  
-   在 CTE 中，可以定義多個 CTE 查詢定義。  
  
-   CTE 後面必須接著單一**選取**陳述式。 **插入**，**更新**，**刪除**，和**合併**不支援陳述式。  
  
-   不支援通用資料表運算式，其中包含參考本身 （遞迴通用資料表運算式）。  
  
-   指定多個**WITH**不允許在 CTE 中的子句。 例如，如果個 CTE_query_definition 包含子查詢，這個子查詢不能包含巢狀**WITH**定義另一個 CTE 的子句。  
  
-   **ORDER BY**子句不能在個 CTE_query_definition，除非**頂端**指定子句。  
  
-   當批次中的陳述式使用 CTE 時，在 CTE 之前的陳述式，後面必須接著分號。  
  
-   當項目來準備陳述式中使用**sp_prepare**，Cte 的行為相同方式其他**選取**PDW 中的陳述式。 不過，如果 Cte 被當做一部分 CETAS 做好**sp_prepare**，行為可以延後從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和其他的 PDW 陳述式，因為方式繫結，則實作**sp_prepare**。 如果**選取**，參考 CTE 使用錯誤的資料行不存在於 CTE， **sp_prepare**偵測錯誤，但此錯誤將會擲回時不會通過**sp_execute**改為。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-simple-common-table-expression"></a>A. 建立簡單的通用資料表運算式  
 下列範例顯示在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 中每個業務人員每年的銷售訂單總數。  
  
```  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="b-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>B. 利用通用資料表運算式來限制計數和報告平均值  
 下列範例顯示業務人員所有年度的平均銷售訂單數目。  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="c-using-multiple-cte-definitions-in-a-single-query"></a>C. 在單一查詢中使用多個 CTE 定義  
 下列範例會示範如何在單一查詢中定義一個以上的 CTE。 請注意，逗號會用來分隔 CTE 查詢的定義。 以貨幣格式顯示貨幣金額的 FORMAT 函數會在 SQL Server 2012 和更新版本中提供。  
  
```  
  
WITH Sales_CTE (SalesPersonID, TotalSales, SalesYear)  
AS  
-- Define the first CTE query.  
(  
    SELECT SalesPersonID, SUM(TotalDue) AS TotalSales, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
       GROUP BY SalesPersonID, YEAR(OrderDate)  
  
)  
,   -- Use a comma to separate multiple CTE definitions.  
  
-- Define the second CTE query, which returns sales quota data by year for each sales person.  
Sales_Quota_CTE (BusinessEntityID, SalesQuota, SalesQuotaYear)  
AS  
(  
       SELECT BusinessEntityID, SUM(SalesQuota)AS SalesQuota, YEAR(QuotaDate) AS SalesQuotaYear  
       FROM Sales.SalesPersonQuotaHistory  
       GROUP BY BusinessEntityID, YEAR(QuotaDate)  
)  
  
-- Define the outer query by referencing columns from both CTEs.  
SELECT SalesPersonID  
  , SalesYear  
  , FORMAT(TotalSales,'C','en-us') AS TotalSales  
  , SalesQuotaYear  
  , FORMAT (SalesQuota,'C','en-us') AS SalesQuota  
  , FORMAT (TotalSales -SalesQuota, 'C','en-us') AS Amt_Above_or_Below_Quota  
FROM Sales_CTE  
JOIN Sales_Quota_CTE ON Sales_Quota_CTE.BusinessEntityID = Sales_CTE.SalesPersonID  
                    AND Sales_CTE.SalesYear = Sales_Quota_CTE.SalesQuotaYear  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
 以下為部分結果集。  
  
```  
  
SalesPersonID SalesYear   TotalSales    SalesQuotaYear SalesQuota  Amt_Above_or_Below_Quota  
------------- ---------   -----------   -------------- ---------- ----------------------------------   
  
274           2005        $32,567.92    2005           $35,000.00  ($2,432.08)  
274           2006        $406,620.07   2006           $455,000.00 ($48,379.93)  
274           2007        $515,622.91   2007           $544,000.00 ($28,377.09)  
274           2008        $281,123.55   2008           $271,000.00  $10,123.55  
  
```  
  
### <a name="d-using-a-recursive-common-table-expression-to-display-multiple-levels-of-recursion"></a>D. 利用遞迴通用資料表運算式來顯示多層級的遞迴  
 下列範例會顯示經理及向經理提出報告的員工的階層式清單。 此範例會開始建立並擴展 `dbo.MyEmployees` 資料表。  
  
```  
-- Create an Employee table.  
CREATE TABLE dbo.MyEmployees  
(  
EmployeeID smallint NOT NULL,  
FirstName nvarchar(30)  NOT NULL,  
LastName  nvarchar(40) NOT NULL,  
Title nvarchar(50) NOT NULL,  
DeptID smallint NOT NULL,  
ManagerID int NULL,  
 CONSTRAINT PK_EmployeeID PRIMARY KEY CLUSTERED (EmployeeID ASC)   
);  
-- Populate the table with values.  
INSERT INTO dbo.MyEmployees VALUES   
 (1, N'Ken', N'Sánchez', N'Chief Executive Officer',16,NULL)  
,(273, N'Brian', N'Welcker', N'Vice President of Sales',3,1)  
,(274, N'Stephen', N'Jiang', N'North American Sales Manager',3,273)  
,(275, N'Michael', N'Blythe', N'Sales Representative',3,274)  
,(276, N'Linda', N'Mitchell', N'Sales Representative',3,274)  
,(285, N'Syed', N'Abbas', N'Pacific Sales Manager',3,273)  
,(286, N'Lynn', N'Tsoflias', N'Sales Representative',3,285)  
,(16,  N'David',N'Bradley', N'Marketing Manager', 4, 273)  
,(23,  N'Mary', N'Gibson', N'Marketing Specialist', 4, 16);  
```  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
ORDER BY ManagerID;  
GO  
```  
  
### <a name="e-using-a-recursive-common-table-expression-to-display-two-levels-of-recursion"></a>E. 利用遞迴通用資料表運算式來顯示兩個層級的遞迴  
 下列範例會顯示經理及向經理提出報告的員工。 傳回的層級數目只限兩個。  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
WHERE EmployeeLevel <= 2 ;  
GO  
  
```  
  
### <a name="f-using-a-recursive-common-table-expression-to-display-a-hierarchical-list"></a>F. 利用遞迴通用資料表運算式來顯示階層式清單  
 下列範例是以範例 D 為基礎所建立，它加入了經理和員工的姓名及其職稱。 各個層級會進行縮排，更明顯地強調經理和員工的階層。  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(Name, Title, EmployeeID, EmployeeLevel, Sort)  
AS (SELECT CONVERT(varchar(255), e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        1,  
        CONVERT(varchar(255), e.FirstName + ' ' + e.LastName)  
    FROM dbo.MyEmployees AS e  
    WHERE e.ManagerID IS NULL  
    UNION ALL  
    SELECT CONVERT(varchar(255), REPLICATE ('|    ' , EmployeeLevel) +  
        e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        EmployeeLevel + 1,  
        CONVERT (varchar(255), RTRIM(Sort) + '|    ' + FirstName + ' ' +   
                 LastName)  
    FROM dbo.MyEmployees AS e  
    JOIN DirectReports AS d ON e.ManagerID = d.EmployeeID  
    )  
SELECT EmployeeID, Name, Title, EmployeeLevel  
FROM DirectReports   
ORDER BY Sort;  
GO  
```  
  
### <a name="g-using-maxrecursion-to-cancel-a-statement"></a>G. 利用 MAXRECURSION 來取消陳述式  
 您可以利用 `MAXRECURSION` 來防止形式不良的遞迴 CTE 進入無限迴圈。 下列範例會刻意建立無限迴圈，然後利用 `MAXRECURSION` 提示，將遞迴層級限制為 2。  
  
```  
USE AdventureWorks2012;  
GO  
--Creates an infinite loop  
WITH cte (EmployeeID, ManagerID, Title) as  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title  
    FROM cte   
    JOIN  dbo.MyEmployees AS e   
        ON cte.ManagerID = e.EmployeeID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT EmployeeID, ManagerID, Title  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 更正編碼錯誤之後，就不再需要 MAXRECURSION。 下列範例會顯示更正的程式碼。  
  
```  
USE AdventureWorks2012;  
GO  
WITH cte (EmployeeID, ManagerID, Title)  
AS  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT  e.EmployeeID, e.ManagerID, e.Title  
    FROM dbo.MyEmployees AS e  
    JOIN cte ON e.ManagerID = cte.EmployeeID  
)  
SELECT EmployeeID, ManagerID, Title  
FROM cte;  
GO  
```  
  
### <a name="h-using-a-common-table-expression-to-selectively-step-through-a-recursive-relationship-in-a-select-statement"></a>H. 利用通用資料表運算式，在 SELECT 陳述式中選擇性地逐步執行遞迴關聯性  
 下列範例會顯示建立 `ProductAssemblyID = 800` 的自行車時，所需要之產品組件和元件的階層。  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
SELECT AssemblyID, ComponentID, Name, PerAssemblyQty, EndDate,  
        ComponentLevel   
FROM Parts AS p  
    INNER JOIN Production.Product AS pr  
    ON p.ComponentID = pr.ProductID  
ORDER BY ComponentLevel, AssemblyID, ComponentID;  
GO  
```  
  
### <a name="i-using-a-recursive-cte-in-an-update-statement"></a>I. 在 UPDATE 陳述式中使用遞迴 CTE  
 下列範例會更新`PerAssemblyQty`值可用來建置產品 ' Road-550-W Yellow，44' 的所有組件`(ProductAssemblyID``800`)。 通用資料表運算式會傳回一份階層式清單，其中包含用來建立 `ProductAssemblyID 800` 的組件、用來建立這些組件的元件等等。 只會修改通用資料表運算式所傳回的資料列。  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
### <a name="j-using-multiple-anchor-and-recursive-members"></a>J. 使用多個錨點和遞迴成員  
 下列範例會利用多個錨點和遞迴成員來傳回指定人員的所有上階。 它會建立一份資料表，且會插入值來建立遞迴 CTE 所傳回的家族族譜。  
  
```  
-- Genealogy table  
IF OBJECT_ID('dbo.Person','U') IS NOT NULL DROP TABLE dbo.Person;  
GO  
CREATE TABLE dbo.Person(ID int, Name varchar(30), Mother int, Father int);  
GO  
INSERT dbo.Person   
VALUES(1, 'Sue', NULL, NULL)  
      ,(2, 'Ed', NULL, NULL)  
      ,(3, 'Emma', 1, 2)  
      ,(4, 'Jack', 1, 2)  
      ,(5, 'Jane', NULL, NULL)  
      ,(6, 'Bonnie', 5, 4)  
      ,(7, 'Bill', 5, 4);  
GO  
-- Create the recursive CTE to find all of Bonnie's ancestors.  
WITH Generation (ID) AS  
(  
-- First anchor member returns Bonnie's mother.  
    SELECT Mother   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION  
-- Second anchor member returns Bonnie's father.  
    SELECT Father   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION ALL  
-- First recursive member returns male ancestors of the previous generation.  
    SELECT Person.Father  
    FROM Generation, Person  
    WHERE Generation.ID=Person.ID  
UNION ALL  
-- Second recursive member returns female ancestors of the previous generation.  
    SELECT Person.Mother  
    FROM Generation, dbo.Person  
    WHERE Generation.ID=Person.ID  
)  
SELECT Person.ID, Person.Name, Person.Mother, Person.Father  
FROM Generation, dbo.Person  
WHERE Generation.ID = Person.ID;  
GO  
```  
  
###  <a name="bkmkUsingAnalyticalFunctionsInARecursiveCTE"></a>K。 在遞迴 CTE 中使用分析函數  
 下列範例顯示在 CTE 遞迴部分中使用分析或彙總函式時可能會發生的錯誤。  
  
```  
DECLARE @t1 TABLE (itmID int, itmIDComp int);  
INSERT @t1 VALUES (1,10), (2,10);   
  
DECLARE @t2 TABLE (itmID int, itmIDComp int);   
INSERT @t2 VALUES (3,10), (4,10);   
  
WITH vw AS  
 (  
    SELECT itmIDComp, itmID  
    FROM @t1  
  
    UNION ALL  
  
    SELECT itmIDComp, itmID  
    FROM @t2  
)   
,r AS  
 (  
    SELECT t.itmID AS itmIDComp  
           , NULL AS itmID  
           ,CAST(0 AS bigint) AS N  
           ,1 AS Lvl  
    FROM (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) AS t (itmID)   
  
UNION ALL  
  
SELECT t.itmIDComp  
    , t.itmID  
    , ROW_NUMBER() OVER(PARTITION BY t.itmIDComp ORDER BY t.itmIDComp, t.itmID) AS N  
    , Lvl + 1  
FROM r   
    JOIN vw AS t ON t.itmID = r.itmIDComp  
)   
  
SELECT Lvl, N FROM r;  
```  
  
 下列結果是此查詢的預期結果。  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    4  
2    3  
2    2  
2    1  
```  
  
 下列結果是此查詢的實際結果。  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    1  
2    1  
2    1  
2    1  
```  
  
 `N` 會針對 CTE 遞迴部分的每個行程傳回 1，因為只有該遞迴層級的資料子集會傳遞給 `ROWNUMBER`。 對於此查詢遞迴部分的每個反覆運算，只有一個資料列會傳遞給 `ROWNUMBER`。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-creating-a-simple-common-table-expression"></a>L. 建立簡單的通用資料表運算式  
 下列範例顯示在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 中每個業務人員每年的銷售訂單總數。  
  
```  
-- Uses AdventureWorks  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="m-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>M. 利用通用資料表運算式來限制計數和報告平均值  
 下列範例顯示業務人員所有年度的平均銷售訂單數目。  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="n-using-a-common-table-expression-within-a-ctas-statement"></a>N. 利用通用資料表運算式內的 CTAS 陳述式  
 下列範例會建立新的資料表包含每個銷售代表在每年的銷售訂單總數[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE SalesOrdersPerYear  
WITH  
(  
    DISTRIBUTION = HASH(SalesPersonID)  
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="o-using-a-common-table-expression-within-a-cetas-statement"></a>O. 利用通用資料表運算式內 CETAS 陳述式  
 下列範例會建立新的外部資料表包含每個銷售代表在每年的銷售訂單總數[!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]。  
  
```  
-- Uses AdventureWorks  
  
CREATE EXTERNAL TABLE SalesOrdersPerYear  
WITH  
(  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:5000/files/Customer',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|' )   
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="p-using-multiple-comma-separated-ctes-in-a-statement"></a>P. 使用多個以逗號分隔 Cte 的陳述式中  
 下列範例會示範在單一陳述式中包含兩個 Cte。 Cte 不可以是巢狀 （沒有遞迴）。  
  
```  
WITH   
 CountDate (TotalCount, TableName) AS  
    (  
     SELECT COUNT(datekey), 'DimDate' FROM DimDate  
    ) ,  
 CountCustomer (TotalAvg, TableName) AS  
    (  
     SELECT COUNT(CustomerKey), 'DimCustomer' FROM DimCustomer  
    )  
SELECT TableName, TotalCount FROM CountDate  
UNION ALL  
SELECT TableName, TotalAvg FROM CountCustomer;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [除了及 INTERSECT &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
