USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[DataCatalog]    Script Date: 8/15/2016 11:20:23 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[DataCatalog](@orgid varchar(10), @reportid varchar(35), @loctype varchar(max), @loctxt varchar(max))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

IF @loctype='HUC'

BEGIN
--BEGIN HUC

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT DATACATEGORY AS 'WC:DataCategory',
	(SELECT WADE_R.DataTypeCatalog(@orgid, @reportid, DATACATEGORY, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.HUC=@loctxt GROUP BY DATACATEGORY FOR XML PATH ('WC:DataAvailable'));
	
END
--END HUC

IF @loctype='COUNTY'
BEGIN
--BEGIN COUNTY

WITH XMLNAMESPACES('ReplaceMe' AS WC)
SELECT @tmp=(SELECT DATACATEGORY AS 'WC:DataCategory',
	(SELECT WADE_R.DataTypeCatalog(@orgid, @reportid, DATACATEGORY, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.COUNTY_FIPS=@loctxt GROUP BY DATACATEGORY FOR XML PATH ('WC:DataAvailable'));	
END
--END COUNTY

IF @loctype='REPORTUNIT'
BEGIN
--BEGIN REPORTUNIT

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT DATACATEGORY AS 'WC:DataCategory',
	(SELECT WADE_R.DataTypeCatalog(@orgid, @reportid, DATACATEGORY, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.REPORT_UNIT_ID=@loctxt GROUP BY DATACATEGORY FOR XML PATH ('WC:DataAvailable'));	
	
END
--END REPORTUNIT

RETURN (@tmp)
		
END



GO


