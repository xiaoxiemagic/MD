#### README

# 







---





>cfdjisa cdasjjj 
>
>







`ffffff`







~~~mysql
select a.* from  (SELECT a.ID, a.SeaExportID, a.OrderCode, a.CanSeeID, a.CustomCode, a.FeeTypeID,  a.ReceiveID, a.Money, a.CurrencyID, a.CurrencyRate, a.RMBMoney, a.InvoiceCode,  a.Remark, a.FKCode, b.JieDanDeptID AS DeptID, a.CreaterID, a.CreateTime,  a.SupplierOrCustomerID, a.GetOrPay, a.BillID, a.Status, a.GetAndPay,    CONVERT(char(10), b.OrderTime, 120) AS time, fee.FeeName AS feeName,    dept.DeptName AS deptName, users.UserName AS username,  case when getorpay=0 then cust.CustomerName else cust1.ShortName end AS cust, b.ShipName, b.FlightNo,  b.ShipName + '/' + b.FlightNo AS transportName, b.CostCenter AS po,  b.Declear_NO AS booking, CONVERT(char(10), b.ETD, 120) AS ETD,  CASE WHEN len(b.MainTransCode) > 0 AND len(b.SubTransCode)> 0   THEN b.MainTransCode + '_' + b.SubTransCode ELSE b.MainTransCode END AS TransCode, b.MainTransCode, b.SubTransCode, port.DetailName AS PortArea,  b.Supplier AS proxy, b.DestinationPort AS dest, cust.PinYin, b.JobType,  CONVERT(char(10), b.OrderTime, 120) AS OrderDate, CONVERT(char(10), b.SendTime,120) AS SendTime, CONVERT(char(10), b.DeclearTime, 120) AS BaoGuan,  CONVERT(char(10), b.ArriveTime, 120) AS ArriveTime, b.ProductName AS GoodName,  b.Count AS number, b.Weight, b.WarehouseArea AS ware, b.Contract_NO, m.mendian,  jdc.CustomerName AS jdcw, address.Address AS address, a.SupplierOrCustomerID as CustomerID, b.Amount,  a.CreaterTypeID, a.RateChanged, b.TransType,  cw.CustomerName AS JSCustomerName, b.JDCustomerID, b.note AS OrderRemark,b.WarehouseNumber,  CASE WHEN b.CustomsMode = 1 THEN '直转进境' WHEN b.CustomsMode = 2 THEN '预申报进境' WHEN b.CustomsMode = 3 THEN '区内转关' WHEN b.CustomsMode = 4 THEN '5+2进境' WHEN b.CustomsMode = 5 THEN '转关出境 ' WHEN b.CustomsMode = 6 THEN '5+2出境' END AS CustomsMode, b.Path,b.JieDanDeptID ,'SSClearCustomsFee' as feeTableName,b.DeclearTime   FROM SSClearCustomsOrderVW AS b   LEFT OUTER JOIN (SELECT   a.ID, a.SeaExportID, a.OrderCode, a.CanSeeID, a.CustomCode, a.FeeTypeID,  a.ReceiveID, a.Money, a.CurrencyID, a.CurrencyRate, a.RMBMoney, a.InvoiceCode,  a.Remark, a.FKCode,  a.CreaterID, a.CreateTime,  a.SupplierOrCustomerID, a.GetOrPay, a.BillID, a.Status, a.GetAndPay,cust.CustomerName AS cust, a.CreaterTypeID, a.RateChanged,a.DeptID FROM    SSClearCustomsFee  as a  left outer join CWCustomer AS cust ON cust.ID = a.SupplierOrCustomerID  where a.getorpay=0 and a.status!=-1  union SELECT    a.ID, a.SeaExportID, a.OrderCode, a.CanSeeID, a.CustomCode, a.FeeTypeID,  a.ReceiveID, a.Money, a.CurrencyID, a.CurrencyRate, a.RMBMoney, a.InvoiceCode,  a.Remark,a.FKCode,  a.CreaterID, a.CreateTime,  a.SupplierOrCustomerID, a.GetOrPay, a.BillID, a.Status, a.GetAndPay,cust.SupplierName AS cust, a.CreaterTypeID, a.RateChanged,a.DeptID FROM      SSClearCustomsFee as a left outer join dbo.SSSupplier AS cust ON cust.ID = a.SupplierOrCustomerID  where a.getorpay=1 and a.status!=-1) AS a ON a.OrderCode = b.OrderCode  LEFT OUTER JOIN dbo.SSCustomerAddress AS address ON  b.SendAddressId = address.ID LEFT OUTER JOIN dbo.MenDian AS m ON m.ID = b.MenDianID LEFT OUTER JOIN dbo.SSPortArea AS port ON b.ImportArea_NO = port.ID LEFT OUTER JOIN dbo.FeeType AS fee ON a.FeeTypeID = fee.ID LEFT OUTER JOIN dbo.Department AS dept ON dept.ID = a.DeptID LEFT OUTER JOIN dbo.VW_FeeCreaterInfo AS users ON users.ID = a.CreaterID AND  users.UserTypeID = a.CreaterTypeID LEFT OUTER JOIN dbo.CWCustomer AS cust ON cust.ID = a.SupplierOrCustomerID LEFT OUTER JOIN dbo.SSSupplier AS cust1 ON cust1.ID = a.SupplierOrCustomerID LEFT OUTER JOIN dbo.CWCustomer AS cw ON cw.ID = b.CustomerID LEFT OUTER JOIN dbo.SSJieDanCustomer AS jdc ON jdc.ID = b.JDCustomerID WHERE   (b.Status >= 0) AND      (a.OrderCode NOT LIKE 'JJ%') AND (a.OrderCode NOT LIKE 'HDC%') AND  (a.Status <> - 1)   )  as a where (BillID is NULL or len(BillID)=0 or BillID=0)  and a.SupplierOrCustomerID=3564 and a.OrderDate <='2019-01-05' and a.OrderDate >='2018-11-01' and a.JobType='5' and a.DeptID=219  and a.GetOrPay=0 and a.Status!=-1  order by OrderCode,FeeTypeID
~~~





