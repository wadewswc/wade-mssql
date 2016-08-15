USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[LocationCatalog]    Script Date: 8/15/2016 11:22:13 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[LocationCatalog](@orgid varchar(10), @reportid varchar(35), @loctype varchar(max), @loctxt varchar(max))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

IF @loctype='HUC'

BEGIN
--BEGIN HUC

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT 'HUC' AS 'WC:LocationType',
	HUC AS 'WC:LocationText',
	(SELECT WADE_R.DataCatalog(@orgid, @reportid, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.HUC=@loctxt GROUP BY HUC FOR XML PATH ('WC:Location'));
	
END
--END HUC

IF @loctype='COUNTY'
BEGIN
--BEGIN COUNTY

WITH XMLNAMESPACES('ReplaceMe' AS WC)
SELECT @tmp=(SELECT 'COUNTY' AS 'WC:LocationType',
	COUNTY_FIPS AS 'WC:LocationText',
	(SELECT WADE_R.DataCatalog(@orgid, @reportid, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.COUNTY_FIPS=@loctxt GROUP BY COUNTY_FIPS FOR XML PATH ('WC:Location'));
END
--END COUNTY

IF @loctype='REPORTUNIT'
BEGIN
--BEGIN REPORTUNIT

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT 'REPORTUNIT' AS 'WC:LocationType',
	REPORT_UNIT_ID AS 'WC:LocationText',
	(SELECT WADE_R.DataCatalog(@orgid, @reportid, @loctype, @loctxt))
	
	FROM 
	
	WADE_R.CATALOG_SUMMARY B WHERE B.ORGANIZATION_ID=@orgid AND B.REPORT_ID=@reportid 
	AND B.REPORT_UNIT_ID=@loctxt GROUP BY REPORT_UNIT_ID FOR XML PATH ('WC:Location'));
	
END
--END REPORTUNIT

RETURN (@tmp)
		
END



GO


