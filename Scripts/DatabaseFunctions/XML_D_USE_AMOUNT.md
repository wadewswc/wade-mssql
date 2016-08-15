USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_USE_AMOUNT]    Script Date: 8/15/2016 11:35:23 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_D_USE_AMOUNT](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(60), @useid numeric(18,0))

RETURNS xml 

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT AMOUNT_VOLUME AS 'WC:AmountNumber',
	C.VALUE AS 'WC:AmountUnitsCode',
	D.DESCRIPTION AS 'WC:ValueTypeCode',
	METHOD_CONTEXT AS 'WC:Method/WC:MethodContext',
	METHOD_NAME AS 'WC:Method/WC:MethodName',
	START_DATE AS 'WC:TimeFrame/WC:TimeFrameStartName',
	END_DATE AS 'WC:TimeFrame/WC:TimeFrameEndName'
 
	FROM 
	
	WADE.D_USE_AMOUNT A LEFT JOIN WADE.METHODS B ON (A.METHOD_ID_VOLUME=B.METHOD_ID)
	LEFT JOIN WADE.LU_UNITS C ON (A.UNIT_VOLUME=C.LU_SEQ_NO) LEFT JOIN WADE.LU_VALUE_TYPE D ON (A.VALUE_TYPE_VOLUME=D.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND WATER_USER_ID=@wateruserid AND BENEFICIAL_USE_ID=@useid 
	
	FOR XML PATH ('WC:UseVolume'));
	
RETURN(@tmp)	

END
GO


