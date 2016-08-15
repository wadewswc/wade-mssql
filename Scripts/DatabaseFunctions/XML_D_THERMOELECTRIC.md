USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_THERMOELECTRIC]    Script Date: 8/15/2016 11:35:16 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_THERMOELECTRIC](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(50), @useid numeric(18,0)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT VALUE AS 'WC:GeneratorTypeName',
	POWER_CAPACITY AS 'WC:PowerCapacityNumber'
	
	FROM     
	
	WADE.D_THERMOELECTRIC A LEFT JOIN WADE.LU_GENERATOR_TYPE B ON (A.GENERATOR_TYPE=B.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND WATER_USER_ID=@wateruserid AND BENEFICIAL_USE_ID=@useid 
	
	FOR XML PATH('WC:ThermoElectricWaterSupply'));
	
RETURN(@tmp)
 
END
GO


