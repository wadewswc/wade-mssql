USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_USE_LOCATION]    Script Date: 8/15/2016 11:35:32 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_D_USE_LOCATION](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(60))
  RETURNS xml 

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT B.VALUE AS 'WC:StateCode', 
	REPORTING_UNIT_ID AS 'WC:ReportingUnitIdentifier', 
	COUNTY_FIPS AS 'WC:CountyFipsCode', 
	HUC AS 'WC:HydrologicUnitCode',
	WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier'
	
	FROM 
	
	WADE.D_USE_LOCATION A LEFT JOIN WADE.LU_STATE B ON (A.STATE=B.LU_SEQ_NO) 
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND WATER_USER_ID=@wateruserid
	
	FOR XML PATH ('WC:DetailLocation'));
	
RETURN (@tmp)	

END
GO


