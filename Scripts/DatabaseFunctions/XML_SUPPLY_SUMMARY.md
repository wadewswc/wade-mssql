USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_SUPPLY_SUMMARY]    Script Date: 8/15/2016 11:36:52 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_SUPPLY_SUMMARY](@orgid varchar(10), 
		@reportid varchar(35), @reportunitid varchar(35))

RETURNS xml

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier',
		B.VALUE AS 'WC:WaterSupplyTypeName',
		(SELECT WADE_R.XML_S_WATER_SUPPLY_AMOUNT(@orgid, @reportid, @reportunitid, SUMMARY_SEQ))
	
	FROM
		
	WADE.SUMMARY_WATER_SUPPLY A LEFT JOIN WADE.LU_WATER_SUPPLY_TYPE B ON (A.WATER_SUPPLY_TYPE=B.LU_SEQ_NO)
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid
		AND REPORT_UNIT_ID=@reportunitid 
		
		FOR XML PATH ('WC:DerivedWaterSupplyType'));
		
IF (@tmp IS NOT NULL)
BEGIN

WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp = (SELECT @tmp FOR XML PATH('WC:DerivedWaterSupplySummary'));
	
END
RETURN (@tmp)
END

GO


