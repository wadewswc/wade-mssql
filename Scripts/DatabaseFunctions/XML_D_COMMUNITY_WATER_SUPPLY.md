USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_COMMUNITY_WATER_SUPPLY]    Script Date: 8/15/2016 11:34:19 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_COMMUNITY_WATER_SUPPLY](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(50), @useid numeric(18,0))
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT POPULATION_SERVED AS 'WC:TotalPopulationServedNumber',
	WATER_SUPPLY_NAME AS 'WC:CommunityWaterSupplyName' 
 
	FROM
	
	WADE.D_COMMUNITY_WATER_SUPPLY WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid 
	AND WATER_USER_ID=@wateruserid AND BENEFICIAL_USE_ID=@useid 
	
	FOR XML PATH('WC:CommunityWaterSupply'));

RETURN (@tmp)
END
GO


