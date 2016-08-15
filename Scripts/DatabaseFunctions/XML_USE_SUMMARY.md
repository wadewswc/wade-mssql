USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_USE_SUMMARY]    Script Date: 8/15/2016 11:37:09 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_USE_SUMMARY](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35))
  RETURNS xml 

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier',
		B.CONTEXT AS 'WC:WaterUseContext',
		B.VALUE as 'WC:WaterUseTypeName', 
		(SELECT C.VALUE AS 'WC:FreshSalineIndicator',
		D.VALUE AS 'WC:SourceTypeName', 
		POWER_GENERATED AS 'WC:PowerGeneratedNumber', 
		POPULATION_SERVED AS 'WC:PopulationServedNumber',
			(SELECT WADE_R.XML_S_USE_IRRIGATION (@orgid, @reportid, @reportunitid, SUMMARY_SEQ, BENEFICIAL_USE_ID)),
			(SELECT WADE_R.XML_S_USE_AMOUNT (@orgid, @reportid, @reportunitid, SUMMARY_SEQ, BENEFICIAL_USE_ID)) FOR XML PATH ('WC:WaterUseAmountSummary'), type)
			
	FROM  
	
	WADE.SUMMARY_USE A LEFT OUTER JOIN WADE.LU_BENEFICIAL_USE B ON (A.BENEFICIAL_USE_ID=B.LU_SEQ_NO) LEFT JOIN WADE.LU_FRESH_SALINE_INDICATOR C ON (A.FRESH_SALINE_IND=C.LU_SEQ_NO)
	LEFT JOIN WADE.LU_SOURCE_TYPE D ON (A.SOURCE_TYPE=D.LU_SEQ_NO)
		
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND REPORT_UNIT_ID=@reportunitid 
	
	FOR XML PATH('WC:WaterUse'));
	
If (@tmp IS NOT NULL)
BEGIN
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT @tmp FOR XML PATH('WC:WaterUseSummary'));

END

RETURN(@tmp)
		
END
GO


