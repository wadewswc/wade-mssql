USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_USE_DETAIL]    Script Date: 8/15/2016 11:37:01 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_USE_DETAIL](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60))
  RETURNS xml 

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT WATER_USER_ID AS 'WC:UserIdentifier',
	WATER_USER_NAME AS 'WC:UserName', 
	(SELECT WADE_R.XML_D_USE_LOCATION(@orgid, @reportid, @allocationid, WATER_USER_ID)),
	(SELECT WADE_R.XML_D_CONSUMPTIVE_USE(@orgid, @reportid, @allocationid, WATER_USER_ID))
	
	FROM 
	
	WADE.DETAIL_USE WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid 
	
	FOR XML PATH('WC:ConsumptiveUse'));

RETURN (@tmp)

END
GO


