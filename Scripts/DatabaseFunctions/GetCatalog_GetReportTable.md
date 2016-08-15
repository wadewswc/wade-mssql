USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetCatalog_GetReportTable]    Script Date: 8/15/2016 11:21:41 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO



CREATE FUNCTION [wade_r].[GetCatalog_GetReportTable] (@orgid varchar(10))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

BEGIN

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT ORGANIZATION_ID AS 'WC:OrganizationIdentifier',
			REPORT_ID AS 'WC:ReportIdentifier',
			REPORTING_DATE AS 'WC:ReportingDate',
			REPORTING_YEAR AS 'WC:ReportingYear',
			REPORT_NAME AS 'WC:ReportName',
			REPORT_LINK AS 'WC:ReportLink',
			YEAR_TYPE AS 'WC:YearType'
	
			FROM 
			WADE.REPORT
					
			FOR XML PATH('WC:CatalogReport'), ROOT('WC:WaDECatalog'));
END

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp)
		
END




GO


