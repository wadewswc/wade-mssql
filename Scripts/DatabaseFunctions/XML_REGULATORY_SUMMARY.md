USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_REGULATORY_SUMMARY]    Script Date: 8/15/2016 11:35:47 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_REGULATORY_SUMMARY](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35))

RETURNS xml 

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp = (SELECT WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier',
	REGULATORY_TYPE AS 'WC:RegulatoryTypeName', 
	B.VALUE as 'WC:RegulatoryStatusText', 
	OVERSIGHT_AGENCY AS 'WC:OversightAgencyName', 
	REGULATORY_DESCRIPTION AS 'WC:RegulatoryDescriptionText'
	
	FROM  
	
	WADE.SUMMARY_REGULATORY A LEFT JOIN WADE.LU_REGULATORY_STATUS B ON (A.REGULATORY_STATUS=B.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND REPORT_UNIT_ID=@reportunitid 
	
	FOR XML PATH('WC:RegulatoryType'));

IF (@tmp IS NOT NULL)

BEGIN
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp = (SELECT @tmp FOR XML PATH('WC:RegulatorySummary'));

END

RETURN(@tmp)
		
END
GO


