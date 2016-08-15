USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_ALLOCATION_LOCATION]    Script Date: 8/15/2016 11:33:49 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_ALLOCATION_LOCATION](@orgid varchar(10), @reportid varchar(35), @loctype varchar(max), @loctxt varchar(max),@allocationid varchar(60)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT @loctype AS 'WC:PrimaryLocationType',
	@loctxt AS 'WC:PrimaryLocationText',
	B.VALUE AS 'WC:StateCode',
	REPORTING_UNIT_ID AS 'WC:ReportingUnitIdentifier',
	COUNTY_FIPS AS 'WC:CountyFipsCode',
	HUC AS 'WC:HydrologicUnitCode',
	WFS_FEATURE_REF AS 'WC:WFSReference/WC:WFSFeatureIdentifier'
	
	FROM  
	
	WADE.D_ALLOCATION_LOCATION A LEFT JOIN WADE.LU_STATE B ON (A.STATE=B.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid
	
	FOR XML PATH('WC:DetailLocation'));
	
RETURN (@tmp)
 
END
GO


