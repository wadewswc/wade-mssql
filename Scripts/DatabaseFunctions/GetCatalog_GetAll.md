USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetCatalog_GetAll]    Script Date: 8/15/2016 11:21:25 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO



CREATE FUNCTION [wade_r].[GetCatalog_GetAll] (@orgid varchar(10))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

BEGIN

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier',
			B.WADE_URL AS 'WC:WaDEURLAddress',
			REPORT_ID AS 'WC:ReportIdentifier',
			DATACATEGORY AS 'WC:DataCategory',
			DATATYPE AS 'WC:DataType',
			A.STATE AS 'WC:State',
			REPORT_UNIT_ID AS 'WC:ReportUnitIdentifier',
			COUNTY_FIPS AS 'WC:CountyFIPS',
			HUC AS 'WC:HUC'
	
			FROM 
			WADE_R.CATALOG_SUMMARY A LEFT JOIN WADE.ORGANIZATION B ON A.ORGANIZATION_ID=B.ORGANIZATION_ID
					
			FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
END

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp)
		
END




GO


