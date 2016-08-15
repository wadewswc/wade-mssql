USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_AVAILABILITY_SUMMARY]    Script Date: 8/15/2016 11:33:30 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_AVAILABILITY_SUMMARY](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35)) 
RETURNS xml

BEGIN

DECLARE @tmp XML='';

;WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier',
			AVAILABILITY_TYPE AS 'WC:AvailabilityTypeName',
			B.VALUE AS 'WC:FreshSalineIndicator', 
			C.VALUE AS 'WC:SourceTypeName',
			(SELECT (SELECT WADE_R.XML_S_AVAILABILITY_AMOUNT(@orgid, @reportid, @reportunitid, SUMMARY_SEQ)),
			(SELECT WADE_R.XML_S_AVAILABILITY_METRIC(@orgid, @reportid, @reportunitid, SUMMARY_SEQ)) FOR XML PATH('WC:AvailabilityEstimate'), type)
	   
	   FROM
	   
	   WADE.SUMMARY_AVAILABILITY A LEFT JOIN WADE.LU_FRESH_SALINE_INDICATOR B ON (A.FRESH_SALINE_IND=B.LU_SEQ_NO) LEFT JOIN WADE.LU_SOURCE_TYPE C ON (A.SOURCE_TYPE=C.LU_SEQ_NO)
	   
	   WHERE
	   
	   ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND REPORT_UNIT_ID=@reportunitid FOR XML PATH ('WC:AvailabilitySummary'));

RETURN (@tmp)
END	   

GO


