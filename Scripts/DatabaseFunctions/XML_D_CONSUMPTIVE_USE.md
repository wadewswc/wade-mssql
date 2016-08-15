USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_CONSUMPTIVE_USE]    Script Date: 8/15/2016 11:34:27 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_CONSUMPTIVE_USE](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(50))
  RETURNS XML

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT 
	B.CONTEXT AS 'WC:BeneficialUseContext',
	B.VALUE as 'WC:BeneficialUseTypeName',
	
	(SELECT WADE_R.USE_AMOUNT (@orgid, @reportid, @allocationid, @wateruserid))
	
	FROM  
	WADE.D_CONSUMPTIVE_USE A LEFT OUTER JOIN WADE.LU_BENEFICIAL_USE B ON (A.BENEFICIAL_USE_ID=B.LU_SEQ_NO) 
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND WATER_USER_ID=@wateruserid 
	
	FOR XML PATH('WC:UseEstimate'));

RETURN(@tmp)
		
END
GO


