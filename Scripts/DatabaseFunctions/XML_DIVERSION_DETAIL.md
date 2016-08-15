USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_DIVERSION_DETAIL]    Script Date: 8/15/2016 11:35:39 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_DIVERSION_DETAIL](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60)) 
RETURNS XML

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT DIVERSION_ID AS 'WC:DiversionIdentifier',
	DIVERSION_NAME AS 'WC:DiversionName',
	F.VALUE AS 'WC:DetailLocation/WC:StateCode', 
	REPORTING_UNIT_ID AS 'WC:DetailLocation/WC:ReportingUnitIdentifier', 
	COUNTY_FIPS AS 'WC:DetailLocation/WC:CountyFipsCode',
	HUC AS 'WC:DetailLocation/WC:HydrologicUnitCode',
	WFS_FEATURE_REF AS 'WC:DetailLocation/WC:WFSReference/WC:WFSFeatureIdentifier',
	
	(SELECT WADE_R.DIVERSION_AMOUNT(@orgid, @reportid, @allocationid, DIVERSION_ID))

	FROM  
	
	WADE.DETAIL_DIVERSION A LEFT JOIN WADE.LU_STATE F ON (A.STATE=F.LU_SEQ_NO) 
		
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid 
	
	FOR XML PATH('WC:Diversion'));
	
RETURN (@tmp)
 
END
GO


