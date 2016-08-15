USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[ReportSummary]    Script Date: 8/15/2016 11:32:45 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[ReportSummary](@orgid varchar(10), @reportid varchar(35), @loctype varchar(max), @loctxt varchar(max), @datatype varchar(60))
  RETURNS xml

BEGIN

DECLARE @tmp XML;

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT REPORT_ID AS 'WC:ReportIdentifier', 
	REPORTING_DATE as 'WC:ReportingDate', 
	REPORTING_YEAR AS 'WC:ReportingYear', 
	REPORT_NAME AS 'WC:ReportName', 
	REPORT_LINK AS 'WC:ReportLink', 
	YEAR_TYPE AS 'WC:YearType',
	(SELECT wade_r.GeospatialRefSummary (@orgid, @reportid, @datatype)),
	(SELECT wade_r.ReportUnitSummary (@orgid, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	wade.REPORT WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid 
	
	FOR XML PATH('WC:Report'))

RETURN (@tmp)
		
END

GO


