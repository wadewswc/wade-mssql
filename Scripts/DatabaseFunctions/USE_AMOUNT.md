USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[USE_AMOUNT]    Script Date: 8/15/2016 11:33:06 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[USE_AMOUNT](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(60))
  RETURNS XML

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT C.VALUE AS 'WC:SourceTypeName',
	B.VALUE AS 'WC:FreshSalineIndicator',
	SOURCE_NAME AS 'WC:SourceName',
	(SELECT WADE_R.XML_D_COMMUNITY_WATER_SUPPLY(@orgid, @reportid, @allocationid, @wateruserid, BENEFICIAL_USE_ID)),
	(SELECT WADE_R.XML_D_IRRIGATION(@orgid, @reportid, @allocationid, @wateruserid, BENEFICIAL_USE_ID)),
	(SELECT WADE_R.XML_D_THERMOELECTRIC(@orgid, @reportid, @allocationid, @wateruserid, BENEFICIAL_USE_ID)),
	(SELECT WADE_R.XML_D_USE_AMOUNT(@orgid, @reportid, @allocationid, @wateruserid, BENEFICIAL_USE_ID))
	
	FROM 
	
	WADE.D_CONSUMPTIVE_USE A LEFT JOIN WADE.LU_FRESH_SALINE_INDICATOR B ON (A.FRESH_SALINE_IND=B.LU_SEQ_NO) LEFT JOIN WADE.LU_SOURCE_TYPE C ON (A.SOURCE_TYPE=C.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid and WATER_USER_ID=@wateruserid
	
	FOR XML PATH(''));

If (@tmp IS NOT NULL)
BEGIN
WITH XMLNAMESPACES ('ReplaceMe' AS WC)
SELECT @tmp=(SELECT @tmp FOR XML PATH('WC:UseAmount'));
END
RETURN (@tmp)

END
GO


