USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_RETURNFLOW_DETAIL]    Script Date: 8/15/2016 11:35:54 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_RETURNFLOW_DETAIL](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60))
  RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp= (SELECT RETURN_FLOW_ID AS 'WC:ReturnFlowIdentifier',
	RETURN_FLOW_NAME AS 'WC:ReturnFlowName',
	B.VALUE AS 'WC:DetailLocation/WC:StateCode', 
	REPORTING_UNIT_ID AS 'WC:DetailLocation/WC:ReportingUnitIdentifier', 
	COUNTY_FIPS AS 'WC:DetailLocation/WC:CountyFipsCode', 
	HUC AS 'WC:DetailLocation/WC:HydrologicUnitCode',
	WFS_FEATURE_REF AS 'WC:DetailLocation/WC:WFSReference/WC:WFSFeatureIdentifier',
	(SELECT WADE_R.XML_D_RETURN_FLOW_ACTUAL(@orgid, @reportid, @allocationid, RETURN_FLOW_ID))

	FROM 

	WADE.DETAIL_RETURN_FLOW A LEFT JOIN WADE.LU_STATE B ON (A.STATE=B.LU_SEQ_NO)

	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid 
	
	FOR XML PATH('WC:ReturnFlow'));
	
RETURN (@tmp)

END
GO


